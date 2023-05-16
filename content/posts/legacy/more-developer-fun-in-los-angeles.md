---
title: 'More Developer Fun In Los Angeles'
date: 2007-10-24T08:17:00.000-07:00
draft: false
url: /2007/10/more-developer-fun-in-los-angeles.html
tags: 
- rails
- cruisecontrol.rb
- iphone
- ruby on rails
- domain specific languages
- web development
- merb
- silverlight
- sinatra
- ruby
- los angeles
- test-driven development
---

[![](http://www.glendalepoa.org/images/citypic.jpg)](http://www.glendalepoa.org/images/citypic.jpg)Last night was the always entertaining [Los Angeles Application Developer Meetup](http://web.meetup.com/34/). L.A. is not known for the same massive quantity of developers as the bay area, for example, but having joined forces with the [LA Ruby on Rails Meetup](http://ruby.meetup.com/84/) crew some time back, the monthly event is still growing.  
  
This month's was held at the impressive new digs of [YellowPages.com](http://www.yellowpages.com/), who have been busy building out a huge Ruby on Rails based local search replacement for their venerable 100K+ lines of Java code. Thanks for the great sandwiches, boys... next time, buy beer!  
  
Anyhow, four presentations took place on various fun topics of technical interest. First, [Jeff Yamada](http://blog.jeffyamada.com/) and his associate (sorry I didn't catch your name) showed [AIR](http://labs.adobe.com/technologies/air/). I then did a short presentation on [Continuous Integration](http://martinfowler.com/articles/continuousIntegration.html) and [CruiseControl.rb](http://cruisecontrolrb.thoughtworks.com/). [Olmo Maldonado](http://olmo-maldonado.com/) talked about his impressive JavaScript library [MooTools](http://mootools.net/), and then [Ari Lerner](http://xnot.org/) showed his just-relased Ruby web development framework, [Sinatra](http://www.xnot.org/sinatra/).  
  
**AIR**  
Long, long ago, I used to work with Flash and ActionScript. Most of us more "serious" programmers were always very frustrated with the language, the programming environment, pretty much everything except for the final product. Since then Adobe has introduced technologies like Flex and AIR to try to address the shortcomings of using Flash as a "real" development tool. Yamada and friend are the authors of the upcoming book "AIR Bible". AIR nee Apollo is designed to provide a way to create native OS applications, while using the toolset that Flash/Flex developers are used to. If you are into Flash/Flex already, then this is probably great for you, but I am not overly in love with so many angle brackets mixed in my code... let's just say that "it ain't Ruby". One small thing I will suggest to the boys: please try to find some relevant application to show for a demo a of a new technology. Between this, and what all of the Microsofties were show a few months back for Silverlight, no one is going to take this new desktop app paradigm seriously!  
  
**How To Get Your Code Together and Keep It That Way**  
Then I did a presentation myself, called "How To Get Your Code Together and Keep It That Way". It was really an exhortation to use the best practice of Continuous Integration, while showing how easy it is to get started with the ultra-cool CI tool CruiseControl.rb. If you are a Rails dev, and you are not using CruiseControl.rb yet, you should be. If you have a development project with greater than zero developers, it is worth it to setup a CI system, even just to keep yourself in check. You can get a [copy of my presentation here](http://files.meetup.com/432104/KeepingItAllTogether.ppt). But don't just believe me, it is in [yesterday's O'Reilly Radar](http://radar.oreilly.com/archives/2007/10/operations-advantage.html) too.  
  
As I was demoing the CC.rb project page, where they are doing CI builds of both CruiseControl.rb itself and the Ruby on Rails project, I noticed that the Rails build has had failing unit tests since Oct. 3. What is up with that? Let's get on it boys!  
  
**MooTools**  
Next up was Olmo Maldonado, once of the authors of MooTools. MooTools is a JavaScript framework for web development along the lines of Prototype or jQuery. I had been hearing about MooTools, but hadn't really checked it out. Naturally, since both of those other JS frameworks already exist, and with Prototype really having dominated in the acceptance wars, MooTools does have a different approach on several levels to justify its existence.  
  
Heavily optimized for speed, according to Maldonado, Moo performs much faster than either Prototype or jQuery on the slickspeed benchmark test at performing DOM selects, which is the core convenience provided by any JS framework.  
  
Another difference is that MooTools libs are completely orthogonal. As such, the developer only needs to incorporate the specific libs that contain the functionality that is required for that application, unlike both Prototype and jQuery which require downloading the entire framework to use any part of it.  
  
MooTools seems to have a more serious emphasis on good software devlopment practices than the othe JS framework projects. One example of this is that MooTools was developed using JSSpec, which is a Behavior Driven Development framework for JavaScript.  
  
Already up to version 1.2, MooTools has been adopted in some very interesting places. The three demos that Maldonado showed were the iPhone version of the Pop-Cap game [Bejeweled](http://static.popcap.com/iphone/), the [Ubuntu.com](http://www.ubuntu.com/) website, and then most curious of all, the [Microsoft Expression](http://www.microsoft.com/expression/) website! What, M$ couldn't use Silverlight? Oh yeah, everyone already has Javascript... no additional download required. Whatever happened to that famous dogfooding?  
  
MooTools is realy designed for the developer who wants to work in pure JavaScript. Most Rails devs like to use the Ruby on Rails Prototype helpers to do nice AJAX-y things like edit in-place and auto-complete functionality. MooTools does all that, plus has a bunch of UI gadgetry too, but having no inline functions, is not really compatible with the way the Rails helpers work. Perhaps someone will create a Rails plug-in that can collect up all of the MooTools Javascript, kida like what the Unobtrusive Javascript plugin does... for those Rails people who want to take advanatge of the DSL-like syntax, instead of dropping all the way into JavaScript.  
  
**Sinatra**  
Speaking of DSLs, the final presentation of the evening was by Ari Lerner, showing his incredibly cool new little Ruby web framework called Sinatra. In fact, I was so impressed by Sinatra, that I decided to give it its own posting. I suggest you go [check it out](http://deadprogrammersociety.blogspot.com/2007/10/sinatra-ruby-web-framework-and-why-it.html) right now!