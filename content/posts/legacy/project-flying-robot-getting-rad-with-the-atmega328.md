---
title: 'Project Flying Robot: Getting RAD With The ATMega328'
date: 2009-04-18T15:08:00.000-07:00
draft: false
url: /2009/04/project-flying-robot-getting-rad-with.html
tags: 
- flying robot
- ruby arduino development
- arduino
---

[![](http://cache.jalopnik.com/assets/resources/2008/04/wind-tunnel.jpg)](http://cache.jalopnik.com/assets/resources/2008/04/wind-tunnel.jpg)I have been wanting to upgrade the hardware used in our [Dorkboards](http://dorkbotpdx.org/wiki/dorkboard) for [flying\_robot](http://flyingrobo.com), from the ATMega168, to the newer better faster ATMega328. More memory, and a faster UART for serial communications with the XBee modems in the same pinout = easy win. Thanks to a quick shipping turnaround from [@adafruit](http://www.adafruit.com) I got them in before the weekend, so I could play a little bit today.  
  
The first step was to upgrade my hard-working Arduino Diecimila to a 328. I now have it working great with [Ruby Arduino Development (RAD)](http://rad.rubyforge.org/), but since RAD was really setup for Arduino 12, I had to make a couple changes. Here is what I did:  
  
1\. D/l and install [Arduino 15](http://arduino.cc/en/Main/Software) (brave, I know, since that is the latest release, and many people run one version down from the latest)  
2\. Change my hardware.yml entry  
```
mcu: atmega328p
```  
3\. Change my software.yml entry  
```
arduino\_root: /Applications/arduino-0015
```  
4\. Lastly, since the ATMega328 bootloader runs at a faster rate, I had to tweak the RAD code itself to support it. The file "/vendors/rad/generators/makefile/makefile.erb" is the template used to create the makefile that compiles and uploads the code to the Arduino. Line 77 in that file controls the baud rate, which needs to be set like this for the '328:  
```
UPLOAD\_RATE = 57600
```  
  
Once I had done this, I was easily and quickly able to recompile/re-upload the latest flying\_robot code to my test board. Yeah! Hopefully tomorrow I can upgrade [Rogue 1](http://github.com/deadprogrammer/flying_robot_rogue_one/tree/master) and try a flight at the new, higher communication speed.