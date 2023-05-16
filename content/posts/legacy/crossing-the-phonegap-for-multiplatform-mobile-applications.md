---
title: 'Crossing The PhoneGap For Multiplatform Mobile Applications'
date: 2010-01-18T08:30:00.000-08:00
draft: false
url: /2010/01/crossing-phonegap-for-multiplatform.html
tags: 
- mobile
- phonegap
- git
- iphone
- android
---

[![](http://www.elvincountry.com/travel-images/02802741.jpg)](http://www.elvincountry.com/travel-images/02802741.jpg)I had first heard of the [PhoneGap](http://phonegap.com/) open source framework for multiplatform mobile development last year at the [FutureRuby](http://futureruby.com/) conference in Toronto. Honestly, I did not really concentrate on all they were saying at the time, and in the flurry of info including back-to-back mobile sessions with [Rhomobile](http://rhomobile.com/), I did not fully retain a clear picture of what they had to offer. My bad.  
  
It was not until late last year, while working on plans for a very cool mobile application, that I was reminded about PhoneGap by one of my colleagues. After a brief evaluation of their benefits vs. the other multiplatform options, we decided to use PhoneGap on this particular project. We have made some amazing progress with using PhoneGap for mobile development since then, and I thought I would share a few of the lessons learned.  
  
First of all, a quick explanation of how PhoneGap works. [Jesse MacFadyen](http://blogs.nitobi.com/jesse), one of the programmers at [Nitobi](http://nitobi.com/), the primary developers of PhoneGap, has a [good blog post](http://blogs.nitobi.com/jesse/2009/11/04/phonegap-for-iphone-exposed/) where he breaks down how the PhoneGap framework works on iPhone. Here is my much condensed take on what he is saying.  
  
All of the mobile platforms supported by PhoneGap have some kind of web browser control. A PhoneGap application is a packaged up application which is a webpage or mini-website, that executes inside whatever web browser control is available on that platform. Add in a standard JavaScript API to a wrapper that accesses the device-specific functionality like GPS or the accelerometer, and you can hook up the JavaScript on your "page" to the hardware.  
  
But don't make the mistake of thinking you should just slap together some web pages formatted for mobile. Rather, you can and must think of it as an application that is written in the form of a single web page with a bunch of JavaScript. To access server data, you will need to write some AJAX code to access the remote resources, then update your UI accordingly. The good news is you can use familiar JavaScript libraries such as [jQuery](http://jquery.com/) to do so. We chose [jqTouch](http://www.jqtouch.com/) to get a very iPhone-like UI.  
  
The PhoneGap framework is under very active development. New code is being committed to their [github repo](http://github.com/phonegap/phonegap) frequently. As such, you really do need to have git installed, and some working knowledge of how to use it, to get things setup.  
  
In fact, the device specific functionality for each platform is contained within the main PhoneGap git repository as a series of git submodules such as [phonegap-iphone](http://github.com/phonegap/phonegap-iphone), [phonegap-android](http://github.com/phonegap/phonegap-android), etc. This makes it all but impossible to install the latest and greatest without git. Being a git user myself, this does not pose any problem, and if you are not gitmotized yet, this is an ideal time to become so.  
  
Here are the series of steps I followed to create my own PhoneGap project...  
  
**Prerequisites**  

  
*   Install iPhone SDK (yes, you must join the iPhone developer program)
  
*   Install Android SDK ([http://www.talkandroid.com/android-sdk-install-guide/](http://www.talkandroid.com/android-sdk-install-guide/) has some good instructions. I am not using Eclipse, so I skipped all that)
  
*   Install Apache Ant (sudo port install apache-ant)
  

  
**Install PhoneGap**  

  
*   Get latest PhoneGap (git clone git://github.com/phonegap/phonegap.git)
  
*   Get submodules for iPhone & Android (cd phonegap && git submodule update)
  
*   Build iPhone Lib and install
  
*   Build Android libs
  

  
**Setting Up A New Multiplatform PhoneGap Project**  

  
*   Create a new iPhone project using the phonegap-iphone template. The www directory in the new project will be becoming the shared part of your project, with all your UI and application logic
  
*   Create the Android project using the phonegap-android build script. Use the www directory from the iphone project as the www-dir param. You will be replacing this with a reference to the git submodule
  
*   Create a new git repo in the www directory in the iPhone project, and commit all the files in the www directory
  
*   Change directories to the parent of where you want to put the directory for the shared git repo, then clone the repo located at /path/to/iphoneproj/www to /path/to/sharedrepo. You may also want to create a remote branch at this point for the new shared repo
  
*   Remove the www directory from the iPhone project
  
*   Create a new git repo in the iphone project directory, then commit all files. You may also want to create a remote branch at this point
  
*   Put the shared code into the iPhone project by using "git submodule add" to put a reference to the shared repo into /path/to/iphoneproj/www
  
*   Create a new git repo in the Android project directory, then commit all files. You may also want to create a remote branch at this point, as you probably did for the iPhone project files
  
*   Remove the /path/to/androidproj/assets/www directory from the Android project, and use "git submodule add" to put a reference to the shared repo at /path/to/androidproj/assets/www
  

  
You now should have 3 git repos, with the shared code, the iPhone specific project code, and the Android specific project code, each in their respective places. Much easier and nicer to work on.  
  
Anyhow, I hope this info is useful to any PhoneGap developers that want to get things setup cleanly for multi-platform mobile programming. Please let me know any feedback or improvements that people out there come up with, for this neat open source framework for doing JavaScript-based mobile development.