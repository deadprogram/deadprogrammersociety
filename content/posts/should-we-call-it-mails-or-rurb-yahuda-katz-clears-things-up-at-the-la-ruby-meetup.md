---
title: 'Should We Call It Mails, or Rurb? Yahuda Katz Clears Things Up At The LA Ruby Meetup'
date: 2009-02-20T00:08:00.000-08:00
draft: false
url: /2009/02/should-we-call-it-mails-or-rurb-yahuda.html
tags: 
- merb
- ruby
- los angeles
- ruby on rails
---

[![](http://4.bp.blogspot.com/_SgxaAaUGqzY/SZ5tt3Pc-bI/AAAAAAAABtU/IEk4Aou8KBg/s200/IMG_0619.JPG)](http://4.bp.blogspot.com/_SgxaAaUGqzY/SZ5tt3Pc-bI/AAAAAAAABtU/IEk4Aou8KBg/s1600-h/IMG_0619.JPG)We just had a fun time at the latest LA Ruby Meetup, once again at UCLA. This time, we had presentations by [James Foster](http://programminggems.wordpress.com/) from [Gemstone](http://www.gemstone.com), and [Yehuda Katz](http://yehudakatz.com/) from [Engine Yard](http://www.engineyard.com/).  
  
James Foster was showing [MagLev](http://maglev.gemstone.com/), which is a Ruby VM based on top of the Gemstone Smalltalk VM. Not much to see here, just some Ruby code benchmarks running at about 4-5X faster than Ruby 1.8.6. That is, of course, not a very fair comparison, but no question that this is another Ruby VM to watch. His talk ended with the ever popular demo showing how [Seaside](http://www.seaside.st/) does continuations, plus running the Smalltalk class browser right in the web browser and editing some code. Yes, this does kick serious butt, but it would be nice to see something new from the SmallTalk universe. I've seen all this from them two years ago, thanks to [Avi Bryant](http://www.avibryant.com/).  
  
The second presentation was where things got a lot more interesting. Yehuda Katz is well known to hard-core developers, thanks to his work on [jQuery](http://jquery.com/) and [Merb](http://merbivore.com/). He has also been very vocal about his differences of philosophy with the Rails way of doing things. Given the fairly recent announcement of the Merb project merging with the [Ruby on Rails](http://rubyonrails.org/) project, we all wanted to know, like, what's up?  
  
As explanation, Yehuda gave a really complete history of Ruby on Rails. He showed slides of DHH's first Mac, he had dates and times of the first SVN commits for Rails. He explained the back story of what was going on in DHH's life while he was creating the first version of Rails. This was all ostensibly to justify that Ruby on Rails and Merb started with the same sort of motivations.  
  
OK, great. That was fun. But what about the real dirt? He did not say anything directly, but my take on it was: when you really look at it, Merb was already turning into Rails++ so why not just merge all that effort into Rails itself? Putting too much emphasis into a separate framework also did not help sell services to the million Rails users out there, which is what Engine Yard's investors need them to be doing.  
  
Yehuda was obviously comfortable with it, even thou he quipped about how many times he said "No!" when first presented with the concept of the great merge. But Merb seems to have the implementation, and Rails the sugar, plus the momentum, so [your peanut butter is now in my chocolate](http://www.youtube.com/watch?v=93hxKtd4CdA). And the big winner? Has to be [Rack](http://rack.rubyforge.org/), or the "Unix of web servers" as Yehuda called it.  
  
Personally, I think it sounds great. Adding some API rigor to Rails will make it a lot more stable of platform for long-term development. And let us not forget that [ezmobius](http://brainspl.at/) has been contributing performance improvements back into Rails for a long time, so nothing shocking there. Just more good stuff for the Ruby web development community.