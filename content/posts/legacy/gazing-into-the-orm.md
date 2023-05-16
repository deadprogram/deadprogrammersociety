---
title: 'Gazing Into The ORM'
date: 2007-02-23T08:24:00.000-08:00
draft: false
url: /2007/02/gazing-into-orm.html
tags: 
- databases
- software architecture
- ruby on rails
---

Jeremy Miller has an [interesting post today](http://codebetter.com/blogs/jeremy.miller/archive/2007/02/23/Don_2700_t-Let-the-Database-Dictate-Your-Object-Model.aspx) regarding [Object Relation Mapping (ORM)](http://en.wikipedia.org/wiki/Object-relational_mapping). Droves of developers are now flocking to ORMs via [Ruby on Rails](http://www.rubyonrails.org/), [Castle](http://www.castleproject.org/), or one of the other many projects in this space, so it is good to have people like Jeremy exploring from a real implementation perspective.  
  
Anyhow, his post really is concerned with applications that use an existing database, have a large amount of logical processing. Simply applying an ORM without considering the logical implications of the data, not only fails to take advantage of the power of ORMs, but falls into a bit of a quagmire, with potentially a very non-DRY result.  
  
Some of the specific examples he cites are:  
  

>   
> 
> *   Big tables don't map to a single object.  I don't think it's possible that a class with a 100 different properties can possibly be cohesive.  We'd be much better off in terms of writing business logic if that 100 column table is modelled in the middle tier by a half dozen classes, each with a cohesive responsibility.  It may make perfect sense to have only one table for the entire object hierarchy, but big classes are almost always a bad thing.
> *   [Data Clump and Primitive Obsession code smells](http://www.codinghorror.com/blog/archives/000589.html).  A database row is naturally flat.  I want to do a bigger post on this later, but think about a database table(s) with lot's of something\_currency/something\_amount combinations.  There's a separate object for [Money](http://www.martinfowler.com/eaaCatalog/money.html) wanting to come out.  If you make your business objects pure representations of the database you could easily end up with a large amount of duplicate logic around currency and quantity conversions.
> *   Natural cases for polymorphism in your object model.  I think the roughest part of O/R mapping is handling polymorphism inside the database.  Check out Fowler's patterns on [database mappings for inheritance](http://www.martinfowler.com/eaaCatalog/).
> 
>   

  
  
He then goes on to make an important point regarding the role of the database in the software architecture of your application. Basically there are only two perspectives that make any sense:  

>   
> 
> *   The database is paramount, and the system is expressed and understood in terms of the tables and rows in the database.  The application code and even user interface is just a conduit to get information back and forth into the database.  You design the database first and then build the business and data layers to match the database.  In the .Net world we might just consume raw DataSet's in the application, effectively just working with the database tables offline.
> *   The behavior of the system, primarily in the middle tier and user interface, is paramount, and the database is "just" a means to persist the state of the system.  The database is either built to match the business classes or designed somewhat independently.
> 
>   

  
  
So in the case of an application that has significant business logic, it would seem to me that the second case is quite preferable. However, in the case where a legacy database is involved, how can we really avoid the first? I have seen many applications get stuck in that quagmire myself, and one real problem is that the business logic becomes a lot harder to represent cleanly when having to preserve the existing database schema's problems. Especially when trying to achieve a very DSL like approach for business service layers. The less that the domain experts have to understand the database, and can just speak in terms of domain concepts, the better!