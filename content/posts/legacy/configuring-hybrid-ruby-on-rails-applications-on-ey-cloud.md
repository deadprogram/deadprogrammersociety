---
title: 'Configuring Hybrid Ruby on Rails Applications On EY-Cloud'
date: 2010-03-04T10:30:00.000-08:00
draft: false
url: /2010/03/configuring-hybrid-ruby-on-rails.html
tags: 
- ec2
- ruby
- ey-cloud
- ruby on rails
- engine yard
---

This last weekend, we completed migration of a slightly more complex Ruby on Rails application than the usual to [Engine Yard's EY-Cloud](http://www.engineyard.com/products/cloud/features). It took a few tries, and a tiny bit of research, before we completely understood what to do to get it up and running with all of the needed capabilities. Naturally this was due to gaps in my own knowledge, and I wanted to post about what I had learned, and how awesome EY-Cloud really is!  
  
If you do not know about it, EY-Cloud is Engine Yard's cloud platform that is based on [Amazon's EC2](http://aws.amazon.com/ec2/). Readers of this blog know I am not afraid to [get hardcore when it comes to EC2 server configurations](http://deadprogrammersociety.blogspot.com/search/label/ec2), and with EY-Cloud I feel like I can now get the best of everything. But I am getting ahead of myself.  
  
Let me briefly describe the architecture of the application I was migrating. The main application is written in Ruby on Rails and uses MySQL as its data store. The app provides UI and an API for interactions with the application, mostly called by a [custom iPhone app written using PhoneGap](http://phonegap.com). The main app is secured using an SSL certificate. In addition, a separate API for a specific high-performance capability is written using Sinatra and DataMapper. This "special API" is also secured via SSL.  
  
OK, you got that? Perhaps not, so here is a diagram to illustrate what I am talking about:  
  
[![](http://www.gliffy.com/pubdoc/2008066/M.png)](http://www.gliffy.com/pubdoc/2008066/M.png)  
  
We call this kind of application a "hybrid" application, meaning that it is built using Ruby on Rails + "something else". For this app, the "something else" is Sinatra + DataMapper.  
  
The previous installation used the same basic setup, but was created manually using hand-configured EC2 instances. This required a lot more management to keep the application going, and especially to add or remove instances to the cluster. Backing up the entire configuration by creating custom AMI's was also very labor intensive.  
  
This was the scenario that led us to wish to migrate the app from raw EC2 to EY-Cloud. So if you are planning to set something like this up yourself, here are my notes to share my experience migrating a hybrid Ruby on Rails application to EY-Cloud.  
  
**Prerequisites**  
You need to have an account setup with Engine Yard for EY-Cloud. In addition, you should have installed the Elasticfox plugin for Firefox to easily administer the security groups. You can also do this via the command line, but it is a lot more effort.  
  
**Configure Main Environment & Application**  
Configuring your main application for EY-Cloud is a pretty simple process. It basically requires setting up private key access to the git repository and the application settings using the web based interface that Engine Yard provides. There is a complete [article that describes this in detail here](https://cloud-support.engineyard.com/faqs/overview/getting-started-with-engine-yard-cloud). The main steps are:  

  
*   Create main environment
  
*   Create main application and configure access to its git repo
  
*   Config ssh key you will use to connect to instances
  
*   Add ssl certificate, and config main app to use it
  
*   Config any needed gems and unix packages to be used by main app
  
*   Launch app server and separate database server in main environment
  

  
**Configure Secondary Environment & Application**  
Now you are ready to configure the environment and application for the other public accessible SSL protected service that is part of the application. This needs to be a secondary application because EY-Cloud currently only allows a single SSL cert per environment, and only allows you to associate it with one application. Hence needing a second environment configured. The main steps are:  

  
*   Create specialapi environment
  
*   Create specialapi application and configure access to its git repo
  
*   Config ssh key you will use to connect to specialapi instances
  
*   Add ssl certificate, and config specialapi app to use it
  
*   Config any needed gems and unix packages to be used by specialapi app
  
*   Launch specialapi app in specialapi environment. No database is necessary.
  
*   Copy contents of database.yml from /data/mainapp/shared/config/database.yml on "main app" server to /data/specialapi/shared/config/database.yml on "specialapi" server. Yes, you will need to use SSH to login to both servers.  
    
*   Use keep file on the database.yml location on the specialapi environment to point to the master database in the main app environment. [This page explains about keep files](https://cloud-support.engineyard.com/faqs/questions/making-changes-to-nginx-apache-or-monit-configs-with-keep-files).
  

  
**EC2 Security Configuration**  
In order to allow the secondary environment to get access to the database located in the main environment, you need to make a small but critical change to the configuration in the EC2 Security Groups. Otherwise the internal firewall at Amazon will not allow the application to access the database. It is very easy to configure this using Elasticfox. Here is how:  

  
*   Setup your EC2 security credentials for your EY-cloud account. You can download them as part of the ey-cloud.yml file
  
*   Once you are connected to that account using elasticfox, click on the "Security Groups" tab. You should see 3 security groups "default", one for the main app named something similar to "ey-myapp\_production-12341234" that refers to the main environment, and another one named something like "ey-secondaryapp\_production-56785678" that refers to the secondary environment
  
*   Click on the "ey-myapp\_production-12341234" group in the left pane labeled "Your Groups" then click on the green checkmark icon at the top of the "Group Permissions" pane. This will bring up the "Add New Permission For Security Group" dialog. Click on the "Group" tab, then choose the "ey-secondaryapp\_production-56785678" group from the Groups dropdown, and click on the "Add" button. Your secondary environment should now be able to access the main environment's database
  

  
**Conclusion**  
It is pretty great to be able to take advantage of both the cool management interface and scalable clustered database and application stack, as well as being able to get down and dirty via SSH, something you really do need in order to configure more complex hybrid Ruby on Rails applications. EY-Cloud provides this kind of capability, and is certainly a lot easier than managing it all yourself. Hopefully, these notes will make it easier for you to migrate your own complex application. Please let me know how it works for you.