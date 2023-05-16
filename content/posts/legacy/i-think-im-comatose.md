---
title: 'I Think I''m Comatose'
date: 2008-11-04T10:50:00.000-08:00
draft: false
url: /2008/11/i-think-im-comatose.html
tags: 
- rails
- ruby
- comatose
- ruby on rails
---

[![](http://images.publicradio.org/content/2006/05/09/20060509_killbill_2.jpg)](http://images.publicradio.org/content/2006/05/09/20060509_killbill_2.jpg)This last weekend, I upgraded a pretty complex application to the latest [Ruby on Rails](http://www.rubyonrails.org/), and consequently had to upgrade a bunch of the plugins. In the case of [Comatose 2.0](http://github.com/darthapo/comatose/tree/master), this was well timed, as there is a new release.  
  
If you have never heard of Comatose, it is a very cool mini-CMS that you add to your Rails app as a plugin. For cases where you have an applcation, and you want to put the 'static' pages under the control of the users, while still integrating with your application, Comatose is the best option I have discovered.  
  
If you are just discovering Comatose, just go check it out. Now. If, on the other hand, you are running into any problems going to the new version, read on.  
  
Since this application had been running the 0.8 version of Comatose, I ran into a little problem, which has been documented on Google Groups [here](http://groups.google.com/group/comatose-plugin/browse_thread/thread/e6402c29de92edc7/db9d2dd0fa9ac9d7?#db9d2dd0fa9ac9d7).  
  
If you are running the older version of Comatose, you have a migration that contains this:  
  
```
  
 module Comatose  
   class Page < ActiveRecord::Base  
     set\_table\_name 'comatose\_pages'  
     acts\_as\_versioned :if\_changed => \[:title, :slug, :keywords, :body\]  
   end  
 end  

```  
  
The new version of Comatose, however requires this:  
```
  
 class ComatosePage < ActiveRecord::Base  
   set\_table\_name 'comatose\_pages'  
   acts\_as\_versioned :if\_changed => \[:title, :slug, :keywords, :body\]  
 end  

```  
  
What I did was, go and change the original migration to match the newly required format. This will allow a new clean installation to work correctly. Then, to handle upgrade installs, I created a separate rake task to perform the migration steps as described [here](http://locomotivation.com/2008/06/16/updating-comatose-to-rails-2-1).  
  
Voila. Now this app is happily running the latest Rails, Comatose, [ActiveScaffold](http://activescaffold.com/), [ActiveMerchant](http://www.activemerchant.org/), and a few other plugins too. Life is good.