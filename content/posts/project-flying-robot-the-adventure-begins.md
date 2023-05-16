---
title: 'Project Flying Robot: The Adventure Begins'
date: 2009-02-18T08:22:00.000-08:00
draft: false
url: /2009/02/project-flying-robot-adventure-begins.html
tags: 
- ruby
- flying robot
- ruby arduino development
- uav
- unmanned aerial vehicles
- arduino
- rad
---

[![](http://www.johnnysokkoandhisflyingrobot.com/johnnysokkoandhisflyingrobot.jpg)](http://www.johnnysokkoandhisflyingrobot.com/johnnysokkoandhisflyingrobot.jpg)I love robots. OK, there, I've gone and gotten that out into the open. Like many programmers, I have long dreamed of dominating the world with my robot legions. Or failing that, at least getting my [RoboSapien](http://en.wikipedia.org/wiki/RoboSapien) to walk around in a little circle by itself.  
  
Recently, my brother [Damen Evans](http://myfirstairship.blogspot.com/) and I decided that we needed to realize our ambitions, and began work on a flying robot. Yes, that is what I said. **Flying robot**. After many years of respective obsessions about Lighter Than Air (LTA) vehicles and autonomous control, we are combining our forces and actually building something.  
  
The "Rogue 1", as we are calling the airship, is heavily influenced (pun only, hopefully) by the very cool [Blimpduino](http://diydrones.com/profiles/blog/show?id=705844%3ABlogPost%3A44817) project. It will be controlled by an [Arduino](http://www.arduino.cc/) based system, like the Blimpduino. However, our focus is a bit different, which is why we are building our own hardware design, although also based on the open source Arduino hardware platform.  
  
One major concept that we are working on, is creating a digital protocol for controlling the airship from a ground station. Where the Blimpduino uses a standard radio control setup, we are creating a fully digital protocol for Unmanned Aerial Vehicles (UAV) similar to what MIDI does for music. For example, an LTA vehicle would have a different way to perform a command like "rudder left 10 degrees" than an airplane or helicopter would. Especially since neither an LTA nor a helicopter even have rudders!  
  
We have decided to use the [Ruby Arduino Development](http://rad.rubyforge.org/) (RAD) project for creating the software needed for [flying\_robot](http://github.com/deadprogrammer/flying_robot/tree/master). It is still a bit rough in some ways, but it allows us to take advantage of a slick Ruby DSL-like approach for implementing the flying\_robot command set for a specific UAV, as well as for integrating a bunch of the hardware we will be needing, like motors and sensors.  
  
As the many small parts come in, both Damen and I will be blogging about the fun, so watch the skies... they're already here!