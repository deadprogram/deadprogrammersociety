---
title: 'Merb Is The Word'
date: 2006-12-14T10:29:00.000-08:00
draft: false
url: /2006/12/merb-is-word.html
tags: 
- merb
- rails
- ruby
---

[![](http://www.reproducts.de/museum/2001/0102_peewee/peewee.jpg)](http://www.reproducts.de/museum/2001/0102_peewee/peewee.jpg)I have been playing around with [Merb](http://merb.rubyforge.org/), which is a very cool project from [Ezra Zygmuntowicz](http://brainspl.at/). Merb combines the [Mongrel web server](http://mongrel.rubyforge.org/) with a lightweight Ruby web framework. It has way less stuff in it than Rails, but is somewhat more than [Camping](http://redhanded.hobix.com/bits/campingAMicroframework.html).  
Where this all started, was that I was looking for some way to use Mongrel to create a new REST web service for a client. This service has no UI, and basically just needs to front end a Ruby DSL that I have been working on. Another need was that I had to have something that can easily handle multithreading. Rails will block on a single thread, and also I do not need all of the Rails AJAXy goodness. So Rails seemed like a bit too much, and Camping not quite enough.  
It was at this point that I discovered Merb. Merb handles threading very simply, by dispatching each new request to a new controller created on a new thread. It also has a very clean and simple support for rendering of HTML, JavaScript, and XML views. In my case, I only really cared about returning XML, so Merb seemed ideal for my needs on this project.  
Starting a new Merb project requires some hand copying of files. There is a sample application included, which helps see some of what Merb can do, as well as showing how to setup your own project. At this point, Merb is very early in its lifecycle, so if you want to use it, prepare for a hands-on experience. The Merb code is very simple and clear, however, so it is not hard to see what is going on under the hood.  
One of the main problems that Merb was designed to solve is better handling of long running server processes. One example of this is uploading files to your web server. Rails will block on each file upload until the upload is completed, which is a recipe for poor performance (read server unresponsive) if you will have a lot of requests to upload big files. The Merb sample app shows how to use Merb to deal with file uploads. And since Merb supports ActiveRecord, you could easily integrate a Rails app with a small Merb app or two to handle some performance bottlenecks.  
Merb is much newer than Rails or Camping, but despite it not being even quite half-baked yet, the parts that are finished are delicious! Looks like it will be a really nice option for an alternative/adjunct to Rails. Now someone just needs to create a generator that lets you start a new Merb project...and some documentation/tutorials.