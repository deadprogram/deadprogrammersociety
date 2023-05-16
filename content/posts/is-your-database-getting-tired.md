---
title: 'Is Your Database Getting Tired?'
date: 2007-10-19T07:52:00.000-07:00
draft: false
url: /2007/10/is-your-database-getting-tired.html
tags: 
- domain specific languages
- databases
---

[![](http://g-ec2.images-amazon.com/images/I/51FQA7SSCAL._AA280_.jpg)](http://g-ec2.images-amazon.com/images/I/51FQA7SSCAL._AA280_.jpg)Is your database getting old and tired? [Mike Stonebraker](http://en.wikipedia.org/wiki/Michael_Stonebraker) thinks so. Stonebraker is a database guru and long-time researcher, and when I say database guru I mean one of the founders of Ingres, and former CTO of Informix, not just some guy who knows how to debug a stored procedure.  
  
Here is a juicy quote from a [recent article published by MIT](http://web.mit.edu/dna/www/vldb07hstore.pdf) of which he is one of the authors:  
  

> We conclude that the current RDBMS code lines, while attempting to be a "one size fits all" solution, in fact, excel at nothing. Hence, they are 25 year old legacy code lines that should be retired in favor of a collection of "from scratch" specialized engines. The DBMS vendors (and the research community) should start with a clean sheet of paper and design systems for tomorrow's requirements, not continue to push code lines and architectures designed for the yesterday's requirements.

  
  
Strong stuff! Especially for a generation of programmers for whom the relational database is just another ubiquitous part of their standard solution architecture. So is [SQL the new HTML](http://www.oreilly.com/pub/a/oreilly/tim/news/2005/09/30/what-is-web-20.html?page=3) as some have claimed? Or are we heading to a new generation of database engines that are created individually for each solution space, perhaps created on the fly and defined in a domain specific language.