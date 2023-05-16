---
title: 'E Is For Editor Envy'
date: 2007-03-28T16:35:00.000-07:00
draft: false
url: /2007/03/e-is-for-editor-envy.html
tags: 
- ruby
- e the editor
- ruby on rails
---

[![](http://www.absoluteanime.com/fullmetal_alchemist/envy.jpg)](http://www.absoluteanime.com/fullmetal_alchemist/envy.jpg)I love it when I find out about a cool new tool. In this case, it is [E](http://www.e-texteditor.com), a Windows clone of the ubiquitous Mac text editor [TextMate](http://macromates.com/). Looks like this project has been around for awhile, but I just heard of it thanks to a blog entry about [creating a Mac-like environment under Windows](http://garbageburrito.com/blog/entry/391/a-macesque-rails-development-environment-on-windows).  
  
Installing E is not a small task, although it is not a difficult one. This is due to the fact that E relies heavily on [Cygwin](http://www.cygwin.com/) to support "bundles" which is how TextMate creates their oh-so-useful macro and template collections. I have installed it on two machines now, and I had trouble with cygwin on both of them. Sigh! After a few missteps, I managed to get Cygwin installed and E working mostly correctly.  
  
Having a text editor that supports changing themes without a massive amount of pain is really nice for a guy like me who likes that retro black background thing. And having the same basic macro capabilities as TextMate under Windows is awesome! I have TortoiseSVN installed, and E's project view lets me see the change status and commit or diff changes. All of your basic needs in a Ruby on Rails editing tool are there.  
  
But basic compatibility is all you get at this point. E does support TextMate "bundles", but there are plenty of differences in the bundles on each platform (Mac vs. Windows), enough so that plenty of things don't work. On each of the two machines I tried E on, I had different problems with the more advanced bundle abilities of bothe the Ruby and the Rails bundles.  
  
The author of E is [working closely with the author of TextMate](http://e-texteditor.com/blog/2006/textmate_on_windows), being as they are both Danes and very open minded, and is planning on a Unix version to join the Windows version. Even with the weirdness and slowness of the Cygwin install, E is rocking, so on Ubuntu, for example, E could become a cornerstone of a slick development platform. At this point, the real TextMate on the Mac is still the optimal route to programming glory. If you need to work under Windows, E is worth trying out, just be ready for some rough edges.