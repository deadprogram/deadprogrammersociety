---
title: 'Sparkline Some Interest With Ruby on Rails'
date: 2010-01-12T12:12:00.000-08:00
draft: false
url: /2010/01/sparkline-some-interest-with-ruby-on.html
tags: 
- sparkline
- ruby
- charting
- ruby on rails
---

![](http://farm1.static.flickr.com/29/62568004_cb569e408c.jpg)Recently, I added some [sparkline](http://en.wikipedia.org/wiki/Sparkline) graphs to a Ruby on Rails application. A sparkline is a very small graphic that displays a large amount of information, typically shown over time, and usually embedded in some other text. Invented by the father of modern infographics [Edward Tufte](http://www.edwardtufte.com), the sparkline has become a fixture of many online applications that want to visually display some stats in a simple, integrated way.  
  
When it come to adding sparklines into a Ruby on Rails application, there are a couple of different options. You can chart the data on the server, output being an image file. You can also chart the data on the client, with a couple of different JavaScript libraries as available options.  
  
I started my plan, intending to implement my charts on the client-side. The project that appears to have the most flexibility, speed, and options, is an amazing jQuery plugin called [jQuery Sparkline](http://omnipotent.net/jquery.sparkline/). Unfortunately, the project to which I needed to add the sparklines is a bit older, and does not use jQuery. As a result, I was not able to use jQuery Sparkline for this current project.  
  
Another interesting JavaScript sparkline library is [lethain's Sparkline.js](http://github.com/lethain/sparklines.js), but it has not been updated in some time, and is not compatible with current Internet Explorer versions. There is also an interesting looking newer lib [topfunky-sparkline-js](http://github.com/topfunky/topfunky-sparkline-js) but I have not tried it out yet.  
  
So that brings us to server-side sparkline generation. If you are using ImageMagick/RMagick then @topfunky once again provides, with the Ruby [sparklines gem](http://github.com/topfunky/sparklines). This gem provides lots of options for doing all sorts of fancy sparklines.  
  
In my case, I am not using ImageMagick for anything else, so I did not want to install it just for this. What I really wanted was something much lighter-weight, and I was willing to accept a lot fewer options to get it.  
  
It turns out that [madrobby](http://twitter.com/madrobby) has written a library for generating very simple sparklines in pure Ruby code, called [spark\_pr](http://github.com/madrobby/spark_pr). The project uses \_why's pure Ruby implementation of a PNG generator to do the low-level work.  
  
spark\_pr has also spawned an interesting application of it from [@technoweenie](http://twitter.com/technoweenie) called [Sparkplug](http://rack-sparklines.heroku.com/), which is a Rack module that generates spaklines from CSV data on the fly, using Rack handlers and Rack caching.  
  
Once I had seen Sparkplug's minimal elegance, it seemed spark\_pr was the option for me. I decided to incorporate spark\_pr into my application. Given that the app was written with a dedicated approach to keeping a clean RESTful interface, and that the database already contained the time-series data, it was quite easy to incorporate. Here is what I had to do:  
  
Step 1: Put spark\_pr.rb file into lib directory. I just grabbed the code from the repo, and dropped it into my project. You may decide to have a more sophisticated way to do it, such as using git submodules.  
  
Step 2:```
require "spark\_pr"
```in your controller  
  
Step 3:```
include Spark
```in your controller  
  
Step 4: Add PNG format to controller action that was already returning my time-series data, and return the sparkline PNG data:  
  
Note that this controller action is already returning XML or JSON. PNG is just another format to be added, if you have a well-designed RESTful controller action.  
  
Step 5: Put image\_tag that requests the sparkline PNG image file into the view where you want it to appear, like this one:  
  
  
Voila! Refresh that view and you should now be looking at your ultra-hipster-chic sparkline graph. It is surprising how much more information comprehension a person has, when they are seeing a visual representation of their data. Plus it looks cool.