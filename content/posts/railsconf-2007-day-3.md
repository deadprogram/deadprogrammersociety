---
title: 'RailsConf 2007 - Day 3'
date: 2007-05-23T07:02:00.001-07:00
draft: false
url: /2007/05/railsconf-2007-day-3.html
tags: 
- railsconf
- railsconf2007
---

[![](http://farm.tucows.com/images/2006/07/dave_thomas_at_railsconf.jpg)](http://farm.tucows.com/images/2006/07/dave_thomas_at_railsconf.jpg)By the time we got to RailsConf Day 3, only the most hard core remained. In other words, almost everyone. And we were glad to have stuck around, because some of the best content of the entire conference was yet to come. David Black, introduced two integral members of the Ruby on Rails team, Jamis Buck and Michael "Koz" Koziarski, the co-authors of the seminal "Rails Way" blog.  
  
**The Rails Way**  
Jamis and Koz and both written and read a lot of Ruby on Rails code. The Rails Way is not just what could be done, but what should be; the best way to build a Rails application. Their knowledge of best practices is second to no one, and they shared a whole bunch of great information. I can't really do their tag team code review justice, but here are the highlights:  
  
  
Fat controller is anti-pattern  
\*hard to test  
\*break apart into a model object  
  
A model is anything that encapsulates data and logic, not just an object that talks to a database.  
\*one benefit of this encapsulation is testing  
\*another advantage is the form\_for handle can easily use a model  
  
When to use with\_scope  
\*move the logic to the parent class, so as to freely get the scoping with no extra work  
\*do not go crazy with DRY  
  
ActiveSupport has helpers to make some code self-documenting for dates/times  
  
Asociations  
\*People make associations, but then fail to use them throughout the rest of the application  
\*this helps keep code from breaking in the case where database keys change, for example  
  
Cargo culting  
\*He hates !! (not-not) idiom.  
\*Ternary operator...likes it sometimes  
\*Explain exactly why you need boolean returned, again?  
  
Model helpers  
\*use associations in views instead of instance variables  
  
Routing  
\*simplifying non restful routes - map.with\_options  
  
Override to\_param to make nice looking URL  
  
Returning method  
```
  
 returning new do |booking|  
  booking.some\_thing  
  booking.some\_other\_thing  
 end  

```  
  
The session was really great. Pretty much everyone in the room, no matter how advanced their level, got something good out of it. We could have stayed there all day, with different people bringing up pieces of code for these guys to refactor. If you can, hire them.  
  
**Javascript - Fu**  
[Dan Webb](http://danwebb.net) is the author of the [LowPro extensions to the Prototype JavaScript library](http://danweb.net/lowpro). He had a really nice tight Takahashi style presentation. He was also extremely funny, and the information incredibly useful. Once again, the last day of RailsConf really had a lot of good stuff!  
  
JavaScript is the language we all love to hate. A peasant language, meaning that "lower-level" programmer have to work on the JavaScript code while "higher-level" ones get to work on the "architecture".  
  
JavaScript - fu is not easy to master. Developers are forced into refuge by using frameworks and libraries.  
  
The Ancient Manuals of JavaScript-Fu  
\* The Tao Of The Event Handler (Events)  
\* Five Method of DOM Fist (DOM)  
\* Lightning Script Style (Optimization)  
\* Iron AJAX Technique (Progressive enhancement)  
  
There are big differences in browser implementation of JavaScript.  
  
Two main techniques: inline vs. scripted event handlers  
  
Inline - applied as soon as browser loads  
  
What happen when more than a little bit of inline code  
  
Scripted event handlers  
\*problem in they attach after the element is loaded  
  
LowPro library is an extension library for Prototype, but Prototype library trunk now has a similar thing.  
  
```
  
// Prototype 1.5+ and LowPro  
Event.onReady(function() {  
  $('item').observe('click', function() {...});  
});  
  
// Prototype trunk  
Event.observe(window, 'DOMContentLoaded', function() {  
  $('item').observe('click', function() {...});  
});  
  
// Basic onload  
Event.observe(window, 'load', function() {  
  $('item').observe('click', function() {...});  
});  

```  
  
  
Attach handler from script to each object you want, in order to stay DRY  
  
Separate your JavaScript out of your pages, just like you separate CSS  
  
Large number of event handlers can choke browser performance  
  
How:  
\* use script based by default  
\* in bug page try event delegation  
\* if all else fails use inline  
  
Event delegation - yahoo tehnique  
\* event bubbling  
  
Better inline handlers  
\*a tag needs an actual HREF  
\*do as little as possible, for example:  
```
  
 return view(this);  
 function delete(elemtn)  
 {  
  new Ajax.Request(element.href), {  
   method: 'delete'  
  });  
  
  return false ;  
 }  

```  
  
5 methods of DOM fist  
\*3 oficial W3C methods to modify the DOM  
\- appendChild  
\- insertBefore  
\- replaceChild  
\*1 non-standard (from IE)  
\- innerHTML  
  
DOM methods insert with precision - have to create nodes first  
InnerHTML shifts large bulk amounts of HTML, but with little control  
  
Really easy to use innerhtml from Rails with Ajax  
  
The bastard son - unholy marriage of DOM methods and HTML  
```
  
Element.fromHTML = function(html) {  
  var root = document.createElement('div');  
  root.innerHTML = html;  
  return root.firstChild;  
}  
  
var node = Element.fromHTML('<div>');  
element.insertBefore(thing, node);  

```  
  
Lightning Script Style  
\* making things as fast as possible  
\* do not use javascript\_include\_tag :defaults cause it downloads 5 big files  
\* browsers take time both to download AND evaluate a script  
\* the less JS the better  
\* mooeffects smaller than scriptaculous, but less powerful  
\* browsers can only load 2 resource at once  
\* combine js files  
\* Use gzip instead of JS based minification.  
  
Make sure everything is cacheable  
  
Faster loops  
```
  
 for(var i - 0, enemy;  
  enemy = enemies\[i\]; i++) {  
 defend(enemy);  
  }  

```  
  
Be careful with selectors  
$$('.anything'); slower  
$$('span.anything'); slow  
$$('#item .anything'); // css xpath selector  
  
Iron Ajax Technique  
\* rule #1: browsers suck  
\* main browsers are getting better quickly  
\* but what about the others?  
\* Corporate security blocks Javascript at firewall  
\* the traditional rails opin: f\* you!  
\* but why turn away users if you don't have to  
  
Progressive Enhancement  
1\. start with plain HTML  
2\. test if necessary brwt features are there (XMLHTTPreq, canvas, etc)  
3\. If present, then apply xtra JS features  
  
Tt's easy to apply to ajax  
\* HTML  
\* JS  
\* RJS  
  
Try progressinve enhancement first  
  
Lastly, Dan recommended a few books on Javascript he said are better than all the others:  
\* [Professional JavaScript Techniques](http://www.amazon.com/Pro-JavaScript-Techniques-John-Resig/dp/1590597273)  
\* [Bulletproof Ajax](http://www.amazon.com/Bulletproof-Ajax-Voices-That-Matter/dp/0321472667)  
\* [DTHML Utopia: Modern Web Design Using Javascript and DOM](http://www.amazon.com/DHTML-Utopia-Modern-Design-JavaScript/dp/0957921896)  
  
Dan's session was full of good stuff. Even the people who thought they knew it all were scribbling down a couple things before the end. And thank you, Dan, for making it really fun as well as informative.  
  
**Dave Thomas**  
Dave's speech was unconventional, in that he doesn't say what people expect him to. I consider that a good thing. Many people in the crowd were perplexed for long moments as he spoke. For those people who need a simple explanation of Dave's speech, the two recurring themes for RailsConf were "give", and "don't get stuck".  
  
"Just to set the record straight, the first RubyConf was 3 people and a dog, and the speaking was in between sips of beer"  
  
Orthodoxy - do what is expected  
Orthopraxy - do the "right thing"  
  
It's called Object oriented programming, not class oriented programming. Challenge: write next next program with objects instead of classes  
  
What Are Your Cargo Cults?  
  
Dave is a real thinker, and I hope that our community can rise to the challenge and keep progressing. Embrace Orthopraxy!