---
title: 'Everybody Into The Pool'
date: 2008-02-20T11:18:00.000-08:00
draft: false
url: /2008/02/everybody-into-pool.html
tags: 
- sinatra
- ec2
- ruby
- s3
- grid computing
---

A few weeks back, I indulged my current obsession with grid computing, and [Amazon's EC2](http://aws.amazon.com/ec2) and S3 services in particular, with a [lengthy post](http://deadprogrammersociety.blogspot.com/2008/01/on-grid-with-ec2.html). I mentioned how friend [Ari Lerner](http://blog.xnot.org/) and I had built a really neat solution, and were going to put all of our processing farm goodness into a nice neat gemified package. Well, mostly thanks to Ari, we now have a new Ruby gem called [ProcessorPool](http://rubyforge.org/projects/processorpool/) that uses EC2 and S3 to do all the hard work for you.  
  
Based on [Sinatra](http://sinatra.rubyforge.org/), with a bunch of S3 goodness mixed in, the ProcessorPool gem makes it staggeringly easy to exploit the power of the EC2 grid. More info about it is available at the [Blog @ CitrusByte](http://blog.citrusbyte.com/2008/2/20/effortlessly-farm-work-to-an-ec2-instance-without-batting-an-eye), and you can also check it out on RubyForge [here](http://rubyforge.org/projects/processorpool/).  
  
All kinds of fun applications await you in the pool... image processing, video/audio transcoding, heavy computational stuff, long crawls of content... and it is fun to delegate to a pool of worker machines in the EC2 cloud.  
  
Come on in... the pool is fine.