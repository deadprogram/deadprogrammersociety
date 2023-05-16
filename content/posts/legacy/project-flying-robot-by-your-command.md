---
title: 'Project Flying Robot: By Your Command'
date: 2009-03-10T13:52:00.000-07:00
draft: false
url: /2009/03/project-flying-robot-by-your-command.html
tags: 
- ruby
- flying robot
- ruby arduino development
- arduino
---

[![](http://paulsstarbasef22.homestead.com/files/Cylon_raider1.jpg)](http://paulsstarbasef22.homestead.com/files/Cylon_raider1.jpg)Our [flying\_robot](http://github.com/deadprogrammer/flying_robot/tree/master) project for Unmanned Aerial Vehicles has been underway for a few weeks now. Much soldering, and playing around with cool [Arduino](http://www.arduino.cc/) tricks has been taking place. You can read more [here](http://deadprogrammersociety.blogspot.com/2009/02/project-flying-robot-adventure-begins.html), [here](http://deadprogrammersociety.blogspot.com/2009/02/project-flying-robot-getting-all-xbee.html), [here](http://deadprogrammersociety.blogspot.com/2009/02/project-flying-robot-compass-two-motors.html), and [here](http://deadprogrammersociety.blogspot.com/2009/02/project-flying-robot-flying-dorkboard.html) if you need to catch up.  
  
One aspect that I have mentioned several times, but not gotten into much detail about, is our protocol for communicating with the UAV from the ground station. It is amazing to me, but there is still no dominant digital protocol for controlling UAV's. Many people are this using analog radio controllers, with some kind of sideband channel for autopilot commands.  
  
There are a few characteristics that seem essential to me for a proper ground control system design:  

*   A nice way to send control stick commands from a "virtual r/c" that can be used with any UAV
  
*   Consistent way to send autopilot commands
  
*   A way to be able to read the instruments remotely, and display them as part of your "control surface"

  
  
Another observation I have, is that there is every current Arduino UAV project has an entirely different code base. There also does not seem to be any practical way for these projects to share much, even though they are all targeting the same microcontroller.  
  
Certain characteristics seem essential for developing on-board UAV system programming, but are lacking in any of the projects I was able to find:  

*   A nice, modular way to put together the pieces you need in software that match the hardware configuration for that particular vehicle
  
*   A high-level domain specific language (DSL) to specify the UAV's behavior, and not just programming in C++ or assembly language
  
*   A consistent programming interface that corresponds to the protocol used by various ground controllers

  
  
With all of these design criteria in mind, I have been implementing the flying\_robot command parser and interface. Here is an example of the minimum code required to create a UAV using the current implementation:  
  
  
  
As you can tell, there is not all that much to it. The base for a UAV in 34 lines of code.  
  
The most current code for the actual "Rogue 1" LTA vehicle is being committed to [http://github.com/deadprogrammer/flying\_robot\_rogue\_one/tree/master](http://github.com/deadprogrammer/flying_robot_rogue_one/tree/master) if you want to follow along with our progress.  
  
Next post, we test the main thrusters and vectoring controllers, and nearly start a fire...