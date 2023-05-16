---
title: 'Making S3 Folders In Ruby'
date: 2008-01-11T17:26:00.000-08:00
draft: false
url: /2008/01/making-s3-folders-in-ruby.html
tags: 
- ruby
- s3
- s3 folders
---

[![](http://baseballcrank.com/RaidersWarehouse.jpg)](http://baseballcrank.com/RaidersWarehouse.jpg)Amazon's S3 storage service is a really cool way to store and serve up massive quantities of data. Interestingly, it is more like a database than like a file system. Despite the convenience of referring to an object like "/path/to/thing.jpg" S3 really does not have any separate objects for "/path" or "/path/to". In fact, neither "/path" nor "/path/to" even exist.  
  
This is why, when you store an S3 object, the name it is given is called "key" instead of "filename". It functions like a database key, returning a file. However, as very "ultra hipster Web 2.0" as this may be, it is still convenient to browse a large collection of files by using a familiar directory/sub-directory/etc.  
  
In fact, all of the S3 utilities that I use allow you to create a folder inside of a bucket, and sub-folders inside of that etc. But I did not see any programmatic facility for creating a folder independent of any object inside of S3. If you have been paying attention, you remember that in S3 there is no such thing as a directory! So how do these nice GUI browsers do it?  
  
I did some Googling, but no luck, beyond "it couldn't be done". Since I had two different programs that already did it, I knew THAT wasn't the case. It took a little old-fashioned investigation... I looked directly at the output from a query to a bucket that had the little folders in them already.  
  
Lo and behold, it turns out, they cheat, by creating a specially named object for each "directory". For a directory named "/path", you would create an object with the key "path\_$folder$", and for a directory named "/path/to", you create an object with the key "path/to\_$folder$". Then to get a directory listing for "/path" you just do a query on S3 for all object whose key starts with "/path". Ignore any objects that end with "\_$folder$" and there you have it: S3 folders.  
  
I decided that it would be nice if the aws/s3 gem would support this foldering the same way that copying a file within a file system does: if the enclosing directories do not exist, they are created before the file copy.  
  
Thanks to the beauty of modern dynamic languages, I was easily able to put together a little monkeypatch for aws/S3 to the S3Object class, that handles this.  
  
```
# This is an extension to S3Object that supports the emerging 'standard' for virtual folders on S3.  
# For example:  
#   S3Object.store('/folder/to/greeting.txt', 'hello world!', 'ron', :use\_virtual\_directories => true)  
#  
# This will create an object in S3 that mimics a folder, as far as the S3 GUI browsers like  
# the S3 Firefox Extension or Bucket Explorer are concerned.  
module AWS  
 module S3  
 class S3Object  
 class << self  
           
        alias :original\_store :store  
        def store(key, data, bucket \= nil, options \= {})  
          store\_folders(key, bucket, options) if options\[:use\_virtual\_directories\]  
          original\_store(key, data, bucket, options)  
        end  
    
        def store\_folders(key, bucket \= nil, options \= {})  
          folders \= key.split("/")  
          folders.slice!(0)  
          folders.pop  
          current\_folder \= "/"  
          folders.each {|folder|  
            current\_folder += folder  
            store\_folder(current\_folder, bucket, options)  
            current\_folder += "/"  
          }  
        end  
    
        def store\_folder(key, bucket \= nil, options \= {})  
          original\_store(key + "\_$folder$", "", bucket, options) # store the magic entry that emulates a folder  
        end  
      end  
    end  
  end  
end
```  
  
Sure, you can have the best of both worlds: massive virtual storage, and a convenient directory-like structure. And now you can have it with your favorite Ruby S3 library.  
  
Happy storage!