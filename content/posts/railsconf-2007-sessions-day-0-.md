---
title: 'RailsConf 2007 - Sessions (Day 0)'
date: 2007-05-19T07:55:00.000-07:00
draft: false
url: /2007/05/railsconf-2007-sessions-day-0.html
tags: 
- ruby
- railsconf2007
- ruby on rails
---

[![](http://conferences.oreillynet.com/images/rails2007/layout/railsConf-logo.gif)](http://conferences.oreillynet.com/images/rails2007/layout/railsConf-logo.gif)Well, I had just got back to my room after day 0 of RailsConf 2007, which was the tutorial sessions before the main conference began. After a fun evening of pizza and beer with the Pragmatic Programmers, I thought I would try to get down some thoughts about the day's events.  
  
Yesterday, I attended "Scaling Rails From The Ground Up" followed by "Harnessing Capistrano". It is very hard to have tutorial sessions at a conference. They either are too basic to satisfy advanced users, or too complex for noobs. In the case of RailsConf 2007, they probably achieved both at the same time. Since the Pragmatics had the intro to Rails thing locked up, the other tutorials probably should have gone way advanced. Friday's sessions will be shorter and more focused, so I expect to get more out of them for myself personally. Not that they were bad, but many of us who were at last year's conference were hoping for more advanced material.  
  
The real action was on IRC, of course. Just before last year's RailsConf 2006, my old notebook's screen died. As a result I was not connected to the hive mind where the really interesting communication. This year, my still mostly shiny MacBook Pro served me well, by letting me experience the full RailsConf experience. You could certainly tell who was connected to #railsconf, from the snickers that escaped from the occasionally brilliant witty commentary.  
  
**Scaling Rails From The Ground Up**  
This presentation was given by Jason Hoffman of Joyent. His presentation did indeed deal with scaling Rails from the ground up. Litterally, he mentioned the kind of flooring that you need for a minimal data center (concrete, if you must know). His talk went from 50000 foot view to a close-up view of a blade of grass, but he left out much of what goes in between during the first part of this presentation. Yes, he told us what kinds of power connectors they like to use at Joyent.  
  
Here are a few excerpts from his talk:  
  
\*Moving parts of your Ruby code that are extremely performance sensitive to C extensions to Ruby is a very viable optimization technique.  
\*Power is a real limitation for building out a data center. There are large physical data centers that have a lot of empty rack space, due to being unable to access enough power to ad any additional servers.  
\*Compared to DNA sequencing, the amount of data on the web isn't that much.  
\*Scaling goes in both directions...you should be able to either up OR down. From running your app on a USB key, to running on a large server farm.  
\*Look for weak points in the architecture, for example a powerful box that has an OS limitation due to number of files in a directory.  
\*Scalable means "Lego"-like adding or removing of elements while keeping the integrity of the system intact.  
\*Rails is just one part of the scaling solution, the rest of the stack that Rails is running on needs to be well understood and kept as simple as possible, as it is easy to over-engineer fast.  
\*Use other data stores besides just relation databases where appropriate. His example was using LDAP for your user authentication, J-EAI for a message processing bus, and Postgres for the relational data.  
  
One thing that impressed me was the amount of Java technologies in the stack that Joyent is espousing. For a community that spends so much time dissing Java, a whole lot of integration between Rails and Java has occurred over the last year.  
  
Jason told some pretty amazing stories about hosting and colocation providers that they dealt with in the past that went out of business in spectacular ways. I'm not sure which was my favorite, trying to buy back their own servers from a bankruptcy proceeding in Sweden, or the one about the baker's racks with normal white box PC clones stacked on them when they were being charged for nice rack-mount servers. BTW, it is only legal to use backer's racks for electrical equipment in Texas. Zap!  
  
Overall, the session was about half details about how Joyent has built their data center out, and about half scaring people into using some hosting provider, like Joyent, for example. Of course, can you blame him? That is a big part of what presenting at conferences is all about! Trading some useful information in exchange for getting to do some sales pitching to a crowd of likely customers.  
  
**Harnessing Capistrano**  
  
Jamis Buck, the erstwhile Rails committer and creator of Capistrano nee Switchtower gave the next session that I attended, an overview of Capistrano, including the upcoming 2.0 release.  
  
Although most of us are using Cap as a deployment tool, it can be used for many other interesting things. Some examples are:  
  
_Ad-hoc monitoring_  
\*Query all servers at once  
\*Uptime  
\*Operating system version (uname)  
\*Currently running processes (ps)  
\*Free disk space (df)  
\*Reading logs  
\*Searching logs  
  
_Query database server status_  
_Server Maintenence_  
\*nfs mount  
\*symlinks  
\*pkg\_add $home/imgmagic  
  
_Troubleshooting_  
_Custom tasks_  
_Clearing cache files_  
_Grep log files_  
  
Capistrano Assumptions:  
Capistrano makes certain assumptions that are requirements for its use.  
\*SSH  
\*POSIX system  
\*Public keys or identical passwords on all servers  
  
Other Interesting Things You Can Do With Capistrano  
Gateways - when you cannot access the server directly over net, you can use set :gateway to tunnel through SSH to target server  
set :gateway, "capistrano.demo"  
  
Invoking Remote Commands  
You can invoke arbitrary commands on a server using "cap -e invoke", and this does not even require CAP file. One drawback of invoke is that Cap needs to reconnect on each invocation.  
  
An alternative to this is the "cap -e shell" command. This is similar to invoke, but caches connections, and can execute both tasks and commands.  
  
Cap 2.0 adds namespaces for tasks. This is very important if you were using a third-party plugin that had its own Cap tasks.  
  
Variables  
Cap variables can be assign values passed in when Capistrano is called. They can be loaded either before or after recipes are loaded. If loading vars after recipies are loaded, any values assigned in the  
  
Transactions  
Cap allows you to wrap one or more deployment commands in a transaction. If a transaction is performed on multiple machines, and fails, Cap auto restores the state of each machine on failure  
Example:  
on\_rollback { task\_to\_perform\_when\_transaction\_fails }  
  
Deployment Recipes  
Capistrano 2 allows you to opt out of deployment recipes, for custom deployment recipes, or for non-deployment uses. The default deployment recipes in Cap do have several assumptions:  
\*Application code in under source control  
\*The app os a web application (Rails)  
\*Production environment is ready (all servers are setup and running)  
\*Using standalone FCGI listeners  
  
How to Cap 2.0 Your App  
Switching to Capistrano 2.0 should not be difficult, according to Jamis. The basic process is:  
\*goto your application base directory  
\*run "capify ."  
\*setup a minimal capfile  
  
There are a couple situations where you might have troubles when upgrading to 2.0:  
\*3rd party ext. and libs  
\*Overridden or extended tasks without namespace  
  
As a result, Cap 2.0 has a compatibility mode, which provides tasks with old names they need.  
  
Conclusions  
Despite the similarity of Rake and Capistrano syntax, they are nothing alike underneath, nor is Cap intended to replace Rake. The new Net::SSH and Net:SFTP gems give Cap even more power as a remote scripting tool to handle not just deployment, but all sorts of time-consuming tasks. The benefits of using Capistrano increase the more machines you are trying to get your software deployed on. And if you are not using it now, what are you waiting for?