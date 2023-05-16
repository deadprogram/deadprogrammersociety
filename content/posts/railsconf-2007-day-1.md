---
title: 'RailsConf 2007 - Day 1'
date: 2007-05-20T18:28:00.000-07:00
draft: false
url: /2007/05/railsconf-2007-day-1.html
tags: 
- ruby
- railsconf2007
- ruby on rails
---

[![](http://4.bp.blogspot.com/_SgxaAaUGqzY/RlGueGCUe-I/AAAAAAAAABA/bnchlQ6YppY/s200/05-18-07_0741.jpg)](http://4.bp.blogspot.com/_SgxaAaUGqzY/RlGueGCUe-I/AAAAAAAAABA/bnchlQ6YppY/s1600-h/05-18-07_0741.jpg)I was primed and ready for RailsConf 2007 Day 1. The excitement was in the air, and the crowd was primed. We awaited a day absolutely packed with mind candy. Starting with [Chad Fowler](http://chadfowler.com/), [David Heinemeier Hansson](http://www.loudthinking.com/), [Robert Martin](http://butunclebob.com/), [Adam Keys](http://mvm.therealadam.com/), [Avi Bryant](http://smallthought.com/avi/), and [Ze Frank](http://www.zefrank.com/). Wow, what a lineup!  
  
As Chad Fowler took the stage, his ukulele in hand, we eagerly awaited his opening remarks. Chad really did a great thing, by not just giving us the "feel-good rah-rah Rails is taking over the world" intro speech that most people probably expected. Instead, he [took a higher path](http://www.chadfowler.com/2007/5/19/changing-the-world). The virtues of sharing are not limited to open source projects, but need to get into the real world. For example, using Rails to create applications that solve real problems that have not been tackled yet, due to the high cost of developing a solution. We as a community can also do a lot for the world outside of just developing software, no matter how cool it is. The Pragmatic Programmer fund-raising drive is a fantastic example of mobilizing the community, and Chad exhorted the crowd to keep those donations coming.  
  
Is the Rails community more concerned with altruism and spirituality than other tech people? Or are we following the once again popular meme of greater social awareness and activism? That may be fodder for another posting some other time...back to the show.  
  
His opening remarks finished, Chad played a little uke ditty, under a delightful beat poetry introduction given by [Rich Kilmer](http://richkilmer.blogs.com/) for David Heinemeier Hansson. As David took the stage, we all wondered, "what would he spring on us this year? We just spent the last year RESTifying our applications, what MORE do you want from us?!"  
  
And here is what he said:  
  
  
**Keynote - David Heinemeier Hansson**  
  
REST is where it is at, and Rails 2.0 doesn't alter that path. But there are 9 other things he really likes about Rails 2.0.  
  
\* Debugging with breakpoints  
David showed the ability to put a breakpoint into your Rails controller that opened irb with all of the context and objects ready to be introspected. Although dropping to command line is not exactly what most of us want out of a debugging session, this could easily have a superior UI put on it.  
  
\* HTTP Performance  
HTTP performance in an area where a couple of small changes can dramatically increase performance. His examples showed very easy combining of all CSS files, and separately all JS files together into a single file, and then compressing of each group of files into a gzip archive for quick download.  
  
Another HTTP performance technique that 2.0 introduces is a way to get around the two connection limit that browsers enforce, by serving static assets from multiple host servers using the new :asset\_hosts configuration option.  
  
\* Query Cache  
Rails 2.0 can look at all of the SQL that ActiveRecord is executing, and if there have not been any inserts or updates, automatically caches that database query.  
  
\* Rendering  
Rendering of a resource request has now been separated from the MIME type of the request. Now, it is much easier to handle multiple format requests like RSS or ATOM that both return XML.  
  
\* Configuration Initializers  
Separates the config.rb into separate files, which reduces the effort and extracts the application unique config info into easier to read chunks.  
  
\* Sexy migrations  
This plug-in, which simplifies the syntax for database migrations, started out as a Rails plug-in, but is so useful that it is now part of Rails core.  
  
\* HTTP Authentication  
DHH didn't feel the pain of not having easy HTTP authentication till he started using his own ActiveResource. Then he realized that although human users with their web browsers might prefer a forms-based authentication, machine users that wabt to call the REST interface for an application would prefer HTTP authentication.  
  
\* MIT License  
Generating a new Rails assumes that you want to use the MIT license. The MIT license being simple and appealing.  
  
\* Spring Cleaning  
Removing things form Rails core, like ActiveWebService, that are not as commonly used by many Rails applications, and turning them into plug-is that can be added separately by applications that require them. In the case of ActiveWebService, DHH also wants to guide users away from SOAP and toward REST, and removing ActiveWebService from Rails core does so in a "subtle" way.  
  
DHH is funny, smart, and yes, opinionated. The Rails community wouldn't have it any other way.  
  
[![](http://3.bp.blogspot.com/_SgxaAaUGqzY/RlGuz2CUe_I/AAAAAAAAABI/k017o814IHI/s200/05-18-07_1144.jpg)](http://3.bp.blogspot.com/_SgxaAaUGqzY/RlGuz2CUe_I/AAAAAAAAABI/k017o814IHI/s1600-h/05-18-07_1144.jpg)**Bob Martin - Writing Clean Code**  
  
Next, I had the extreme pleasure of seeing the great Bob Martin. Getting to be up close and personal to a legend of software, who normally is a keynote speaker at massive conferences like SDWEST, was a special treat. And Bob certainly lived up to expectations. He had incredible energy, was funny, and very insightful. Here are some excerpts from his remarks.  
  
\*Ward Cunningham noticed that "it was too easy to make a mess in Smalltalk".  
\*Have you ever been significantly impeded by bad code?  
\*Why did you write it? - "don't have time to write it correctly"  
\*Due to the quality of the code, we end up with diminishing returns from productivity over time as the code bloats  
\*Only solution to the problem is to clean up your code  
  
\*So what do we do about bad code?  

  
*   grand redesign in the sky, or
  
*   incremental improvement
  

  
  
\* Grand redesign in the sky  

  
*   all requirements are buried in the old system
  
*   most companies will create a tiger team
  
*   tiger team is hated by old team
  
*   both systems are still under development however, so
  
*   it takes years for the old system to be replaced by the new system
  
*   as a result, the new system needs to be redone by the time it replaces the old system
  

  
  
\*Incremental improvement  

  
*   always check in code better than when you checked it out
  
*   never let sun set on bad code
  
*   test first
  
*   provides necessary flexibility
  

  
  
\*Elizabeth Hendrickson had given Uncle Bob a green wristband labeled "test-obsessed". He feels like he cannot take it off. Ever. Because if he does, he is not really committed to testing.  
  
\*How much code coverage should we have? We should attempt to reach 100%, asymptotically.  

  
*   rspec is really good. Use it.  
    
*   Open closed principle is violated by repeating code  
    
*   Modules should open for extension, but closed for modification  
    

  
  
\*What do you do when it gets yucky?  

  
*   Refactor quick when you smell the mess  
    
*   Do not ignore these rules, or you will end up with a festering pile of code!  
    
*   Remember, we cannot write the correct code the 1st time. Trying to is egomaniacal.  
    

  
  
\*Iterate, like your teacher showed you how to write your grade school papers. Start with a rough draft, then refine.  
  
\*One of the best ways to ruin a program is try to make massive changes all at once  
\*Keep it running at all times  
\*You are not allowed to make a change that breaks the system  
  
\*How do you refactor? You need tests!!!  
\*Stick to the principle of least surprise  
\*Make tiny incremental changes, always running tests each time, minute by minute  
\*Notice what happens when you shrink the granularity of your development  
\*Uncle Bob is not sure that designating class methods as private is worth it?  
\*Software design is about separation of concerns - volatile and non-volatile code should be separated  
  
\*What if you make a mess? Was it worth it?  
\*Bad code gets harder to clean - Clean as soon as it gets messy  
\*So what about time to market? Isn't that the most important thing? What is the fastest way to finish dinner? Once you are done eating, just leave everything on the table, get up, and walk away. However, the fastest way to finish dinner is also the slowest way to start dinner, as you will have to clean everything before you can start cooking, and the plates will be hard to clean.  
  
\*Bad code  

  
*   Nothing has worse effect on a project than bad code  
    
*   Schedule slips  
    
*   Requirements missed  
    
*   Team dynamics problems  
    
*   Bad code rots and ferments  
    
*   Becomes a weight that drags team down  
    

  
  
\*Professional behavior  

  
*   Commitment like the "green band"  
    
*   Pros write tests first  
    
*   Pros clean their code  
    
*   Pros know going fast means going well  
    
*   Making the mess is NOT faster  
    

  
  
\*Like DHH said earlier today: "it's about making things a little bit nicer"  
  
  
**Standing On The Shoulders Of Giants**  
  
I was not really familiar with Adam Keys, but on the advice of a friend, I went to his session. Being a bit of a code archeologist myself, I looked forward to hearing Adam's thoughts about reading Ruby code. It was indeed worthwhile attending the session. Here are some notes of his remarks.  
  
\*Rails sucking all of the air in the web space has been a good thing...  
\*You need to listen or perform a composer's music to really know it...likewise we need to read the code to fully understand any piece of software.  
\*Reading code requires 5 times more effort than writing code  
\*We all write legacy code, if you look at a long enough timeframe  
\*Protect yourself from yourself, 5 days ago - going too fast with a pet technique  
  
\*Why reading code could be hard  

  
*   Not a lot of tool support for reading ruby  
    
*   Unfamiliar idioms  
    
*   Code written by non-heros  
    
*   You need a helmet with light on it - concentrate on only one part of code  
    
*   Find the entry points and hooks  
    
*   Don't chase rabbits into holes  
    

  
  
Adam's guide to spelunking the code  

  
*   Look at URL, look at routes  
    
*   Controller  
    
*   Controller filters  
    
*   Controller actions  
    
*   Method called by actions  
    
*   templates and temp. helpers  
    

  
  
Preface to spelunking  

  
*   filters in application controllers or helpers in application helpers  
    
*   model observers, validations  
    
*   code in libs or plugins  
    

  
  
  
**Keynote Introduction**  
After a rather dry and not that well executed speech by Five Runs CEO Steve Smith, [Joey deVilla aka AccordianGuy](http://www.joeydevilla.com/blog) gave a brilliant rendition of Radiohead's "Creep" as "I'm A Noob" an absolutely hillarious ode to DHH.  
  
**Avi Bryant**  
  
Avi Bryant is the creator of [DabbleDB](http://dabbledb.com/) which was built using Smalltalk and the [Seaside](http://www.seaside.st/) framework. As a Smalltalk enthusiast, many people were confused as to why on earth he would be a keynote speaker at a Rails conference. Ah, how we limit ourselves by putting everything into a little conceptual box and leaving it there for the rest of our lives. Getting outside perspective is the only way we ever learn anything and grow.  
  
Avi started out by telling us that "He comes from the future". What he really meant was that Smalltalk has already gone through a similar evolution as Ruby, but that he considers Smalltalk 10-20 years ahead as far as solving certain problems that the Ruby community is still working on.  
  
Avi considers Ruby and Smalltalk really the same language, at the core level. He showed a couple simple examples of their similarities. Then, he explained why he was giving his talk: to help out Smalltalk.  
  
He had a number of other points:  
  
\* Ruby's features make it inherently slow.  
\* Smalltalk was bought, sold, then bought again by Sun. The VM developed for Smalltalk ended up as the Java VM.  
\* No reason Ruby cannot have the same performance characteristics as Smalltalk  
\*Having proper REAL debugging is crucial  
\*Ruby needs better VM tech  
\*What if Ruby's ObjectSpace was:  

  
*   transactional & persistent  
    
*   transparently distributable  
    
*   terabyte scale  
    
*   no restrictions to storage location  
    

  
  
\*GemStone - Portland based VM company, that has a very high performance runtime for Smalltalk. Acording to Avi, GemStone supports over 1000 VM's sharing 100s of GB of object memory. GemStone is free up to 4GB of storage.  
  
\*Objects get better with age  
\*Object lifecycle  
\*create  
\*use  
\*save  
  
During the Q & A at the end, [Ola Bini](http://ola-bini.blogspot.com/) asked Avi about using Rubinous. Rubinious is a runtime for Ruby that is actually written entirely in Ruby itself. I was impressed by the fact that Ola didn't ask what Avi thought about JRuby. Ola is really cool, and his question was right on target after Avi's criticism of Ruby being written in C, and not turtles all the way down. Avi's response included his opinion that the Smalltalk VM is so advanced it would take the Ruby community 10 years to develop, just like it took that long to write the Smalltalk VM.  
  
Personally, I do not buy that argument. Just because it took them 10 years to develop their runtime engine doesn't mean that all such tasks will take the same length of time. But Avi's perspective is a bit more biased than Ola's, I think.  
  
And then came Ze Frank...  
  
  
[![](http://encounters.typepad.com/photos/uncategorized/ze_vertical.jpg)](http://encounters.typepad.com/photos/uncategorized/ze_vertical.jpg)**Ze Frank**  
  
I like Ze's stuff, but I had no idea what we were in for. I knew he was witty and smart, but what I didn't know what that he was a total genius. Ze is to theory of online community what Why The Lucky Stiff is to Ruby. On the surface everything is very amusing, but if you dig in you can go deep. Very deep.  
  
Ze started out with a hilarious bit on "Acceleration Anxiety". He had the crowd laughing so hard that tears were coming out, as he made fun of his own fear of flying, and the idiocy of so many everyday things like the safety instructions and vomit bags on airplanes.  
  
And then, he told us about a second kind of "Acceleration Anxiety". Here are a few of his key points on socialogy and online community:  
  
People are learning a new language (ours)  
  
People are having a media conversation  
  
What can you do with your audience if they do things you don't like  
\*ignore them  
\*control them  
\*shut them down  
  
Facilitating conversation : cultivating the energy  
  
At a really good dinner party, it about the focus of the experience. Most people asked would not remember what had been discussed, but they would have remembered enjoying themselves - all of the different kinds of guests need to engaged.  
  
Ze then shared his history of how he started and become the net culture star that he is today. At first his communications were one-way. But then his audience started becoming participants. He showed us a few examples:  
  
The show  
Earth sandwich  
Human baton  
  
Complexity of narrative has become much more complex  
  
Technology is a facilitator of basic human emotions  
  
The Core Values  
\*Conversation  
\*Community  
\*Belonging  
  
There are one to one online communication. And there is mss online communication. We we need to do is look to the middle.  
  
  
All I can say is wow. During Ze's introduction, Chad Fowler said he didn't realize that Ze was like some kind of Malcolm Gladwell. Neither did I.