---
title: 'The Ruby.NET Interview From Down Under'
date: 2007-03-26T15:49:00.000-07:00
draft: false
url: /2007/03/rubynet-interview-from-down-under.html
tags: 
- ruby.net
- ruby
- jruby
---

An [interview with Dr. Wayne Kelly](http://channel9.msdn.com/showpost.aspx?postid=295197) has been put up on [Channel 9](http://channel9.msdn.com), Microsoft's video interview site. Dr. Kelly is head of the Ruby.NET compiler project at the [Queensland University of Technology in Australia](http://www.qut.edu.au/). As always, I am eager to see progress on the .NET side of the [Ruby language wars](http://deadprogrammersociety.blogspot.com/2007/03/jruby-has-won-rails-race-vs-net.html). I drank my coffee, and put on my phones for the 15 minute interview.  
  
After watching the video, I must say I am a little underwhelmed. Not to disparage the fine work of the good doctor on this worthy project, far from it. But I was not impressed by his comments about his lack of familiarity with the Ruby language itself. "If I was going to do any real Ruby programming, I would have to have the pickaxe book at my side to help me with the syntax, " says Dr. Kelly midway thru the interview.  
  
Compare that to a zealous Ruby language fan like [Ola Bini](http://ola-bini.blogspot.com/search/label/ruby) with the JRuby team. And I say this as a long time detractor of Java! How DARE they flaunt their superiority.  
  
There were a couple of interesting points, one of which was the trouble with implementing the Ruby.NET compiler by directly matching Ruby language methods to CLR methods. The collection of CLR methods for an assembly being set at compile time, vs. Ruby class and instance methods which are a very fluid and wonderful thing and can be created at any time.  
  
It was also curious that he said they are not using any of the .NET techniques being pioneered by the IronPython team, like use of dynamic delegates and Lightweight Code Generation. I was really expecting that they would be. At least I would be, if I were them.  
  
Dr. Kelly was apologetic over his team's missing their self-imposed monthly delivery of updated code. He was so understated, that by the end of the interview I got the feeling that "under promise and over deliver" wasn't just cliche, but it was this guy's personal mantra. I hope I got the correct impression.  
  
Let's see some bits, boys! Keep those updates coming...the race isn't over yet.