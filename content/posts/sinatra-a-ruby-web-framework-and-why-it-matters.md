---
title: 'Sinatra, a Ruby web framework, and Why It Matters'
date: 2007-10-24T09:16:00.000-07:00
draft: false
url: /2007/10/sinatra-ruby-web-framework-and-why-it.html
tags: 
- domain specific languages
- web development
- merb
- sinatra
- rails
- ruby
- ruby on rails
---

[![](http://sinatra.rubyforge.org/logo.png)](http://sinatra.rubyforge.org/logo.png)As followers of this blog know, I am very interested in the Ruby language itself, not just web development. But it is undeniable that Ruby has become popular largely due to web development powered by Ruby on Rails. However amazing Rails is, however, it is not the final web framework to be developed in Ruby.  
  
When [Ari Lerner](http://xnot.org/) first told me of the [Sinatra](http://sinatra.rubyforge.org/) project, I was interested to see where he was going with it. Now that I have seen it, I totally get it, and I am more interested than ever. Let's compare it to Rails, [Camping](http://camping.rubyforge.org/), and [Merb](http://merb.rubyforge.org/), to better understand where Sinatra fits in, and why Ruby programmers should take a look at it.  
  
Unlike Ruby on Rails, Sinatra is not a Model-View-Controller (MVC) based framework for creating websites. If you want helper functions that help you create forms, connect to databases, or any of the other myriad of functions that Rails provides, you will not find them. Instead, Sinatra is a very simple, yet powerful, Domain Specific Language (DSL) for defining RESTful HTTP actions, and then defining how the application is going to respond to them.  
  
Rails requires a separate routes file to define how the web application is going to respond to requests, which hooks up to the appropriate controllers/models. Sinatra defines the simplest thing that could possibly work. When you declare a new "get" or "post" action, Sinatra will automatically add the route, and simply start responding to requests that match.  
  
Here is a simple example of a Sinatra application:  
  
```
  
require 'rubygems'  
require 'sinatra'  
  
get '/' do  
   "Hello world"  
end  

```  
  
As you can see, a Sinatra application's code is tiny, similar to Camping in that you can easily create an entire web application deployed as a single file. Unlike Camping, Sinatra does not have such a "crazy meta magic" feel to it... why's coding style is not for the faint of heart.  
  
Like Merb, Sinatra is implemented as a Mongrel handler. Also, like Merb it is both thread-safe and has better performance than Rails. However, where Merb tries to be a "Rails-lite" for devs who are already familiar with Rails, but want a more bare-metal approach, Sinatra unabashedly takes an entirely different direction with its very minimal DSL-syntax.  
  
Not to say that you cannot use ActiveRecord or whatever other Ruby gems you want to create your application. But unlike Rails, Sinatra's base core is incrediby minimal, and it puts the onus on the developer to decide what to include, instead of adding a bunch of things that may not be appropriate for the type of application that Sinatra would be good for.  
  
So what would it be good for? API implmentations, quick minimal applications, and web development that does not want or need things that are included in Rails, like ActiveRecord. Control panel mini-applications, or perhaps widgets. I am looking forward to really getting into some fun with Sinatra... check back soon here for more.  
  
Yesterday, the [Ruby Inside](http://www.rubyinside.com/) blog mentioned Sinatra, and some of us have been [digging it](http://digg.com/programming/Sinatra_Classy_web_development_dressed_in_a_DSL) for the last few days. Take a look, and you will enjoy the appeal of a simplicity and elegance in development you haven't felt from Ruby for a long time... a very long time.