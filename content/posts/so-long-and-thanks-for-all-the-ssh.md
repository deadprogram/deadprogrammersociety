---
title: 'So Long, And Thanks For All The SSH'
date: 2009-02-25T09:38:00.000-08:00
draft: false
url: /2009/02/so-long-and-thanks-for-all-ssh.html
tags: 
- open source development
- capistrano
- ruby on rails
---

[![](http://www.stevenkontos.com/images/dolphins_at_sunset.JPG)](http://www.stevenkontos.com/images/dolphins_at_sunset.JPG)I read [Jamis Buck's posting](http://weblog.jamisbuck.org/2009/2/25/net-ssh-capistrano-and-saying-goodbye) late last night, about how he was retiring from involvement with [Capistrano](http://www.capify.org/), [Net:SSH](http://net-ssh.rubyforge.org/) and a few other closely related projects. First of all, the community owes him a lot for doing so much work on these crucial parts of the [Ruby on Rails](http://rubyonrails.org/) ecosystem.  
  
Seems like he has fallen victim to his own project's popularity. So many people using your code, and they start to expect things, and then demand them. I have seen friends in the Ruby community who are committers on a very popular tool, pretty much accosted at a conference, by fervent users of their project, who proceed to drag them off to the side to show them some obscure edge case. And like any good public servant, they go off to see whatever it is, regardless of whatever they were planning on doing the moment before.  
  
Jamis was for sure getting burned out. I know that from personal experience, when programming pal [Ari Lerner](http://blog.xnot.org/) and I worked [some patches for Net:SSH](http://github.com/jamis/net-ssh/commit/1e2834380e383fdada2ddf2c907c9b449b463181) that solved a [longstanding problem for public key authentication](http://groups.google.com/group/capistrano/browse_thread/thread/1102208ff925d18). Our first discovery on cloning the repo was that the original commit did not actually pass all of the unit tests. Then once we had corrected both that, and the original issue, and we contacted Jamis, he was pretty ambivalent. I am not knocking him here. Eventually, he accepted the patches. I think it was more that he had just had it with being a slave to his own creation.  
  
Now we are on own, people. However, there does need to be some organization to the community. [Github](http://github.com) allows anyone to fork a project, sure. But having 25 different versions of the same project wandering around is too confusing for most people. New users would not know which version to install, the beauty of the standardization would be lost.  
  
Jamis, you need to pick a successor to inherit the main responsibility for these projects, if for no other reason than this. Anyhow, we thank you again for all your efforts, and we look forward to seeing what you get into next.