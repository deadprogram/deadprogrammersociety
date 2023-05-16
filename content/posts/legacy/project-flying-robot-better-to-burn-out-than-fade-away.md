---
title: 'Project Flying Robot: Better To Burn Out Than Fade Away?'
date: 2009-03-15T17:57:00.000-07:00
draft: false
url: /2009/03/project-flying-robot-better-to-burn-out.html
tags: 
- flying robot
- los angeles rubyconf
- ruby arduino development
- uav
- unmanned aerial vehicles
- arduino
- rad
---

[![](http://www.wired.com/images/article/full/2008/04/hindenburg_500px.jpg)](http://www.wired.com/images/article/full/2008/04/hindenburg_500px.jpg)We had [made](http://deadprogrammersociety.blogspot.com/2009/02/project-flying-robot-adventure-begins.html) [incredible](http://deadprogrammersociety.blogspot.com/2009/02/project-flying-robot-getting-all-xbee.html) [strides](http://deadprogrammersociety.blogspot.com/2009/02/project-flying-robot-compass-two-motors.html) [forward](http://deadprogrammersociety.blogspot.com/2009/02/project-flying-robot-flying-dorkboard.html) in our [construction](http://deadprogrammersociety.blogspot.com/2009/03/project-flying-robot-by-your-command.html) of ["Rogue 1"](http://github.com/deadprogrammer/flying_robot_rogue_one/tree/master) our autonomous blimp that we are building as the first implementation of [flying\_robot](http://github.com/deadprogrammer/flying_robot_rogue_one/tree/master), our [Arduino](http://www.arduino.cc)\-framework for Unmanned Aerial Vehicles based on top of [Ruby Arduino Development (RAD)](http://rad.rubyforge.org/). We are also heavily influenced by the cool [Blimpduino](http://diydrones.com/profiles/blog/show?id=705844%3ABlogPost%3A44817) project. We were finally ready for a live test... or so we thought. We inflated our envelope, and [my brother](http://myfirstairship.blogspot.com/) attached the gondola that he has been carefully constructing.  
  
We had already done some testing of the software/hardware, so we were heady with our previous successes. "Let 'er rip," said Damen. Next thing you know, the blimp was careening about, as the motors pulsed wildly out of control, then stopped abruptly. "That is not a good sign from an electric motor controller, " said my brother glumly.  
  
We peeled the gondola off the envelope, and disassembled the components that had been connected so carefully, and yet not carefully enough. Multimeter in hand, Damen carefully traced each connection looking for power as I entered the commands into the serial interface.  
  
Finally, after a few moments we looked at each other. There was one more test... we rewired everything properly, but using the spare [Pololu Micro Dual Serial Controller](http://www.pololu.com/catalog/product/410) and a breadboard. I entered the commands and the motors powered up. Now there was only one conclusion: we had fried our costly little Pololu.  
  
Ouch! After spending a while on post-mortem analysis of our dead little bird, Damen muttered something about power. "Huh?" I looked up from debugging the Arduino code for the differential thrust calculations.  
  
"Power. We need less power."  
  
"Less power? I thought the specs said that controller was rated for more than our LiPo battery and more?"  
  
"Specs lie."  
  
I had to acknowledge the simple truth of that statement, especially given the obviously dead chip. With a lot more knowledge about our bimps power requirements, learned the hard way, Damen began planning the third iteration of our main board wiring, with a new extra power regulator. And an external kill switch.