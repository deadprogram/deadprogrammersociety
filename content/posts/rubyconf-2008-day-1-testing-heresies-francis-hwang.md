---
title: 'RubyConf 2008 - Day 1 - Testing Heresies - Francis Hwang'
date: 2008-11-13T09:07:00.000-08:00
draft: false
url: /2008/11/rubyconf-2008-day-1-testing-heresies.html
tags: 
- rubyconf2008
- ruby
- rubyconf 2008
- test-driven development
---

[![](http://media-2.web.britannica.com/eb-media/10/18910-004-7F8BCBE7.jpg)](http://media-2.web.britannica.com/eb-media/10/18910-004-7F8BCBE7.jpg)The sessions for RubyConf 2008 day one were nearly over, when I attending this highly entertaining and informative one. I had missed the chance to see a previous presentation by [Francis Hwang](http://fhwang.net/), and being as test-obsessed as I am, I was not going to make the same mistake twice.  
  
Many people are confused over mocks, stubs, and other fakes. Here are the real definitions.  
  
[Gerard Meszaros](http://xunitpatterns.com/) - Test Doubles  
\- dummies - passed around but never used  
\- fakes - work but unstable in production  
\- stubs - provide canned answers to calls made during test  
\- mocks - mostly concerned with surface interaction  
  
Classical TDD use real objects.  
Mockist TDD will always use a mock for any object with interesting behavior  
  
Problem #1 with mocks  
Cannot figure out problem and solution at same time  
  
Problem #2 with mocks  
Bugs can slip between layers  
  
Francis Hwang, TDD Clasiscist  
\- test setup creates records in the db  
\- no sqlite in test  
\- when you use test doubles, it's always a big deal  
  
Real world example #1  
Ensure that an optimization is actually being used  
Redefine the actual surface interaction to 'scream' on error  
  
Real world example #2  
Faking a real web service (not written by us)  
Best to use stub, to duplicate functionality  
Need test, stub, AND test for stub  
  
Dogma - if you tests do not run quickly, there's something wrong with you  
Heresy - I'd like my test to run 30 sec. I'd also like a pony  
  
Francis does not use autotest, because he does not want to run all of the tests every time he changes something. [Eric Hodel](http://blog.segment7.net/) chimed in from the audience says that it can run only what changed. Only if it passes, will it run ALL tests. Me, I loves my [autotest](http://www.zenspider.com/ZSS/Products/ZenTest/)... with growl notifications, it's all good.  
  
[devver](http://devver.net/)  
They say it is a ec2 based distributed test system...  
  
[testjour](http://github.com/brynary/testjour/tree/master)  
uses bonjour to trigger a farm of machines in your LAN to perform distributed tests  
  
Dogma - you code should always be well-structured  
Heresy - under-structuring can be freeing  
  
Uses example of constantly cleaning small NYC apt. It was living on a boat, where you spent all your time putting things away.  
  
Dogma - Fine grained focus leads to high quality code  
Heresy - Never forget the unknown unknowns  
  
System design 101  
How likely fail  
What will fail look like  
How can I find out quickly  
How can I limit damage  
  
Dogma - testing makes my job easier  
Heresy - testing makes it easier for others to do my job - unless my job keeps growing  
  
Rails has made it so simple to implement simple business logic, so way more is expected now.