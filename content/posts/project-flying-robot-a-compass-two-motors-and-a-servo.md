---
title: 'Project Flying Robot: A Compass, Two Motors, And A Servo'
date: 2009-02-26T11:01:00.000-08:00
draft: false
url: /2009/02/project-flying-robot-compass-two-motors.html
tags: 
- pololu
- flying robot
- digital compass
- instruments
- uav
- unmanned aerial vehicles
- arduino
- hmc6352
---

[![](http://4.bp.blogspot.com/_SgxaAaUGqzY/SagUfS1A_dI/AAAAAAAABtw/eEnnwwY4kQc/s200/IMG_0644.JPG)](http://4.bp.blogspot.com/_SgxaAaUGqzY/SagUfS1A_dI/AAAAAAAABtw/eEnnwwY4kQc/s1600-h/IMG_0644.JPG)Last weekend was a fantastic hardware/software jam session with [my brother Damen](http://myfirstairship.blogspot.com/), working on our autonomous [Ruby Arduino Development (RAD)](http://rad.rubyforge.org/) powered blimp. Lots of little pieces had been coming in the mail, my brother had been soldering, and I had been programming away. Both of us were eager to start putting it all together.  
  
The first item of business was getting our bearings. We had acquired from Sparkfun a very cool [HMC6352 digital compass](http://www.sparkfun.com/commerce/product_info.php?products_id=7915) module. Based on the Honeywell chip, this tiny but powerful breakout board is a very easy device to use with [Arduino](http://www.arduino.cc/), thanks to supporting the i2c protocol, also known as "two-wire interface" or TWI. No one had created a RAD plugin yet for this device, so I had whipped one together a couple days earlier using some Arduino code I found online, combining with the techniques used in some of the examples in RAD. Now, finally I would get a chance to see if it would work.  
  
We plugged in the unit to our handy breadboarding setup, downloaded the code to the Arduino via USB cable, and viola! Amazingly, it worked perfectly the first time... we were able to obtain the heading, and turning around the unit resulted in the compass data updating correctly. Naturally, we started to get a little excited.  
  
Of course, things would get a little bit trickier with our next item for integration: the [Pololu Micro Dual Serial Controller](http://www.pololu.com/catalog/product/410). The pricey but useful Pololu chip allows for extremely simple serial command of 2 DC motors. Why would we want to do this, when we already have the Arduino itself? The ease of commanding a separate device that handles monitoring and setting the motor speeds, allows us to focus on the important parts of our application: integrating it all together. Plus, there is only so much processing power available in the ATMega microcontroller, so offloading that part of the work to the separate Pololu microcontroller frees up our Arduino to process more sensor inputs, and also do other interesting things we have planned.  
  
Since the Pololu is a serial device, we used the Arduino's AFSoftSerial library to communicate with it. The soft serial library allows you to use any 2 of the Arduino's digital pins as a serial interface. Support is already in RAD for this library. With some more Google searching, and some assistance from the Pololu forums, I had written another RAD plugin. A few moments for Damen to wire things up, and we were ready for our test. We had only wired up one motor, and we had used the Arduino's own power to power both the Pololu's logic chip, as well as the motor. That would turn out to not be a very good idea.  
  
The Pololu works by sending it simple serial commands. You tell it which of the two motors, which direction, and what speed to set it to. We fired things up set our motor to "forward speed 10" and it started to move. Glorious! So, overwhelmed with enthusiasm, we decided to try "20". Much to our surprise, setting the speed to 20 caused the motor to stop entirely. Say what? We looked at each other blankly.  
  
You simply cannot power both the Arduino, and the motors, from the same power, unless you do some additional circuitry to provide both the higher voltage that the motors want, along with the 5V that the Arduino desires. Once we had thought about it for a few moments, it seemed obvious. We switched the motor supply to a separate battery, and the motor performed at 20. "Let's try full power", I said, and with a nod from my brother, I boosted the power to maximum. "Hey!" we both exclaimed at once a second later, as Damen grabbed for the now flying motor, which was trying it's best to lift the breadboard up by its power leads, and I frantically typed the commands that would shut down the motor. I wish we had THAT on video!  
  
We then decided to keep going, and integrate our servo. The servo is used to change the vector of the thrust motors, a design that is also used by the [Blimpduino](http://diydrones.com/profiles/blogs/blimpduino-home-page). Unlike the main thrusters, we are just using the Arduino itself to control the servo motor, using one of the digital pins. It is really easy to use the servo library to move a servo to a particular position. In this case, no new plugin for RAD was required, cause others have already figured it all our for us. Which is nice.  
  
We made the same mistake of connecting our servo to the same battery as the Arduino itself, due to the fact that the servo wanted the same voltage. By this point in the day, the poor thing just didn't have the force left in it. This caused the very odd side effect of resetting the Arduino itself when the servo would be ordered to move. We only realized that was what it was, once we tried getting power from the USB port. We had been testing using our wireless [XBee](http://www.digi.com/technology/wireless/products.jsp) modems. Once the power problem was solved, the servo did exactly what we told it.  
  
It was a tremendous session, and we were now very satisfied that this project was, ahem, going to fly.