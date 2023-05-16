---
title: 'Project Flying Robot: Getting All XBee With It'
date: 2009-02-22T10:38:00.000-08:00
draft: false
url: /2009/02/project-flying-robot-getting-all-xbee.html
tags: 
- xbee
- zigbee
- flying robot
- wireless
- uav
- unmanned aerial vehicles
---

[![](http://4.bp.blogspot.com/_SgxaAaUGqzY/SaGtHgTCZeI/AAAAAAAABto/oQ4rSOtEeZs/s200/IMG_0609.JPG)](http://4.bp.blogspot.com/_SgxaAaUGqzY/SaGtHgTCZeI/AAAAAAAABto/oQ4rSOtEeZs/s1600-h/IMG_0609.JPG)We have been making some amazing progress on our flying\_robot project. This post is actually from almost a week ago, but I have not had time to catch up blogging with what we have been getting accomplished.  
  
As I had mentioned in my first posting, one of the reasons that we did not simply copy the [Blimpduino](http://diydrones.com/profiles/blog/show?id=705844%3ABlogPost%3A44817), is that we do not want to use a standard R/C controller for manual control. No, that would be too easy. Actually, it is because we have other kinds of ground control in mind... but I will get into that in future posts, once we have a working vehicle.  
  
One focus of our project is to create a fully digital protocol to communicate wirelessly with UAV's. Something like MIDI is to music, the flying\_robot command set is to flying. In other words, flying\_robot is intended to provide a device-independent way to communicate with various kinds of unmanned aerial vehicles. So we started looking at digital wireless solutions. WiFi is common, but does not have the range, plus it uses too much power. Bluetooth just lacks range, period. Sounds like a job for [XBee](http://www.digi.com/technology/rf-articles/wireless-zigbee.jsp) to me.  
  
If you have not heard of it, XBee is a wireless data standard that has several priorities: it must have good range, use very low power, and be very cheap. The internet of things will likely be connected via XBee, since it it ideal for low-cost devices that wish to communicate with each other.  
  
XBee modems come in several different flavors, depending on the needed range and desired type of network topology. The simplest version supports the 802.15.4 protocol, which is probably best for most point to point type applications, like a ground control to a base station. This is what they sometimes refer to as the "Series 1" modems.  
  
The ZigBee modems, also sometimes called Series 2, add a protocol for mesh networking that looks to be very interesting. It could be used for a swarm of robots that communicate with each other, not just with a base station. This appealed to my inner geek, and so I ordered two of these modems, with the intention of experimenting with mesh networking in the near future.  
  
On that note, there is an [amazing deal right now for experimenters directly from Digi](http://www.digi.com/products/wireless/point-multipoint/xbee-pro-868.jsp). You can get a development kit for the super-powerful next-generation XBee 868, that includes a pair of the modems, for only $99. I could not resist, and just ordered a pair of these to play around with, as well as the [XBee-Pro 2.5's I already had acquired from SparkFun](http://www.sparkfun.com/commerce/product_info.php?products_id=8768).  
  
One thing I discovered quickly, was that the XBee modems I had purchased are really small. The next, was that I had to do some additional programming on them, before they would talk to each other. I found a [useful Ruby script for configuring XBee modems](http://github.com/madrona/xbee-modem-setup/tree/master) from madrona, but it turned out to be a little more complicated, due to my choice of ZigBee over the simpler 802.15.4 protocol.  
  
Fortunately, others have already been blazing this wireless trail, so I found [these recent instructions](http://antipastohw.blogspot.com/2009/01/xbee-shield-to-xbee-shield.html) on the Liquidware blog. It turns out that when dealing with ZigBee, one of the modems needs to be designated the "coordinator" for all the others in that mesh network, to hand out the all-important MY addresses. The coordinator needs different firmware than the individual nodes, which requires a utility provided by Digi, which is Windows only. Without this firmware on one of the modems in your mesh, you can send as many AT command as you like, the modems will never talk to each other. I dusted off a VM, and installed the Digi utility. Once I had updated the firmware, and updated the configurations of each modem using madrona's script, I was ready to go.  
  
With one XBee modem plugged into my Mac via the USB port thanks to the [XBee Explorer](http://www.sparkfun.com/commerce/product_info.php?products_id=8687) adapter, and the other plugged into the Arduino via the [XBee Shield](http://www.sparkfun.com/commerce/product_info.php?products_id=8471) from Sparkfun, serial communication "just worked". Now I was ready to start coding on the Arduino itself... but that is another story.