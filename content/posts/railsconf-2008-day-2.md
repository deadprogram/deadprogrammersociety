---
title: 'RailsConf 2008 - Day 2'
date: 2008-06-08T21:14:00.000-07:00
draft: false
url: /2008/06/railsconf-2008-day-2.html
tags: 
- railsconf
- railsconf 2008
- railsconf2008
---

[![](http://3.bp.blogspot.com/_SgxaAaUGqzY/SEzEQxsxKAI/AAAAAAAABMw/F65ZTrMgTb0/s200/05-31-08_0744.jpg)](http://3.bp.blogspot.com/_SgxaAaUGqzY/SEzEQxsxKAI/AAAAAAAABMw/F65ZTrMgTb0/s1600-h/05-31-08_0744.jpg)Day 2 of RailsConf 2008 began with a keynote from [Jeremy Kemper](http://bitsweat.net/), uber-committer and now main man behind Ruby on Rails. According to the brief introduction by DHH, Jeremy did around one third of the Rails 1.0 release himself, cares deeply about the "whole thing", and has been busy helping get RoR running on Ruby 1.9 and other platforms.  
  
That must explain why Jeremy kept yawning incessantly during his presentation... he is the reason DHH is able to get more sleep! There was some speculation that Jeremy was actually suffering from a hangover... I have no idea, I was asleep the night before.  
  
Anyhow, Jeremy gave an overview of going from Rails 1.0 to the new 2.1 release. Basically, in his opinion 1.2 was "out for a while and got stale". In 2.0, we got all these foxy and sexy things, plus shed a lot of fat and gained speed. But the real story was the growth of the movement behind Rails from a fairly small group of core people, to a massive community of interested contributors. Here are some amazing stats:  
  
From the 2.0 release in Dec 2007 to the 2.1 release in June 2008  
  
\> 1400 contributors (Trac, Lighthouse, and Github users combined... obviously a bunch are duplicates, but even 450+ is a large number!)  
\> 1600 patches  
\> 9000 comments  
  
I cannot imagine the chaos of having THAT MANY people harassing me over getting their pet patches into the Rails trunk. No wonder they seem a little preoccupied... they are actually thinking about how many patches that will have to reviewed by later tonight! Much respect to the team just for dealing with that many crazed developers. This is to a large extent the key benefit of moving [RoR on to Github](http://github.com/rails/rails/tree/master): the much easier process of managing all these people's contributions.  
  
Here are a few brief highlights of the new 2.1 features:  
  
\* New merged migrations - helps deal with keeping migrations synched throughout the development team. It does this by a new naming system, and now making sure that all unapplied migrations have been handled, instead of the old simple schema\_info table, RoR now keeps track of all migrations, and makes sure that all migrations have been applied  
  
\* Time zone support - there were several plugins for time zone support. RoR has now included a fairly simple way of handling this with some baked in logic that extends both the Time class as well as some new ActiveSupport hotness.  
  
\* Ruby gem dependencies - now you can specify exactly which gems and versions are needed for your Rails app, instead of playing "one of these gems is not like the others" when trying to install or deploy a Rails app.  
  
\* Memcache - support for the ultra powerful memcache is now baked in, making fragment caching work nicely... made memcache a first class member of framework, and the memcache client is now bundled with the code distribution.  
  
\* ActiveRecord Dirty - now a way of track what has changed in a AR instance. This improves performance slightly by eliminating unnecessary database writes, but even more importantly results in much cleaner log files.  
  
\* Smarter :include - avoids combinatorial explosion with out of control includes, that result in too many left outer joins on every DB access. Instead, will just perform two queries to DB, with resulting database performance improvements. For example:  
```
  
Msg.find(:all, :include => :user) # two queries  
Msg.find(:all, :include => :user, :order\_by => 'users.created\_at) # uses outer join  

```  
  
\* Named scopes - with complex models, you will have repeated convenience associations. For example:  
```
  
user.recent\_messages  

```  
You would prefer:  
```
  
user.messages.recent  

```  
especially if you can pick it up "for free". Here is a tiny example:  
```
  
class User  
 has\_many :messages  
 ...  
end  
  
class Messages  
 named\_scope :recent, :order => 'created\_by DESC'  
 ...http://www2.blogger.com/img/gl.link.gif[](http://www.ironruby.net/)  
end  

```  
  
**An Embarrassment Of Riches In Ruby VM-land**  
Rails is now running in (milestone achieved just before the conference, thanks to heroic efforts by [John Lam](http://www.iunknown.com/), and the rest of what is a very under-appreciated team within the Ruby community at-large). Rails has been running in [JRuby](http://jruby.codehaus.org/) for months. Also, RoR has been running in [Rubinius](http://rubini.us/) since about two weeks before RailsConf.  
  
And adding to the fun, [Ruby 1.87 is now released](http://www.ruby-lang.org/en/), which includes a bunch of performance related backports from the once and future Ruby 1.9 release.  
  
Just to show all of this multi-platform hotness, Jeremy did a little Rails 2.1 demo, showing the a minimal Rails app running on JRuby, Rubinius, and Ruby 1.9. That was amazing really, that we are actually here. Sure, Rubinius was kinda slow at starting up, but it _worked_, that is what counts.  
  
**Ruby 1.9 on Rails**  
Yes, you can actually run Rails on Ruby 1.9, at least somewhat. ruby-1.9 script/server  
  
In Ruby 1.9, string encoding is huge change. According to Jeremy, 1.9 looks really fast... despite no formal benchmarks. He sees modest performance improvements on typical pages, and really notices it on bigger ERB pages. The typical page is about 20% faster. He says all rails tests are running on ruby 1.9.  
  
Despite all of the yawning, I was not put to sleep at all by seeing some cool new Rails features, and even more importantly a few huge milestones in the Ruby VM race.  
  
**"Getting Git" - Scott Chacon**  
The keynote was good, but it had only whetted my appetite for even more substance. After a tip from a friend, I went to check out [Scott Chacon](http://jointheconversation.org/)'s presentation on git. If you knew nothing about git, this was not the place for you. Scott really got into the internals of git, which many of us found captivating.  
  
The room was pretty packed, and the crowd was held in rapt attention. Several of us remarked afterwards that it was the most organized presentation we had ever seen. It somewhat mimicked the format used during [Dick Hardt's presentation on "Identity 2.0" at OSCON 2005](http://identity20.com/media/OSCON2005/), if you have seen that one. Each section of the presentation was precisely timed, and amount of material covered was massive. I took copious notes, but there was no way to try to capture that much info. Check it out online [here](http://www.gitcasts.com/git-talk), if you want to dive deeply into the glory that is git.  
  
  
**"Advanced RESTful Rails" - Ben Scofield**  
  
Next, I went to [Ben Scofield](http://www.culann.com/)'s presentation on REST. Surprisingly a lot of people are not yet using REST. Or if they are, there appears to be some confusion over exactly how to implement things correctly. It was a decent presentation, but "Intermediate" would have been slightly more accurate. I mean, where was the discussion about polymorphic RESTful controllers? Now THAT would have been advanced.  
  
It was still a good, if not great presentation. Ben knows what he is talking about, I would just suggest raising the bar as far as use of the word "advanced". That suggestion applies across the board to all RailsConf presentations.  
  
**"StoryRunner" - David Chemlisky**  
  
[David Chelimsky](http://blog.davidchelimsky.net/) is the closest thing we have to a test guru in the Ruby community. Here I am using the word guru in a precise way, "any person who counsels or advises; mentor". No single person has had as much impact on introducing best test practices like behavior-driven development to the Ruby community. Even the way that plain old test-driven development is done, is heavily influenced by [RSpec](http://rspec.info/). Not to mention the clones like [Test::Spec](http://rubyforge.org/projects/test-spec/) and [shoulda](http://www.thoughtbot.com/projects/shoulda). All of the cooler projects I work on have test specs, and not just unit tests. The projects that I work on that are not as precisely thought out, turn out to not have test specs, but only unit tests.  
  
Coincidence? I think not. The reason for going through the process of really defining what is to be done is to provide a common understanding between the people in the project. But if that was the whole story, BDUF might work. The problem is you need to apply test-driven development principals _to the specifications themselves_ in your project, not just the code. And you need to be doing this as the project goes on, not just once in the beginning.  
  
Behavior-driven development is about closing the gap between the "customer" (the system/site/application user, if you work in something other than a consulting firm) and the "developer" (that would be you). And that is where StoryRunner comes in.  
  
StoryRunner makes it easy to create a kind of simple parser for a very english language oriented, simple text based way to write specs, requiring far less structure that the current RSpec format. It is really like a DSL that customers can use themselves to define their needs. As David put it, "Ruby code is very readable, but you will not be getting customers to send you emails with new requirements in the form of Ruby code."  
  
So BDD is about helping the customer/user formalize their thoughts about exactly what solution they need. Can you imaging a future, where an initial RFP is put out in the form of test specs? That might provide a lot better basis for estimating, than the pages and pages of static docs that seem to still be getting cranked out inside large development organizations.  
  
Have the requirements been changing? Just do a diff on the specs. There are so many advantages to this approach, that once you get the customer "spec-obsessed", just like developers who become "test-obsessed" the game is totally changed. You can't go back, at least willingly.  
  
David talked about a couple of other tools that fit nicely in the RSpec stack. One very cool way to use it for full-stack integration testing is using [Webrat](http://github.com/brynary/webrat/tree/master). Another is doing true browser testing using [Selenium-RC](http://selenium-rc.openqa.org/). David showed a demo of this, and remarked on how happy it made customers to be able to actually see their web site being tested, not just get the results back.  
  
Note that RSpec is for use with Ruby, not just Rails, so if you are using Merb or Sinatra, or whatever, you can still write test specs using RSpec and StoryRunner.  
  
[![](http://3.bp.blogspot.com/_SgxaAaUGqzY/SEzEc9zpt7I/AAAAAAAABM4/YAJ7D0J1yiE/s200/05-31-08_1855.jpg)](http://3.bp.blogspot.com/_SgxaAaUGqzY/SEzEc9zpt7I/AAAAAAAABM4/YAJ7D0J1yiE/s1600-h/05-31-08_1855.jpg)**Keynote - Kent Beck**  
During Chad Fowler's introduction, Chad said he was "like one of the superdelegates, getting to cast his vote about what we would get for presentations regardless of what we thought we wanted." All I can say is, Chad, keep it up. Some of these people might not get it, but if they continue to stay in this game long enough, they will.  
  
At last, the moment I had been waiting for, and the biggest attraction for me personally in the RailsConf 2008 schedule: [Kent Beck](http://en.wikipedia.org/wiki/Kent_Beck), one of the extremes, the Saturday night keynote.  
  
Kent's presentation on the surface appeared highly informal, just a bunch of stories. It actually consisted of a serious of overlapping arcs on three topics that he knows a little about, because he helped create them: test-driven development, design patterns, and Extreme Programming. These stories took place over a 20 year timeline, stretching back to the origins of the work that the whole Rails community indirectly rides on today. This was before a bunch of RailsConf attendees were born, or at best were still in diapers.  
  
I was pretty immersed in Kent's storytelling. I was too young to have been part of that original movement, but I'm old enough to want to learn all I can from the great masters, before they are all retired or just inaccessible. Amazing to have access to a couple of the extremes, like Ward Cunningham who was just hanging out on Day 1, at a fairly small conference like RailsConf, where most of the people do not even know who they are. For me, it is like a dream come true. If a bunch of other people are passing up the equivalent of intellectual caviar to stuff themselves with potato chips, well, good for them.  
  
Enough ranting, back to Kent's ["Tales to His Grandson"](http://www.amazon.com/Beelzebubs-Tales-His-Grandson-Everything/dp/0140194738). The unifying theme that emerged to me was that Kent is a true 60's radical who chose software as his weapon of choice to use in order to achieve social change. Like many great thinkers, Kent is a reader of books. Yes, those old things. Here are a few that he specifically mentioned that were instrumental in the development of his philosophies:  
  
[Christopher Alexander - "The Timeless Way Of Building"](http://www.amazon.com/Timeless-Way-Building-Christopher-Alexander/dp/0195024028)  
  
[Robert Mankoff - "The Naked Cartoonist: A New Way to Enhance Your Creativity"](http://www.amazon.com/Naked-Cartoonist-Enhance-Your-Creativity/dp/1579122361)  
  
[Dr. Frank Luntz - "WORDS THAT WORK: IT'S NOT WHAT YOU SAY, IT'S WHAT PEOPLE HEAR"](http://www.amazon.com/WORDS-THAT-WORK-WHAT-PEOPLE/dp/1401302599)  
  
The last question in the Q&A was really telling. When asked "do you think that you accomplished the political changes you set out to?" he responded that "No, he had not. And that he really did not fully understand why". Oh, those idealistic baby boomers! Kent, you may not have achieved all you set out to do directly, but the forces you set in motion are still going. Even though many of the attendees at RailsConf do not know you, they have grown up in a world where they expect more freedom and openness, and that is in part thanks to you, and fighting the good fight back then. Thanks, Kent, for staying true to the movement.  
  
**RailsConf - The Jam Session**  
After that very high level of intellectual brilliance, what could possibly top it off? How about a fantastic musical jam session. Chad had arranged the Musical BoF, and somehow [Jim Weirich](http://onestepback.org/) had talked a [very generous and cool local music store](http://www.artichokemusic.com) into loaning him a perfectly playable acoustic guitar. Chad had his ukulele, [Andrea Wright](http://www.chariotsolutions.com/) a recorder, and [Dan Tripp](http://blog.almostaspacegame.com/), a portable folding guitar. I had brought a couple of my harmonicas with me, though not enough, of course. There were a bunch of other fun musical things, like a flute, and an impromptu Brazilian song or two from actual Brazilians. Not to mention a very creative approach toward an impromptu percussion setup by [Forrest Chang](http://funkworks.blogspot.com/).  
  
Anyhow, great fun was had by all! We are already planning the RubyConf 2008 Jam, so it you will be coming, bring your ax! I will commit right now to the Dead Programmer Society helping sponsor having some instruments and/or PA system... plus some beer!  
  
As I headed back to my room, I felt the smug contentment that comes from having had a really good time. Thanks everyone, for having made RailsConf 2008 "worth it" by the end of Day 2. Day 3 was still coming, and would have a few surprises of its own...