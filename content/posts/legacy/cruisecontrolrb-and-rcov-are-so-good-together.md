---
title: 'CruiseControl.rb and RCov Are SO Good Together'
date: 2007-06-24T09:00:00.000-07:00
draft: false
url: /2007/06/cruisecontrolrb-and-rcov-are-so-good.html
tags: 
- cruisecontrol.rb
- ruby on rails
- continuous integration
---

I spent a bit of time this morning getting [CruiseControl.rb](http://cruisecontrolrb.thoughtworks.com/) and [RCov](http://eigenclass.org/hiki.rb?rcov) working together for a new client's fairly LARGE Ruby on Rails (70+ models, 40+ controllers) project. If you are not familiar with CruiseControl.rb, it is the Ruby based continuous integration tool from [ThoughtWorks](http://www.thoughtworks.com/). RCov, on the other hand, is a very well known code coverage tool for Ruby. The implementation was incredibly simple, but finding the information on how to get the two working together required a perusal of the CruiseControl.rb code itself.  
  
First of all, you will need to install the [rails\_rcov](http://blog.codahale.com/2006/05/26/rails-plugin-rails_rcov) plugin. This useful plugin allows you to really easily run RCov using rake, and is essential to simple RCov integration with your CruiseControl.rb builds. You can install rails\_rcov like this:  
  
```
  
./script/plugin install http://svn.codahale.com/rails\_rcov  

```  
  
Use the "-x" option if you want to use an svn:external link to the latest version of the plugin. I personally don't like to do that...I want control over when the software I am using gets updated, thanks.  
  
Once the plugin is installed into your project you have some useful rake tasks like this one:  
  
```
  
\# sort by coverage  
rake test:units:rcov RCOV\_PARAMS="--sort=coverage"  

```  
  
Now you are ready for the final bit, which is adding a "cruise.rake" task to the "lib/tasks" directory of your Ruby on Rails project. The task should have something like this, which was lifted verbatim from the CruiseControl.rb build of CruiseControl.rb itself (that all sounds kinda twisted, but it is cool):  
  
```
  
desc 'Continuous build target'  
task :cruise do  
  out = ENV\['CC\_BUILD\_ARTIFACTS'\]  
  mkdir\_p out unless File.directory? out if out  
  
  ENV\['SHOW\_ONLY'\] = 'models,lib,helpers'  
  Rake::Task\["test:units:rcov"\].invoke  
  mv 'coverage/units', "#{out}/unit test coverage" if out  
    
  ENV\['SHOW\_ONLY'\] = 'controllers'  
  Rake::Task\["test:functionals:rcov"\].invoke  
  mv 'coverage/functionals', "#{out}/functional test coverage" if out  
    
  Rake::Task\["test:integration"\].invoke  
end  

```  
  
That's it. Now you have incredible code coverage goodness right within your build. You can even browse the source within the browser window of the CruiseControl.rb dashboard and see which lines of code were covered by your tests, and which were not...  
  
So if you have a Ruby on Rails project, with a project team of greater than 1 developer, you had better start using CruiseControl.rb. It is too easy, and the payoff of doing continuous integration is huge!