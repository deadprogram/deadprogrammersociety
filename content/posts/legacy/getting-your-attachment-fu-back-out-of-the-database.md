---
title: 'Getting Your attachment_fu Back Out Of The Database'
date: 2007-04-26T13:25:00.000-07:00
draft: false
url: /2007/04/getting-your-attachmentfu-back-out-of.html
tags: 
- attachment_fu
- ruby on rails
---

I have been busy the last few nights incorporating the brilliant Rails plugin called [attachment\_fu](http://svn.techno-weenie.net/projects/plugins/attachment_fu/) from Rick Olson aka [technoweenie](http://weblog.techno-weenie.net/). If you do not know about attachment\_fu, it is a complete solution to the problem of uploading image files attachments to include with your models.  
  
First, I had to get past the initial hurdle of getting ImageScience and FreeImage correctly installed and working on my Mac. Despite the claims that Locomotive should have already had these in the bundle, I had to go thru a small process to get the prerequisites going.  
  
I was then able to easily follow the careful instructions of Mike Clark, who has blogged at some length of [how to get started with attachment\_fu](http://clarkware.com/cgi/blosxom/2007/02/24). In very short order, I had a working upload page, and another page displaying the automatically generated thumbnails. I was happily bragging to myself that "my attachment\_fu has grown powerful, ha ha ha".  
  
Then it occurred to me that using the :file\_system option which stores uploaded files and thumbnails onto the web server's drive, typically into a special part of the "public" directory, was quick and easy, but not very scalable. Suddenly my attachment\_fu is wimpy.  
  
Luckily, attachment\_fu supports the idea of "backends", which are code modules designed to communicate with the backend storage to be used for the images and thumbnails. The three provided backends are the file system, database, and Amazon's S3 storage. I decided that switching to the database storage was the best for my particular application. I changed the configuration option as described by Mike Clark, and ran my app expecting everything to just work...  
  
Boom! Errors up the wazoo. OK, I wade in and discover that there is plenty of hidden away functionality in that plugin. First, the database storage backend requires an additional table called "db\_files" not mentioned in mike clark's blog. The required additional migration is as follows:  
  
```
  
t.column :db\_file\_id, :integer  
  
create\_table :db\_files do |t|  
  t.column :data, :binary  
end  

```  
  
You will need to add the "db\_file\_id" column to the table that stores your attachments. Then you need to create the "db\_files" table to hold the actual binary data for the images and thumbnails.  
  
I made the changes, ran the migration, and then I was able to upload the image. Almost there... However, I was shocked to see an error on the page that was supposed to display said image. Uh-oh!  
  
It turns out that although the mechanism for displaying images which are stored in the file system or in S3 are exposed so they are web server accessible, the database storage engine is not yet fully implemented. Most importantly, the "public\_filename" method is not there. So images get into the database, but there is no convenient way to display them.  
  
At first I thought that I could use the "create\_temp\_file" method. However, a Ruby Tempfile deletes itself when it goes out of scope. Not the right thing, unless you don't mind images that disappear before they are actually displayed in the browser.  
  
Anyhow, I went and after studying the code a bit, made a few changes to attachment\_fu to provide better support. My solution was to add a method to the database backend to render the binary image data on the fly whenever it is requested.  
  
```
  
  def image\_data(thumbnail = nil)  
    if thumbnail.nil?  
      current\_data  
    else  
      thumbnails.find\_by\_thumbnail(thumbnail.to\_s).current\_data  
    end  
  end  

```  
  
To keep things nice and restful, I added support to my User controller to render the image when image format is requested:  
  
```
  
  def show  
    @user = current\_user  
  
    respond\_to do |format|  
      format.html # show.rhtml  
      format.xml  { render :xml => @user.to\_xml }  
      format.jpg do  
        picture = current\_user.picture  
        image = picture.image\_data(:thumb)    
        send\_data (image, :type     => 'image/jpeg',  
            :filename => picture.filename,  
            :disposition => 'inline')  
      end  
    end  
  end  

```  
  
Once this is all completed, displaying the image within a view is simple with a helper:  
  
```
  
  def user\_thumbnail\_tag(user)  
    image\_tag("#{user\_path(user)}.jpg")  
  end  

```  
  
And there you have it. The nice thing about this solution is you can deploy on multiple web servers behind a load balancer without concern. Thanks to the awesome power of attachment\_fu...you have been warned.