---
title: 'Recaptcha On Rails'
date: 2008-02-01T14:54:00.000-08:00
draft: false
url: /2008/02/recaptcha-on-rails.html
tags: 
- ruby
- recaptcha
- ruby on rails
---

[![](http://www.uncg.edu/rom/courses/campo/511/RosettaStone3.jpg)](http://www.uncg.edu/rom/courses/campo/511/RosettaStone3.jpg)UPDATED Oct. 15, 2009 with most current info  
  
I hate implementing captchas. You know, those annoying things that your users think are deciphering hieroglyphics. I have hated them because I do not want to install a whole massive assemblage of software like ImageMagick/RMagick just to provide some basic protection from spam and bots.  
  
To avoid this, I had hacked together a simple implementation using some free public captcha. However, a client recently turned on SSL on their signup page, and my free public captcha gave a nasty error cause of the domain name in the SSL certificate not matching the domain of their site. How cheap!  
  
I needed a new solution. I waded thru pages of search results with the dreaded RMagick sotuions. But then, lo and behold, I discovered there is a fantastic simple [plugin for Ruby on Rails from Ambethia](http://ambethia.com/recaptcha/) that supports the marvelous [Recaptcha](http://recaptcha.net/).  
  
Recaptcha is a really neat project that uses crowdsourcing to implement a form of human OCR on old books that defy machine OCR. They need human scanners, and we need proof that the people signing up on the site are human. Perfect match!  
  
Less than 10 minutes later I had the plugin installed, implemented, and deployed in production. It is that easy. Here is a four step process that will have you up in moments:  
  
Step 1 - Install the Recaptcha plugin  
`  
script/plugin install git://github.com/ambethia/recaptcha.git  
`  
'Nuff said.  
  
Step 2 - Set Your Recaptcha Account Data in Rails  
OK, so I lied. You need to tell the plugin what your account info is, and if you do not yet have a free Recaptcha account, you will need to sign up for one. Once you do, save your keys into config/initializers/recaptcha.rb  
`  
ENV['RECAPTCHA_PUBLIC_KEY'] = 'youractualpublickey'  
ENV['RECAPTCHA_PRIVATE_KEY'] = 'youractualprivatekey'  
`  
  
Step 3 - Display The Recaptcha Widget In Your View  
You will need to display the Recaptcha widget somewhere. In my case, it was the signup page for the site. Just put this view helper where you want the widget to appear:  
`  
<%= recaptcha_tags %>  
`  
If you are using SSL, use this instead:  
`  
<%= recaptcha_tags :ssl => true %>  
`  
  
Step 4 - Validate The Recaptcha  
You need to make sure that the user entered the proper values for the Recaptcha. Just add this to the controller action that the view submits to:  
  
  
If you want to display any Recaptcha errors right along with any model errors of the model you are trying to control adding using the Recaptcha, you could do this instead:  
  
  
  
You may have guessed by now that it took me longer to write this posting than to implement Recaptcha using the Ambethia plugin. Hey, that is just the kind of guy I am. It was just so cool, and such a quick solution to a common problem, that I couldn't help myself.  
  
Let the digitizing begin!