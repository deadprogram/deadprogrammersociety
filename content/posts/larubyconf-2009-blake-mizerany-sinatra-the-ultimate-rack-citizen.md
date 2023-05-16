---
title: 'LARubyConf 2009 - Blake Mizerany - "Sinatra: the Ultimate Rack Citizen"'
date: 2009-04-07T12:19:00.000-07:00
draft: false
url: /2009/04/larubyconf-2009-blake-mizerany-sinatra.html
tags: 
- sinatra
- ruby
- los angeles rubyconf
- larubyconf2009
- larubyconf
---

[![](http://1.bp.blogspot.com/_SgxaAaUGqzY/SduqsU4uYRI/AAAAAAAABuc/jJNFX8yokJk/s200/Picture+1.png)](http://1.bp.blogspot.com/_SgxaAaUGqzY/SduqsU4uYRI/AAAAAAAABuc/jJNFX8yokJk/s1600-h/Picture+1.png)I was very happy when the next presenter at the [Los Angeles Ruby Conference 2009 (LARubyConf)](http://www.larubyconf.com/) was [Blake Mizerany](https://twitter.com/bmizerany), creator of the very cool Ruby micro-framework [Sinatra](http://sinatrarb.com). As long-time readers of this blog know, I am very into Sinatra.  
  
There has been an incredible amount of work going into Sinatra lately, so I was very interested to catch up on what the team has been up to.  
  
What is Sinatra? A Ruby Domain Specific Language (DSL) Mapping REST to simple actions  
  
Why?  
\- small  
\- fast  
\- great rack and ruby citizen  
\- strong focus on HTTP  
\- HTTP caching helpers built in before it was cool  
\- content negotiation  
\- no boilerplate  
\- dead simple config when the default are not enough  
\- smart configuration  
\- DOCS- sinatrarb.com  
\- extending is easy  
\- rack is the only dependency  
\- very low WTF to LOC ratio (jeremy mcnally's rubyfringe talk)  
  
when?  
\- a few controllers models and views  
\- starting any web application  
\- you need reusable apps and/or middleware and/or resources  
\- you need speed  
  
who?  
\- heroku  
\- github  
\- taps  
\- integrity  
  
sinatra in your gems  
\- a mini-github for offline repo browsing  
\- a local plugin and play wiki  
\- memcached utilization graphs  
\- config reusable github hook  
  
Example: NotTwitter  
  
As classic Sinatra  
```
  
set :username,  
  Proc.new { fail "yo"}  
    
get '/' do  
  ...  
end  

```  
  
Change  
```
  require 'sinatra'
```  
to  
```
  require 'sinatra/base'
```  
  
  
But I want to deploy to Passenger or Heroku! No problem.  
  
./bin/install-not-twitter  
Copy example config.ru to cwd  
Copy .gems file  
  
.ru is a standard Rack config file.  
  
.gems is a Heruku configuaration file that will handle any needed Ruby gems installations  
  
```
  
  git init && git add .  
  git commit  
  heroku craete  
  git push heku  aster  
  heroku   

```  
  
3 Awesome Features in Sinatra  
pass - I cannot handle this request, try the next route  
forward - sinatra as middle ware... done my job, let the next app take over... pop in front of rails metal  
use - Sinatra loves rack so much, we made sure not to hide it  
  
  
Resources  
[http://sinatrarb.com](http://sinatrarb.com)  
[http://github.com/rack/rack](http://github.com/rack/rack)  
[http://github.com/rack/rack-contrib](http://github.com/rack/rack-contrib)  
[http://github.com/rtomayko/rack-cache](http://github.com/rtomayko/rack-cache)  
  
If you are doing everything with Rails, you are probably using too much for the job. Sinatra is simple, fast, and extensible. I am using it in two production applications right now, along with Rails. Sinatra handles parts of the application better than how Rails does, so that is how I roll.  
  
Especially with the ever increasing momentum behind Rack, Sinatra is a good bet for getting things done. Combined with Rails Metal, and you really have it all.