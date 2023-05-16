---
title: 'LARubyConf 2009 - Dan Yoder - "Resource Oriented Architectures and Why It Matters"'
date: 2009-04-05T08:35:00.000-07:00
draft: false
url: /2009/04/larubyconf-2009-dan-yoder-resource.html
tags: 
- los angeles rubyconf
- larubyconf2009
- larubyconf
- ruby waves
---

[![](http://s.wsj.net/public/resources/images/NA-AW447_LA_G_20090312182513.jpg)](http://s.wsj.net/public/resources/images/NA-AW447_LA_G_20090312182513.jpg)Lead-off man [Dan Yoder](http://dev.zeraweb.com/blog/mousetrap-2) started off the day's proceedings at the [Los Angeles Ruby Conference (LARubyConf) 2009](http://www.larubyconf.com/), with a presentation on [Ruby Waves](http://rubywaves.com/) called "Resource Oriented Architectures and Why It Matters". Despite not getting the same attention that some Ruby frameworks have, the Waves team has been tirelessly working on it. According to Dan, the foundation of Waves has gotten pretty solid. Waves adds a lot of support for things over and above just handling http requests. So what is Waves really? It is a layer on top of [Rack](http://rack.rubyforge.org/) for defining application frameworks.  
  
The next thing beyond MVC is to help developers write more rest compliant apps.  
  
But do the constraints in REST really buy anything? Actually, yes.  
  
One nice thing about internet-based development, is that the existing infrastructure is already there like proxies, load balancers etc.  
  
But why does it work? At the heart are the constraints.  
  
The web is NOT MVC  
\- so why do we use it so often for web apps  
\- piggybacking off of the web browser  
  
Example of busting out of the browser - RSS feeds from blogs and podcasts  
  
OAuth SMART Proxies  
  
Video Search  
\- edge caching  
  
Resource Oriented Architecture (ROA) is just distributed objects, loosely based on Roy Fielding's definition  
  
ROA solves an old problem, that there have been many attempts at solving previously with CORBA, COM, etc. But this time will be different.  
  
Learning From Past Mistakes  
\- be platform neutral  
\- be wire neutral (any protocol)  
\- define meta-object protocols  
\- good performance, use edge and client caching  
\- allow layered architectures  
  
Waves and ROA  
  
Rich DSL for HTTP Requests  
```
  
on (:get, \['location'\],  
  :query => {:lat => /\\d{4}/, :long => /\\d{4}/},  
  :accept => \[:json, :xml\])  

```  
But it is still Ruby!  
  
The One File Waves App  
\- influenced by Sinatra  
\- not quite as clean as Sinatra  
  
Roadmap  
  
A Resource DSL Example  
```
  
class Blog  
  include Waves::Resource::Server  
    
  resource :list, :expires => 3.days, \['blogs'\] do  
    get { model.find\_all}  
  end  
    
  ...  
    
  schema :element, \['schema', 'blog', '2009-03'\] do  
    attributes :title, String, :descriptions => String  
    link :entries, :list => Story  
  end  
    
  ...  
end  

```  
  
What's with that "schema" block? This example also defines the RDF schema for the resource to provide machine-discoverability. That is one very cool aspect of ROA that I personally have not seen addressed much within the Ruby community.  
  
Waves is really coming along, and I am planning to explore it a bit in the coming weeks. For more info, go check out [http://rubywaves.com](http://rubywaves.org)