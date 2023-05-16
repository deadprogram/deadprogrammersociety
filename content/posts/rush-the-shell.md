---
title: 'Rush The Shell'
date: 2008-02-20T14:20:00.000-08:00
draft: false
url: /2008/02/rush-shell.html
tags: 
- ruby
- unix
- rush
- rush shell
---

[![](http://www.ferhiga.com/progre/portadas/rush-mpictures.jpg)](http://www.ferhiga.com/progre/portadas/rush-mpictures.jpg)I just read the [latest posting](http://adam.blog.heroku.com/past/2008/2/19/rush_the_ruby_shell/) from Adam Wiggins, very cool dude, hard-core Rubyist, and friend. He has a new project called [Rush, the Ruby shell](http://rush.heroku.com/). Adam is one of the guys behind [Heroku](http://heroku.com/), which is a pretty amazing pure web browser-based IDE/deployment/hosting solution for Ruby on Rails, if you haven't seen that yet.  
  
Anyhow, like many of us, Adam seems like he just wants to use Ruby for everything. And when I say everything, I mean EVERYTHING. Writing bash scripts.... sucks. Destroying the sanctity of your Ruby code with```
\`bash-shell-command /ugly /madness\`
```is not hardly any better. My man is trying to help us do away with all that, by applying a friendly familiar Rubyness, not just caging the ugliness away.  
  
Here is a little taste of Rush, from the Rush site:  

>   
> How about killing those pesky stray mongrels? Before:  
> ```
>   
> kill \`ps aux | grep mongrel\_rails | grep -v grep | cut -c 10-20\`  
> 
> ```  
> After:  
> ```
>   
> processes.each { |p| p.kill if p.command == "mongrel\_rails" }  
> 
> ```  
> But rush is more than just an interactive shell and a library: it can also control any number of remote machines from a single location. Copy files or directories between servers as seamlessly as if it was all local. bash and ssh, we love you, but your era is past.  
>   
> Example of remote access:  
> ```
>   
> local = Rush::Box.new('localhost')   
> remote = Rush::Box.new('my.remote.server.com')  
> local\_dir = local\['/Users/adam/myproj/'\]   
> remote\_dir = remote\['/home/myproj/app/'\]  
> local\_dir.copy\_to remote\_dir   
> remote\_dir\['\*\*/.svn/'\].each { |d| d.destroy }  
> 
> ```  

  
I have not had a chance to play with Rush yet, but I'm sure I will be. Unix shell scripting is not syntactical sugar, that is for sure, and Rush looks pretty sweet.