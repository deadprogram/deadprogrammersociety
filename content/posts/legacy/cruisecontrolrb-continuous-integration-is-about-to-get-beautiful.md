---
title: 'CruiseControl.rb: Continuous Integration Is About To Get Beautiful'
date: 2007-03-13T14:09:00.000-07:00
draft: false
url: /2007/03/cruisecontrolrb-continuous-integration.html
tags: 
- ruby
- cruisecontrol.rb
- ruby on rails
- continuous integration
---

[![](http://cruisecontrolrb.thoughtworks.com/images/cruise_logo_large.png)](http://cruisecontrolrb.thoughtworks.com/images/cruise_logo_large.png)At last, Ruby has a real Continuous Integration system, not just some crazy hacked-together solution. Nothing against crazy, hacked-together solutions, but your CI system is not the place for such madness. From those wonderful folks at [Thoughtworks](http://www.thoughtworks.com), we now have [CruiseControl.rb](http://cruisecontrolrb.thoughtworks.com), to join the CruiseControl and CruiseControl.NET offerings for Java and .NET projects respectively.  
  
I have been a constant user of CruiseControl.NET for all of the MS-platform projects for the last couple of years, and having a powerful, flexible system has been great. However, having to pay heavily of the angle-bracket tax to create the XML for the NAnt build scripts, CC.NET config files, and pretty much everything else has been a real pain. The pleasure has been the real-time integration with the CCTray notification program (shows up red in your system tray, and pops up a balloon notification when a build has been broken).  
  
Now, a pure Ruby solution has been created. Although a very young offering, the incredible simplicity of Ruby allows a far easier extensibility than the other CruiseControl options. Here are a few of the interesting features:  
  

  
*   All CruiseControl.rb config files are Ruby, for nice DSL-ish syntax
  
*   Uses Rake by default for builds, but can support NAnt, Ant, MSBuild or anything other build tool. In other words you CAN use CruiseControl.rb as your CI systems for any target language or environment, not just for Ruby or Ruby on Rails projects.
  
*   Build messages can be sent via IM using Jabber
  
*   The same CCTray system tray application can monitor CruiseControl.rb servers as well as CruiseControl.NET servers.
  

  
  
CruiseControl.rb looks to have the core features required for a decent, even an amazing CI system. However, being such a new tool it still lacks some really cool and useful add-on things like integration with Fitnesse, Simian code analysis, and the other neat [add-ons that can easily integrate with CruiseControl.NET](http://confluence.public.thoughtworks.org/display/CCNET/Using+CruiseControl.NET+with+other+applications). Given that the CruiseControl.rb is pure Ruby, and the prolific nature of the Ruby open source community, I would not be surprised if those gaps are filled very quickly.  
  
Rock on, Thoughtworks!