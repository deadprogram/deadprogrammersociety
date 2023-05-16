---
title: 'In Search Of Search'
date: 2008-05-19T15:09:00.000-07:00
draft: false
url: /2008/05/in-search-of-search.html
tags: 
- mysql
- acts_as_ferret
- postgres
- ruby
- sphinx
- ferret
- ruby on rails
- thinking sphinx
---

[![](http://yourtech.typepad.com/main/WindowsLiveWriter/ThesearchforSTIIITheSearchforSpock_9B38/star_trek3_thumb1.jpg)](http://yourtech.typepad.com/main/WindowsLiveWriter/ThesearchforSTIIITheSearchforSpock_9B38/star_trek3_thumb1.jpg)My client was having troubles. The site was crashing, seemingly at random. QA was baffled, management concerned. After hunting thru logs, the culprit was found: the ferret search service.  
  
Despite having configured [acts\_as\_ferret](http://projects.jkraemer.net/acts_as_ferret/) to use the DRb server option, the "whole thing" would fall apart on a regular basis whenever the ferret daemon would crash... which was pretty often. The ruby on rails plugin acts\_as\_ferret would revert to a local mode of operation, which would only make matters worse when competing mongrels would corrupt the index files on disk.  
  
Much has been [written already about this](http://www.ruby-forum.com/topic/137629) by [more](http://www.robbyonrails.com/) [famous](http://brainspl.at/) Rubyists then myself, so the time had come to make the switch to [Sphinx](http://www.sphinxsearch.com/) like all the rest of the cool kids. However, there were a few tricky issues that awaited.  
  
One is that the client site was using [PostgreSQL](http://www.postgresql.org/) instead of the more common [MySQL](http://www.mysql.com/). This meant you had to have already downloaded the pgsql client libs, and also when compiling the sphinx server use the --with-pgsql flag. However, what they didn't mention was that you would need to also download and include the MySQL client libs AS WELL, even if you were not using MySQL. Good to know... seems like a big of baggage to carry, but whatever.  
  
That was one obstacle avoided. The next would prove to be more subtle and complex. There are four different choices of Ruby on Rails clients for Sphinx:  
  

*   [acts\_as\_sphinx](http://www.datanoise.com/articles/2007/3/23/acts_as_sphinx-plugin)
  
*   [Sphincter](http://seattlerb.rubyforge.org/Sphincter/)
  
*   [UltraSphinx](http://blog.evanweaver.com/files/doc/fauna/ultrasphinx/files/README.html)
  
*   [Thinking Sphinx](http://ts.freelancing-gods.com/)

  
  
I looked briefly at acts\_as\_sphinx, but my superficial prejudices against anything named "acts\_as\_" caused me to continue my search for search. Next, I tried Sphincter, just to prove that I could be accepting about project names. However, I was not successful as getting it working correctly, and project development seemed like it had slowed to near non-existence. The search moved on.  
  
My search was getting desperate as half of the options had been eliminated. I briefly perused UltraSphinx and I started to get a little excited. Development was active, and proper functionality with Postgres was claimed. But there was just one little problem: this client's site is still Rails 1.2.x.  
  
Now, before you all start throwing various disparaging comments my way, consider how much work some clients are willing to pay far vs. something that they can actually see. Multiply that by how long since they started their project, and you are starting to get the idea of where this thing is at. I probably should have MADE them upgrade at that point, but I'm just not that kind of guy.  
  
So that left Thinking Sphinx. I dove in with the manic desperation of someone looking to avoid major amounts of work. That rarely works out well, but in this case it wasn't so bad. The latest trunk of thinking sphinx had comments that said "basic postgres functionality" so perhaps it was possible after all.  
  
Several hours and some major hacking of the original plug-in to actually handle proper psql syntax later, and something was working! I will try to come up with patch to thinking-sphinx for [freelancing-god](http://freelancing-gods.com/), cause his work was a great help.  
  
Lastly, the delta index. By adding a single field (boolean for MySQL, integer for Postgres) you can remove the need to reindex all data every time a record is updated. Sphinx allows storing the changed records in a separate index (delta) that it will search along with the main index. This way, you do not have to wait for reindexing to be able to search, but you also do not have to reindex the entire data set every time any data within it is changed. You still need to do a complete reindex, but that can occur at off-peak hours, instead of constantly.  
  
The code was deployed, and now all was well with the world. My search was complete.