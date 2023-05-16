---
title: 'Beware Of The Merb'
date: 2008-01-14T14:56:00.000-08:00
draft: false
url: /2008/01/beware-of-merb.html
tags: 
- merb
- ruby
---

[![](http://media.npr.org/programs/wesat/features/2005/july/blob200.jpg)](http://media.npr.org/programs/wesat/features/2005/july/blob200.jpg)Apparently the [Merb](http://merbivore.com/) team was not yet satisfied with just having created a better Rails than Rails itself. Now, they are going after even more conceptual high ground, and creating an even more flexible web development paradigm that incorporates many of the great ideas percolating around the mongrel community.  
  
According to Yahuda Katz, the next version of Merb will completely revise the existing Merb framework, in order to provide for many more ways to utilize it. He has an [excellent writeup](http://yehudakatz.com/2008/01/14/merbnext/) about what they are up to, and it sounds really cool.  
  
The upcoming Merb 0.9 will break Merb into two parts: merb-core, and merb-more. merb-core will be a separate gem based on Rack, and as such will be able to plug into any web server like mongrel, evented\_mogrel, thin, or even the venerable WebBrick. With this stripped down merb-core, you could create mini one file applications like those that you might been thinking of doing with Sinatra or Camping. Back to the Merb roots, if you will.  
  
The other part of the new Merb, is the merb-more gem, which supports a more complete application structure like Rails or the current Merb. Combine this with a bunch of plugins, and the new Merb sounds to be an excellent way to really recombine elements to create an application.  
  
I will be checking it out as soon as practical... stay tuned for more Merb.