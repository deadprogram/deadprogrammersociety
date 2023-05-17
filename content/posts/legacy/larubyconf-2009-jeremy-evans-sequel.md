---
title: 'LARubyConf 2009 - Jeremy Evans - "Sequel"'
date: 2009-04-05T20:22:00.000-07:00
draft: false
url: /2009/04/larubyconf-2009-jeremy-evans-sequel.html
tags: 
- ruby
- los angeles rubyconf
- sequel
- larubyconf2009
- larubyconf
---

[![](http://www.freeclassicimages.com/images/ghostbusters_2_1989.jpg)](http://www.freeclassicimages.com/images/ghostbusters_2_1989.jpg)

The next session at the 2009 [Los Angeles Ruby Conference (LARubyConf)](http://www.larubyconf.com) was [Jeremy Evans](http://code.jeremyevans.net/sequel) presenting [Sequel](http://sequel.rubyforge.org/), which is a very powerful database toolkit for Ruby.  
  
Ruby originally had adapters for each database. The problem was that each was very database specific. This was a problem due to both SQL differences, as well as API differences.  
  
no behavior  
  
1997 - ruby-postgres was first created.  
  
2000 - DBI  
  
2004 - Active Record  
Although AR made things easier, it had strong opinions. These opinions did not always map perfectly to any particular database.  
  
2007 - Sequel  
  
Completely DB independent API.  
  
Example is concatanating strings, which requires a completely different syntax in each flavor of SQL database.  
  
Concise  
  
Optional Behavior  
  
Opinions?  
  
Ruby should be like clay in a child's hands - Matz  
  
Sequel advantages:  
\- Simple - as possible but no simpler  
\- Flexible - opinions, not dogma  
\- Powerful  
\- Lightweight - 1/2 memory usage as active record  
\- Well maintained  
\- Easy to Contribute  
\- Easy to Understand  
\- More Fun  
  
Show me the \*\*\* code!  
```
  
require 'seq'  
DB = Sequal.sqlite('larun')  
DB\[:attendees\].count  
\# => 1  
  
DB\[:attendees\].first  
\# => {:name ='', :address =>}  

```  
Transactions  
```
  
DB.trans do  
  DB\[:entry\],insert(:account\_id => 1)  
  
  ...  
  
end  

```  
  
SQL Loggers  
```
  
DB.loggers << Logger.new($stdout)  

```  
  
Each DB has its own connection pool  
```
  
DB\[:table\].all # or .each  
  
.update(:column => 'value)  
  
.delete  
  
DB\[:table\] # this is a dataset... like query cursor  

```  
  
Sequel is a functional API, where object methods return copies of themselves.  
  
.select - while columns  
.filter  
.order  
  
This means you can easily chain function calls, like jQuery. Awesome!  
  
Sequel represents its internal objects using SQL's own internal representations  
  
Sequel has 'core' and 'model'  
```
  
class Attendee < Sequel::Model  
  many\_to\_one  
  one\_to\_many  
    
    
end  

```  
  
Hooks & Validations - got 'em  
  
Sequel it built entirely out of plugins. That sounds interesting, but experience with DataMapper has shown me that too many plugins may not be a good thing. However, I do not have any direct experience with Sequel yet, so this may be a non-issue.  
  
13 - # of database adapters that Sequel supports today  
  
Database graphing  
  
Everything was going so well up to this point. However, Jeremy then tried to do his demo on Windows, just to show that if you are one of the poor souls using Windows, it can still work for you. He failed to account for the quirkiness of conference display adapters, and what that can do to a machine. Oh well, no demo.  
  
That said, I was really impressed by what I heard about Sequel. I think I will have to try it out on something, just to see how it does.