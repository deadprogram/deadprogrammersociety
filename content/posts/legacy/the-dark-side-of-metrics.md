---
title: 'The Dark Side Of Metrics'
date: 2006-11-13T20:41:00.000-08:00
draft: false
url: /2006/11/dark-side-of-metrics.html
tags: 
- software metrics
- agile development
---

I have usually been in favor of measurement of any possible aspect of the software development process. Proper techniques of gathering and analyzing metrics have been espoused since [Capers Jones](http://www.unt.edu/isrc/Faculty/FacultyFellows/jones.htm) created the study of software measurement. I was first introduced to many of these concepts in the writings of Steve McConnell, particularly when his book [Rapid Development](http://www.amazon.com/exec/obidos/ISBN=1556159005/stevemcconnelconA/) first came out. If a thing cannot be measured, it cannot be easily studied or improved.  

But any tool, no matter how well intentioned its purpose, can be used for ill. Any system that relies entirely on user entered information can by lied to. Such systems can be gamed, for various purposes. In a very political environment, a rogue group can manipulate their own metrics to gain power over other groups, gain budget, or simply steer the company in the direction of their own egos. Sometimes metrics can be used to hide something important. "But look at our metrics," protests the manager in charge of a spectacular failure.  

Even worse, once this starts to happen, the "everybody's doing it" syndrome strikes, and it can spread like a disease. Pity the poor foolish team that actually tries to tell the truth within such a system once this dynamic sets in. They will be punished, sometimes severely, for "not measuring up to the standards of the company".

The best sorts of metrics are collected automatically. All sorts of interesting information can be learned from analysis of the source code repository. Other information can be assessed from other dynamic sources such as number of unit tests passed, or [Fitnesse](http://fitnesse.org/) tests, or measuring [Running Tested Features](http://www.xprogramming.com/xpmag/jatRtsMetric.htm). The important thing is that it is a lot more reliable to use metrics that are not so easily fooled by people with various agendas.