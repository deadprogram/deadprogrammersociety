---
title: 'Sinatra and Passenger Back On The Rack'
date: 2009-01-21T08:16:00.000-08:00
draft: false
url: /2009/01/sinatra-and-passenger-back-on-rack.html
tags: 
- sinatra
- ruby
- integrity
- rack
- passenger
---

[![](http://giniann.files.wordpress.com/2007/07/grilled-lamb-rack-with-herbs.jpg)](http://giniann.files.wordpress.com/2007/07/grilled-lamb-rack-with-herbs.jpg)There is a new release of the [Sinatra](http://sinatra.github.com/) gem, version 0.9.1. This happens to work out well, since the newest [Passenger](http://www.modrails.com/) 2.0.6 has a strong dependency on [Rack](http://rack.rubyforge.org/) 0.9, and the previous Sinatra 0.3 simply did not work at all due to dependency on Rack 0.4. The last few days have had some of us apoplectic over Ruby gem version hell.  
  
And lots of interesting and even important things require all three. For example, I have been messing around with [Integrity](http://integrityapp.com/), a very cool little continuous integration server which is built using Sinatra. [Foca](http://foca.tumblr.com/) and the rest of Team Integrity are still struggling with upgrading a morass of [DataMapper](http://datamapper.org) gems, but this should help.  
  
The point here, is getting everything up on Rack 0.9 seem to have made these problems go away, at least for my own Sinatra-based projects. Thanks to everyone who worked on these new releases, and special thanks to the IRC dwellers that provide support for the community.