---
title: 'Frankie Goes To Facebook'
date: 2008-04-08T22:04:00.000-07:00
draft: false
url: /2008/04/frankie-goes-to-facebook.html
tags: 
- sinatra
- ruby
- frankie
- facebooker
- facebook
---

**UPDATED 4/12/2008: Now compatible with Sinatra 0.2.0**  
So you want to create a small Facebook application... seems like it should be a small thing, right? But creating an entire Ruby on Rails application just for a tiny little Facebook application is, at the very least, a bit wasteful. In the case of a overly popular Facebook app you could end up with, as Marc Andreessen put it, a ["self-inflicted denial of service attack"](http://blog.pmarca.com/2007/06/analyzing_the_f.html), unless you have both a pretty serious infrastructure to support it, as well as lots of cash to keep that data center running.  
  
Wouldn't you rather be able to create a highly scalable "hello, world" Facebook application in around 13 lines of Ruby code? Say hello to [Frankie](http://facethesinatra.com):  
  
```
require 'rubygems'  
require 'frankie'  
  
configure do  
  set\_option :sessions, true  
  load\_facebook\_config "./config/facebooker.yml", Sinatra.env  
end  
  
#\# facebooker helpers  
before do  
  ensure\_authenticated\_to\_facebook  
  ensure\_application\_is\_installed\_by\_facebook\_user  
end  
  
#\# the site  
get '/' do  
  body "<h1>Hello #{session\['facebook\_session'\].user.name} and welcome to frankie!</h1>"  
end  

```  
  
Frankie is a plugin for the minimalist and very fast [Sinatra web framework](http://sinatrarb.com/) that allows you to easily create a Facebook application by using the [Facebooker](http://facebooker.rubyforge.org/) gem. Why would you want to use it? If your Facebook application needs to be highly scalable, is fairly small, or is really a mashup of other web-available resources, than Frankie could be a good solution.  
  
Frankie is available now for your enjoyment. Here is how to get started:  
  
\- Install the Frankie gem, which will install the Sinatra and Facebooker gems if you do not already have them.  
```
sudo gem install frankie
```  
  
\- Create the application directories for your new app:  
```
mkdir myapp  
cd myapp  
mkdir config
```  
  
\- Put your facebooker.yml file into the /myapp/config directory, and set the values to your information. Here is a simple example of the file:  
```
  
\-------  
development:  
 api\_key: apikeyhere   
 secret\_key: secretkeyhere  
 canvas\_page\_name: yourcanvashere      
 callback\_url: http://localhost:4567  
test:  
 api\_key: apikeyhere   
 secret\_key: secretkeyhere  
 canvas\_page\_name: yourcanvashere      
 callback\_url: http://localhost:4567  
production:  
 api\_key: apikeyhere   
 secret\_key: secretkeyhere  
 canvas\_page\_name: yourcanvashere      
 callback\_url: http://yourrealserver.com  

```  
  
\- Make sure you have setup your facebook application on the facebook site. Google "setup new facebook application" if you are unsure how to do this. I recommend starting with an IFrame application, so that you can point a development version of your Facebook application to your local machine. This, like our example here, would use "http://localhost:4567" as the callback URL when configuring the Facebook app.  
  
\- Create your application, based on the sample above, and run it:  
```
ruby sample.rb
```  
  
This will start the Sinatra Ruby web server running:  
```
\== Sinatra has taken the stage on port 4567!
```  
  
\- Test it by pointing your browser to http://apps.facebook.com/yourappname. If you have things setup correctly then you should see your application appear inside of Facebook's site.  
  
Facebook is now your playground... have fun with [Frankie](http://facethesinatra.com)!