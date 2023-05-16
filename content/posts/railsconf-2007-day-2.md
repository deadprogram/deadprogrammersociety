---
title: 'RailsConf 2007 - Day 2'
date: 2007-05-22T10:30:00.000-07:00
draft: false
url: /2007/05/railsconf-2007-day-2.html
tags: 
- rails
- ruby
- railsconf2007
- railsconf on beer
- ruby on rails
- jruby
---

[![](http://1.bp.blogspot.com/_SgxaAaUGqzY/RlMsr2CUfAI/AAAAAAAAABQ/L2YxJRZjAMg/s200/IMGP5364.jpg)](http://1.bp.blogspot.com/_SgxaAaUGqzY/RlMsr2CUfAI/AAAAAAAAABQ/L2YxJRZjAMg/s1600-h/IMGP5364.jpg)After the incredible energy of RailsConf Day 1, Day 2 seemed to slow down the pace a little bit. That was good for me, as I could spend some time catching up with friends both old and new, and not just attending sessions like an information junky. First would come the morning keynote speeches from [Cyndi Mitchell of ThoughtWorks](http://www.thoughtworks.com/mitchell+cyndi.html), and headliner [Tim Bray of Sun Microsystems](http://www.tbray.org/ongoing/), with a short interlude from [Charles Nutter](http://headius.blogspot.com/).  
  
**Cyndi Mitchell - Thoughtworks**  
  
Ms. Mitchell is UK Managing Director of ThoughtWorks. As such, she is a polished corporate representative, which is exactly the kind of emissary that Rails needs in big organizations. She had a few interesting points:  
  
\* 40% of new work at ThoughtWorks is coming from Ruby on Rails in the enterprise  
\* We need to reclaim the word "enterprise" back from meaning "bloated, inefficient, and expensive" to its original meaning of "entrepreneurial"  
\* The "real" enterprises are using Ruby on Rails to get stuff to market quickly  
\* ThoughtWorks is offering a complete Rails production stack called RubyWorks, and is will be providing paid 24/7 support for Rails.  
  
**Tim Bray - Sun Microsystems**  
After Cyndi, the irrepressible Tim Bray took the stage. Despite not really being that much into Java, I have been following Tim's blog for quite some time, as he is a smart thinker with plenty to say to the industry at large.  
  
Tim thinks that the Ruby language is as important as Rails (I agree!!). With JRuby, Sun wants to sell lots of hardware to large enterprises that will be choosing Sun Hardware and Solaris as the preferred platform for their Rails applications. Sun is also doing lots of work on NetBeans to do better Rails development.  
  
Tim then briefly brought up Charles Nutter to give him some Rails street cred...er, I mean to explain why Ruby developers should care about JRuby.  
  
Charles made two main points:  
\* A whole different way to do Ruby dev...using tried and true Java tools that already exist  
\* Move into enterprise where Java is accepted but Rails is still not  
  
Then back to Tim:  
It is not CIO's who lead industry...it is people like us.  
  
How to make money on free products  
\* first you get adoption  
\* then you get deployments  
\* then you can monetize at point of value - no large business will adopt any tech that is not supported  
  
Big companies will either get a handle on web 2.0 or get disintermediated  
  
He assumes Rails will succeed beyond our wildest dreams.  
  
Java, php, and .NET will never go away  
  
The network is the computer...and its a heterogeneous network. And JRuby is how we get everything to talk to each other.  
  
Java really consist of three main parts: language/JVM/Java APIs.  
JRuby lets Rails programmers access the latter two.  
  
How do we get everything to talk to each other? REST  
  
[Etags](http://en.wikipedia.org/wiki/HTTP_ETag) are a way to solve the REST problem with different versions of the same data.  
  
[ATOM](http://en.wikipedia.org/wiki/Atom_(standard)) - Everything should have a publish button: cameras, phones, browsers, etc  
  
Is REST all there is? SOAP... WS-\* 36 specs, ~1000 pages of documentation.  
  
[WSIT](https://wsit.dev.java.net/) - interop with [MS WCF](http://msdn2.microsoft.com/en-us/netframework/aa663324.aspx)  
  
Hot developer issues  
\*static vs dynamic languages  
\*maintenance  
\*tooling  
\*integration  
\*concurrency  
\*time to market  
\*scaling  
\*load balancing  
\*observability  
\*file IO  
\*DBMS  
\*Shared nothing architectures  
\*CPU  
\*concurrency  
\*debugging  
\*unit test  
\*functional programming?  
  
Which matter the most?  
\*Conventional wisdom for each language  
\- Java: performance, tooling  
\- php: web scaling, ease of use  
\- Rails - time to market, maintainability  
\*Tim says: The most important are Time to market, and maintainability  
  
**Extra Action Marching Band**  
After the speeches, I went to a session I didn't find that interesting at all, and so in the interest of not offending anyone else too badly, I shall let it remain anonymous...you know who you were. But near the end, a massive blast of sound came from the entrance to the conference center, and then proceeded past the sessions rooms toward the main hall.  
  
It was the [Extra Action Marching Band](http://www.extra-action.com/), an amazing avant-garde performance troupe. If San Francisco (which is where they are from) had a love-child with New Orleans, it would be something like this band.  
  
Despite an almost-incident with the conference center security staff, they were able to finish their set. The music and performance were quite incredible, showing a high level of musicality as well as serious creativity. The bullhorn with a delay pedal attached was really amazing sounding...I have to make one like that for my harmonica.  
  
After this unique musical interlude, it was back to the conference sessions...thamks to Tim Bray for the photograph.  
  
  
**Xen And The Art of Deployment**  
Ezra Zygmuntowicz of [Engine Yard](http://www.engineyard.com/), [Merb](http://rubyforge.org/projects/merb/), and [BackgrounDRb](http://backgroundrb.rubyforge.org/) fame gave my favorite presentation of the day. The session was packed, with both information and people. If you wanted information about scalability, at least from the perspective of the stack, then this was the high point of the entire conference. Here are copious notes of what he said:  
  
Serving up Rails right now is all about Mongrel  
  
Mongral uses a Ragel state machine for validation  
  
Why is mongrel better:  
\*HTTP is well known protocol  
\*Mongrel easy to setup and use  
\*Transparent wire protocol  
  
Thread safety  
\*Rails not thread safe  
\*1 request at a time per mongrel  
  
New dog, old tricks  
\*Wide # of options to load balance front end  
\*pen, pound, HA-proxy  
\*Lightspeed can serve static files  
\*Apache 2.2/mod\_proxy\_balancer can do same  
  
Each current solution has problems  
  
[Nginx](http://nginx.net/)  
\*serious performance  
\*small resource footprint  
\*no leaks under heavy load  
\*killer rewrite and proxy mods  
\*author is cool and responsive  
\*Nginx + Mongrel  
\*This is THE stack  
\*apache for mod\_dav\_svn  
\*flexible config allows both serving static and dynamic requests  
\*fast!!!  
\*Nginx cannot do upload progress due to buffering  
\*no connection rate limiting for proxy modules yet  
  
The future for nginx  
\*mod\_rewite going away  
\*replace with http\_script\_module  
\*embed NekoVM directly into nginx  
  
Perfect simple stack  
\*Linux  
\*Nginx  
\*Mongrel (mongrel\_cluster)  
\*Monit  
  
[Swiftiply](http://swiftiply.swiftcore.org/index.html) - the cool new solution  
  
Evented Mongrel  
\*hot patch  
\*remove ruby treeads  
\*replace with eventmachine event loop  
\*mongrel single threaded  
\*big IO speed increase  
\*stand up to higher load  
  
How is single threaded faster?  
\*Ruby green threads are slow  
\*mutex locks are expensive  
\*one process can only do so much IO  
\*event driven means running in a tight loop and firing callbacks  
\*without context switching between threads, single process has less overhead  
  
Mongrel vs evented mongrel - performance stats  
\*1 user - 1K more req/sec  
\*100 users - 758 req/sec vs. 3700+  
  
Swiftiply proxy  
\*event drive proxy, small memory footprint  
\*faster than ha-proxy  
  
How is swiftiply different  
\*In a normal proxy, you need to config each back end server in advance before starting proxy  
\*swiftiply is a client/server architecture, where new back end servers register with proxy  
\*keeps persistent connection between proxy and back end servers  
\*auto-configuration of proxy  
  
This means you can start/stop as many mongrels as you want, and they get configured into proxy, opening the door to auto-scaling  
  
The Zen of Xen  
\*monolithic linux VS modular lnux  
\*old model: one box running all services  
\*new: specific virtual machines setup for specific purpose  
  
We all want to modularize application why not modularize servers  
  
What about more than 1 box?  
  
Old school - more boxes  
\*mysql box  
\*another box for other services  
  
New school  
\*add another xen box  
\*pick resource intensive parts, and more to another VM  
\*each VM only runs one thing, but well  
\*target performance problems  
\*scale better  
  
Advanced clustering  
\*boot off dom0 off of USB drives  
\*SAN for all Xen domU  
\*red hat clustering suite for fencing and cluster options  
\*GFS for 100% posix file sys  
\*hardware load balancer, or dedicated box running Ultra Money or LVS  
  
Create a fabric of compute and storage  
\*If a node fails, just swap in another  
\*Move hot VM's to less loaded machines  
\*Deploy app on 1 node, then bounce mongrels with GFS  
\*Fragment and page cache across nodes  
\*Scale from 1 or 2 VMs to as many as traffic requires and then back down again as traffic subsides  
  
RAM RAM RAM  
\*most rails apps are RAM bound before they become CPU bound  
\*Avg mongrel serves 70-120 mMP PER mongrel  
\*RMagick is a typical RAM hog  
\*:include on active record also very bad performance  
\*95% of rails apps will leak memory at point or another  
  
Use Rails plugin leakhouse to find leaks  
  
Rails eats DB resources for breakfast  
  
Most people's production apps hav no database indexes! Learn where and when to apply indexes.  
  
ActiveRecord insulates developers so much to the point of massive inefficiencies.  
  
You will need to denormalize data and use custom SQL statements to get performance  
  
Other Tips  
\*do not use file system sessions  
\*script/runner is inefficient. do not load rails into bgprocesses.  
\*Use raw MySQL and Ruby without Rails if you can  
\*DO NOT use script/runner to pocess incoming email. Run deamon in loop and poll svr with net/pop3 or net/imap  
  
Rails is great for 80/20 rule, but you are on your own for last 20%  
  
Learn how to write custom mongrel handlers  
  
When is optimization NOT premature?  
  
Ruby is plenty fast, its Rails that is on slow side  
  
Cache, cache, cache espcially static HTML files  
  
Do not store full ActiveRecord object in session, just store hash to recreate it  
  
Parting thoughts  
\*do not take anyone's word as gospel  
\*test and benchmark for yourself  
\*trust but verify  
  
**The Rest Of The Day**  
After Ezra'a session he was swarmed like a rock star. I know, cause I was standing nearby having a really nice chat with [Zed Shaw](http://www.zedshaw.com/) the creator of Mongrel and [Evan Phoenix](http://blog.fallingsnow.net/), the creator of the [Rubini.us](http://rubini.us/) Ruby runtime I was mentioning yesterday. You go, Ezra!  
  
Later on, I got to hang out at the Engine Yard booth with Ezra for a few minutes, where Mike Brown and some other brilliant Kiwi whose name I didn't catch were chatting him up. I learned even more about hard-core clustering from listening to those guys go off...all I can say is I'm glad I have hosting at Engine Yard!  
  
I wanted to go to Dr. Nic's [RejectConf](http://drnicwilliams.com/2007/05/10/rejectconf-at-railsconf/), but so many people told me they planned on going that I figured I wouldn't get in. I couldn't take the prospect of being rejected twice at the same conference, so I made other plans which turned out to be really fun.  
  
After dinner with the same group of RailsConf friends from last year, with more delicious Portland beer, and excellent conversation, I headed to the BoF sessions, to hear about [Amazon's EC2](http://aws.amazon.com/ec2) service. I really wanted to learn more hard-core details about it, but so many people were just hearing about it for the first time, that the session was dominated by introductory questions. Oh, well!  
  
I was about ready to turn in. Lucky for me, [Rails Machine](http://railsmachine.com/) was having their party at my hotel. Bradley and company are really smart, cool people, and also offer a fantastic service, so I was glad to hang out with them for a few minutes. The most fun was jamming on harmonica with [Joey deVilla the AccordianGuy](http://www.joeydevilla.com/). After hearing him last year, I had brought a couple of my harps with me just in case, and we finally had a chance to bust out a couple of songs together. That was really fun! Thanks, Joey. If anyone has any photos or video, please post it somewhere...if not, well, you had to be there.