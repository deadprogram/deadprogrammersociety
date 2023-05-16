---
title: 'On The Grid With EC2'
date: 2008-01-12T10:08:00.000-08:00
draft: false
url: /2008/01/on-grid-with-ec2.html
tags: 
- sinatra
- ubuntu
- ec2
- ruby
- s3
- ruby on rails
- grid computing
---

[![](http://www.musicbox-online.com/images/complete-on-the-corner.jpg)](http://www.musicbox-online.com/images/complete-on-the-corner.jpg)Lately, I have had a chance to get seriously into [Amazon's Elastic Compute Cloud (EC2)](http://aws.amazon.com/ec2) service. I doubt any reader of this blog is unfamiliar with the existence of EC2, but many of you have probably not even gotten to the tire kicking stage, like I had been until recently.  
  
Even after attending several sessions about Amazon's EC2 at RailsConf 2007, I still had only a very general idea about the service. However, it is true that there is no substitute for experience, and now that I have finally been getting hands-on, I am pretty excited about what you can do with it.  
  
A client with a pretty complex Ruby on Rails application needed to create a processing farm for doing video conversion, as well as serving up the resulting video files. Sounds like the perfect application for Amazon's utility computing services. I dug in to the myriad of online sources of information available...  
  
I decided to base my Amazon Machine Image (AMI) on [Ubuntu](http://www.ubuntu.com/) 7.1. Oh, Ubuntu, such a modern operating system you are! That turned out to be a very good decision, and apt-get was quite co-operative getting the myriad of prerequisites my open source video processing farm would require.  
  
I also decided to base my upload processor on [Sinatra](http://sinatra.rubyforge.org/). My application's entrypoint is a single stateless call, but there are lots of these calls, and each requires a bunch of intensive back-end processing. Something nice and multithreaded, like some kind of mongrel handler, was called for. In this case, even [Merb](http://merbivore.com/) seemed like it was too heavyweight!  
  
Luckily, I had colleague [Ari Lerner](http://blog.xnot.org/) available to help me strap Sinatra into my processing farm, who proved to be indispensable. We ran into some issues with [Rack](http://rack.rubyforge.org/), which I am sure Ari will be blogging about. Thanks, Ari, you are the man.  
  
  
Some lessons learned about working with EC2 and S3:  

  
*   When you can launch a new instance whenever you want, you can really work on your machine configurations in an iterative way. Treat your AMI like source code, and don't be afraid to bundle and upload iterations of the AMI as you go along. If you mess up something, you will be glad you did. And there is no bandwidth charge between EC2 and S3 so go ahead, pile it into S3! At $0.15 per GB-Month of storage used, you cannot afford not to.
  
  
*   Amazon provides very [complete instructions on how to create an image](http://docs.amazonwebservices.com/AWSEC2/2007-08-29/GettingStartedGuide/creating-an-image.html). When you are "developing" an AMI, by iteratively modifying a running instance, and re-bundling and re-uploading, you can skip the step of uploading your keys. However, you will need to delete /mnt/image before you can re-run the "ec2-bundle-vol" utility, or else you get an "the specified image file /mnt/image already exists" error.
  
  
*   You can get DRY with your AMIs. You can use a single AMI, and pass in launch parameters to set various configuration settings. For example, when I launch a processor instance, I use my main AMI and just pass in the required launch parameters to tell it if is staging or production, and which pool of processors to join itself to. And how do you retrieve this individual instance data at runtime? You [use a REST call](http://docs.amazonwebservices.com/AWSEC2/2007-03-01/DeveloperGuide/AESDG-chapter-instancedata.html) to get it. Neat!
  
  
*   At some point, I did something wrong with the code that generated keys for each file I was saving to S3, which in S3 corresponds to the path and file name. For whatever reason, it messed up, and I could not even delete the S3 objects using the [S3 Firefox Organizer](https://addons.mozilla.org/en-US/firefox/addon/3247)! Fortunately, the somewhat ugly, but much more functional [Bucket Explorer](http://www.bucketexplorer.com/) was able to get rid of the offending files.
  
  
*   To really take advantage of the distributed nature of the solution, I decided to use a client-side load balancing scheme like that described by Lei Zhu in [this article](http://www.digital-web.com/articles/client_side_load_balancing/).  
      
    The solution described does load balancing without a separate load balancer. It accomplishes this as follows: when a new processing node comes online, it registers itself by saving its name into a special bucket. Any server listed in this special bucket is available to serve requests. Add in regular peer to peer checking to verify that a node has not gone offline, and the peer removes it from the bucket. If that node, or a replacement, comes online, it will register itself. And so on... Zhu's solution is both effective and minimalist.  
      
    As I said, the solution proposed at the end of the article was really cool, but no actual code was provided, since it is part of what appears to be the codebase for the author's startup company. So, I decided to implement it myself, which proved to be really fun and easy. A fully Ruby-based client side load balancer for EC2 is a pretty useful thing to have around. If anyone else is interested, I will publish as a gem or something.
  

  
  
We are not quite finished with our video processing farm, but it is almost there, and the results are a surprisingly small amount of code. I am been extremely impressed by the relative ease with which we have put together a pretty sophisticated solution.  
  
Grid computing... it's not just the future, it's the present.