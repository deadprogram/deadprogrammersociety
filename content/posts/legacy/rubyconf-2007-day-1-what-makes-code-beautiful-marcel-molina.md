---
title: 'RubyConf 2007 - Day 1 - "What Makes Code Beautiful" - Marcel Molina'
date: 2007-11-05T00:19:00.000-08:00
draft: false
url: /2007/11/rubyconf-2007-day-1-what-makes-code.html
tags: 
- good code
- rubyconf 2007
- programming languages
- ruby
- rubyconf2007
---

[![](http://faculty.frostburg.edu/phil/forum/Plato-3.jpg)](http://faculty.frostburg.edu/phil/forum/Plato-3.jpg)I remember Marcel Molina from the first RailsConf, when the Rails core team was introduced to the audience. What had impressed me at the time, besides his cool glasses, was the fact that Marcel comes from a literature background.  
  
That makes his take on programming in Ruby very interesting, because he approaches it from an aesthetic perspective, not just a functional one. To Marcel, code must achieve both, for it to be considered beautiful.  
  
**What Is Beautiful?**  
Here are some historical definitions of beauty:  
Plato - "The ability to grasp mere appearances cannot lead to adequate understanding. At its worst, the appreciation of beauty can mire us in the world of sense experience... but at its best it can lead to the understanding of goodness."  
Rousseau - "I have always believed that good is none other than Beauty in action, that the one is inextricably bound up with the other and that both have a common source..."  
  
There is something deeper than appearances that makes something beautiful.  
  
Looking at human language, meaning is often implicit in sentences. Normally in software, using rhetorical effects is considered bad, unlike literature.  
  
Ruby had an appeal to Marcel as a language, as a visceral response to the language itself. But why? Elegance and beauty are used to describe Ruby code, but what does that mean?  
  
**Settle On A Working Definition**  
Marcel goes with Thomas Aquinas for a working definition of beauty requiring three qualities:  
Proportion - Economy of size & ratio of parts  
Integrity - a glass hammer may look good, but it doesn't work for a hammer - to have integrity, a thing must fit its intended purpose  
Clarity - something should be simple and clear. There is a big difference between sophistication and complication  
  
**Apply definition of beauty to software**  
Marcel provided a contrived example, a case study that created a Coercion class to "help" when parsing XML. In his example, he starts with a 25 line class with three methods and such obfuscated code that even the author admitted that he does not understand it. He then proceeds to show how it can be reduced to 12 lines of reasonably clear syntax.  
  
To achieve beauty, we need checks and balances between each of the qualities of beauty - each is necessary, but none are sufficient themselves alone.  
  
**Does code quality relate to beauty?**  
Marcel cites Kent Beck's "Smalltalk - Best Practice Patterns" as a strong influence. The book is full of pearls of wisdom like "most good Smalltalk methods fit into a few lines". After reading the book, Marcel realized that it was a set of descriptions of the elements that make Smalltalk code beautiful.  
  
**How Is This Useful?**  
We may not be very impressed by the beauty in a case statement. But imagine programming before the 'if' statement. 'If' is way better than assembly code... there is a relativity to what makes code beautiful. Today, Ruby is considered beautiful. In the future, we may consider it as ugly as 70's assembly code based on the aesthetics available to us.  
  
"An expert is someone who has made all the mistakes that can be made in a very narrow field" - Neils Bohr  
  
Ruby is optimized for beauty.  
\- try to imagine better modes of expression  
\- violations of beauty rules reveal mistakes  
\- do enough of this and you will innovate