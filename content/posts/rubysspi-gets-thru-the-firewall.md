---
title: 'RubySSPI Gets Thru The Firewall'
date: 2006-12-01T11:00:00.000-08:00
draft: false
url: /2006/12/rubysspi-gets-thru-firewall.html
tags: 
- ruby
---

[![](http://www.rift.com/~sacha/pictures/web/checkpoint.jpg)](http://www.rift.com/~sacha/pictures/web/checkpoint.jpg)One of the biggest problem that Guerilla Rubyists have had getting our favorite language into the big companies that pay our bills, has been the corporate firewall. Using corporate Windows machines, behind corporate firewalls that use NTLM authentication to the corporate domain, has meant "no Ruby programmatic access to resources on the other side of the firewall." In other words, no RubyGems! Having to try to download every Gem (and every Gem that the Gem you want to install depends on) for a local install it at the very least a big pain in the behind. I have been feeling this pain for a couple of years now!  
  
Recently Justin Bailey released a Gem called [RubySSPI](http://rubyforge.org/projects/rubysspi/) that patches the Net::HTTP class to support NTLM authentication. I was excited! I manually downloaded and installed it...but it did not work for me. Others had successfully used it, however, so I did not give up so easily.  
  
I have been working with Justin Bailey to help him figure out why it was not working in our typical huge corporate environment, and we have achieved success! I was just able to download a Gem in the "normal" way. I'm sure he will uploading an updated version of the Gem soon...Thank you, Justin!