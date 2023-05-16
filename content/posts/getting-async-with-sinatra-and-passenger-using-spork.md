---
title: 'Getting Async With Sinatra And Passenger Using spork'
date: 2009-01-28T10:31:00.000-08:00
draft: false
url: /2009/01/getting-async-with-sinatra-and.html
tags: 
- sinatra
- asynchronous processing
- ruby
- async
- multithreading
- passenger
- spork
---

[![](http://www.trophybikes.com/content/Image/MISC%20GOODS/SPORK.jpg)](http://www.trophybikes.com/content/Image/MISC%20GOODS/SPORK.jpg)  
Everyone wants it all. In the case of upload processing, this means we want both the convenience of [Sinatra](http://www.sinatrarb.com) coding, plus the performance that a nice process/threading model gives us. Go off and do some work I just assigned you, and don't make me wait around to see you do it.  
  
If you are using [Passenger](http://www.modrails.com), it already is buffering your uploads, and not calling your Sinatra application until the upload is complete. That saves system resources for more important things, like even more uploads. Pretty nice.  
  
But a lot of work often has to take place after the upload is completed. A common example these days would be a video transcoding or image processing server. Once your user has uploaded their file, it would be considerate to let them go off and do something else. Sites like YouTube and Flickr have been doing exactly this for some time.  
  
For certain highly transactional system, a solid message queue would be essential. But more humble needs, like an upload/transcoding/image thumbnail server, does not really need all of those extra moving parts.  
  
Thanks to the power of the underlying Ruby language itself, it is very simple to fork off blocks of code into a separate process. Combining this with Passenger's already pretty robust process handling, and you get a pretty well performing solution with not much coding effort.  
  
But wait... it does not work?! Sure enough, there are issues in the underlying interaction between Passenger and [Rack](http://rack.rubyforge.org/), that you must address, or your long-running code will be just that, long-running, making the user sit there and wait for it to complete before Passenger allows Sinatra to return a response.  
  
Enter [spork](http://github.com/deadprogrammer/spork)... a blatant ripoff of both the spoon and the fork... I mean of the [Spawn](http://github.com/tra/spawn) plugin for Rails, except with no actual Rails stuff in it, of course. spork handles the monkeypatching required to get things working the way they should be, and also lets you run under thin with no code changes should you so wish, like when running in development mode locally.  
  
Anyhow, it may not be a glamorous implement, but it is a useful one. Have a look at spork if you are using Sinatra on Passenger, and you want to get all asynchronous on your users.