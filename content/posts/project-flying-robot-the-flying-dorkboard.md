---
title: 'Project Flying Robot: The Flying Dorkboard'
date: 2009-02-28T08:53:00.000-08:00
draft: false
url: /2009/02/project-flying-robot-flying-dorkboard.html
tags: 
- dorkboard
- flying robot
- ruby arduino development
- arduino
---

[![](http://3.bp.blogspot.com/_2iIswAD6O1U/SaRAXOWcBSI/AAAAAAAAAAw/t2qntX2W2lA/s320/Pictures+122.jpg)](http://3.bp.blogspot.com/_2iIswAD6O1U/SaRAXOWcBSI/AAAAAAAAAAw/t2qntX2W2lA/s320/Pictures+122.jpg)As we proceeded along with our [flying\_robot](http://github.com/deadprogrammer/flying_robot/tree/master) project, one thing became abundantly clear: weight matters. The [Arduino Diecimilla](http://www.arduino.cc/en/Main/ArduinoBoardDiecimila) that we had been using up to this point, although a fine package for beginners, was just not going to make it when it came time to weigh in. Yes, there is the [Arduino Nano](http://www.arduino.cc/en/Main/ArduinoBoardNano), but it is not a cheap device. Also, it has a few options that were not important to us, like the integrated USB, since we planned on only using [XBee](http://www.digi.com/technology/wireless/products.jsp) based communication with the blimp.  
  
I had been doing some research, and have learned a lot more about this whole Arduino ecosystem. There is incredible work being done by people like [ladyada](http://www.ladyada.net/), and many others too numerous to list here. There are many variations on the Arduino, like the [Boarduino](http://www.ladyada.net/make/boarduino/), [Sanguino](http://www.wulfden.org/TheShoppe/freeduino/sanguino.shtml), and so many others.  
  
However, one option in particular caught my attention, called the [Dorkboard](http://dorkbotpdx.org/wiki/dorkboard). This thing is small, I mean tiny. Especially considering that it does not use the surface mount version of the ATMega microcontroller. And it has almost nothing on the board itself. You need to provide both power, and an interface to communicate with it, in our case, using the XBee modems.  
  
This highly stripped down, minimalist approach was exactly what we had been looking for! Cheap, simple, light, and having everything that one needs from any Arduino/Freeduino platform. I ordered a few of the kits, and they were shipped from [Wulfden](http://www.wulfden.org/TheShoppe/products.shtml) just a few days later.  
  
Once they came in, my brother was eager to get right into one. I dropped off the package, and he had soldered up one, plus the power supply, in less then an hour. We had the [USB-BUB](http://wulfden.org/TheShoppe/pa/index.shtml) interface, so we just plugged it in. Once we had all the cable pinout correct, and we had downloaded the "hello, LED" code from [RAD](http://rad.rubyforge.org/), we were watching it flash under our command.  
  
The brain of our flying robot was ready! Now we needed a way to communicate with it, and update its code, all wirelessly. The next step, would be building an XBee breakout board, and doing some XBee hardware/firmware hacking...