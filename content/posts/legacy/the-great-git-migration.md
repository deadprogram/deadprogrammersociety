---
title: 'The Great Git Migration'
date: 2008-10-26T10:15:00.000-07:00
draft: false
url: /2008/10/great-git-migration.html
tags: 
- msysgit
- subversion
- git
- svn
---

I have been using [git](http://git.or.cz/) for a while, not quite as long as the [really](http://www.rubini.us/) [cool](http://peepcode.com) [kids](http://www.gitcasts.com/), but long enough to have become a git snob. As such, having to work on existing projects that were using that nasty old [subversion](http://subversion.tigris.org/) was just like, a drag, man.  
  
I kept saying, "I'm going to migrate everything over to git." Somehow, I just never seemed to find the time. Another little problem was the underwhelming level of support for git on Windows. Yes, a couple of projects I am involved with have Windows code for client applications in there.  
  
So when the [msysgit](http://code.google.com/p/msysgit/) project was announced, I followed it with great interest. The most recent versions are actually quite usable. I was able to install on a Vista VM (I use [VMWare Fusion](http://www.vmware.com/products/fusion/) on OS X to keep the Windows thing to a minimum) and connect to several repositories on both [github](http://github.com/) and [Unfuddle](http://unfuddle.com/) with ease.  
  
A couple of hours waiting on git-svn to [import](http://github.com/guides/import-from-subversion) the old repositories (under OS X, cause mysysgit does not appear to support git-svn), and it was all git all the time. No more svn on any of the projects I am actively working on. And I was able to preserve the entire version history of each repo, too.