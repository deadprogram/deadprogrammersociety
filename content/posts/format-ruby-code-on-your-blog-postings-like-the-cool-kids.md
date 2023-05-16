---
title: 'Format Ruby Code On Your Blog Postings Like The Cool Kids'
date: 2007-02-19T16:41:00.000-08:00
draft: false
url: /2007/02/format-ruby-code-on-your-blog-postings.html
tags: 
- ruby
---

[![](http://www.barronmind.com/attire6.jpg)](http://www.barronmind.com/attire6.jpg)I had noticed that almost [all](http://brainspl.at) [of](http://chadfowler.com/) [the](http://drnicwilliams.com/) [cool](http://errtheblog.com/) [people](http://dablog.rubypal.com/) post nicely formatted, color coded, beautiful looking Ruby code whenever they post.  
  
Well, some of the cool people use a [style of formatting that defies description](http://redhanded.hobix.com/inspect/streamCopyYoutubeRevverEtc.html)...but I digress.  
  
Anyhow, I looked at my poor pitiful postings, and felt like a second, or even third class citizen. Everybody's code is looking better than mine! What can be done?! Extreme makeover, Ruby CSS edition.  
  
Mac developers who are using TextMate already have a built-in way to get back nicely formatted HTML. Does this mean they have built-in coolness? Yes it does. But for others who are using a different OS, or maybe an IDE like RadRails, there is also a solution.  
  
On the Ruby Advent calendar site from last year, is a [cool posting from Peter Cooper](http://www.rubyinside.com/advent2006/7-coloring.html) that allows you to submit some Ruby code thru a web page, and get back formatted HTML. Add a little bit of CSS to your page, and you too can be one of the cool people.  
  
I had to modify the suggested CSS for my ultra-retro TTL terminal look that I usually set my editors up with. So my Ruby code went from this:  
  
```
  
class Animal < DSLThing  
 attr\_accessor :name  
   
 def initialize(name=nil)  
  @name = name  
 end  
end  

```  
  
To this:  
```
class Animal < DSLThing  
 attr\_accessor :name  
   
 def initialize(name\=nil)  
  @name \= name  
 end  
end
```  
  
With my new CSS, I can now hopefully masquerade as one of the cool kids, and maybe even sneak into the club.