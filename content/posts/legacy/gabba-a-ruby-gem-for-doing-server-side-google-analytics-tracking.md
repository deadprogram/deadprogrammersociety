---
title: 'Gabba: A Ruby Gem For Doing Server Side Google Analytics Tracking'
date: 2010-11-30T23:05:00.000-08:00
draft: false
url: /2010/11/gabba-ruby-gem-for-doing-server-side.html
tags: 
- rails
- ruby
- ruby on rails
- google analytics
---

[![](http://www.thehype.fm/wp-content/uploads/2009/05/yo-gabba.jpg)](http://www.thehype.fm/wp-content/uploads/2009/05/yo-gabba.jpg)  
Yo, Gabba! Gabba, hey? [Gabba](https://github.com/hybridgroup/gabba) is a Ruby gem to do easy server-side [Google Analytics](http://google.com/analytics/) tracking of page view and custom events. Gather around and I'll show you how it works.  
  
Google Analytics is the gold standard of website traffic reporting. In addition to tracking page views, one of the interesting capabilities it has is to track custom events. These could be shopping cart checkouts or video plays from clicking on a button in a Flash player.  
  
The way that Google Analytics is implemented is using the typical tracking image technique. An image is fetched from the server, and based on the infomation pased with this request, the information about the visit is tracked. One twist on this is that Google Analytics generates the tag for the "traxel" using a piece of asynchronous JavaScript. This means that clients without javascript are not able to use Google Analytics to track visitor metrics... or does it?  
  
There is another lesser-known way to integrate that can generate the needed info entirely on the server. This is normally used to handle older mobile browsers that do not have JavaScript implementations. Since all you are doing is fetching a 1x1 pixel GIF image, all you really need is the magic URL.  
  
This is in fact exactly what you would need to do if you want to track custom events, the only real difference being the specific parameters passed to Google Analytics.  
  
There are a number of cases where you might want to track custom events for non-browser devices or other unique situations. Tracking when a purchase is completed, or when a video is played by Flash player or a phone call is initiated, are just a few things you might want to track entirely on the server, with no browser interaction at all.  
  
I did a bit of searching, but did not find any Ruby library that did what I needed. You know what that means! Fire up the editor, I'm going in! And that is how the gabba gem was born.  
  
It is very easy to use:  
```
  
\# track page views  
Gabba::Gabba.new("UT-1234", "mydomain.com").page\_view("something", "track/me")  
  
\# or track custom events  
Gabba::Gabba.new("UT-1234", "mydomain.com").event("Videos", "Play", "ID", "123")  

```  
  
That is all there is to using it. Simple way to get server side Google Analytics tracking of page view and custom events. Fork [gabba](https://github.com/hybridgroup/gabba) on github, or just "gem install gabba" and start tracking all your fun stuff.