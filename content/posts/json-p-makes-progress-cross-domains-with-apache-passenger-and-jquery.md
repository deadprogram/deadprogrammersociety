---
title: 'JSON-P Makes Progress Cross Domains With Apache, Passenger, and jQuery'
date: 2009-02-10T09:37:00.001-08:00
draft: false
url: /2009/02/json-p-makes-progress-cross-domains.html
tags: 
- jsonp
- json-p
- jquery
- apache
- upload progress
- passenger
---

[![](http://www.best-horror-movies.com/images/Jasonchainsmall.jpg)](http://www.best-horror-movies.com/images/Jasonchainsmall.jpg)As yet another part of the be-all, end-all media upload processing solution, my client wanted to provide a nice progress bar for tracking the status of file uploads. Let me note, that providing user feedback as to the state of an extended upload turns out to be a very important UI feature.  
  
Luckily, the problem of a nice way to track file upload progress had already been solved several times. My own platform of choice at the moment is [Apache](http://httpd.apache.org/) running with [Passenger](http://www.modrails.com/), and cool dude [Peter Sarnacki aka drogomir](http://drogomir.com) had kindly provided a handy version of the same JSON based file upload progress tracking that had been done so well on nginx, except this time for Apache in the form of [apache-upload-progress-module](http://github.com/drogus/apache-upload-progress-module/tree/master). He even had created a [jquery-upload-progress](http://github.com/drogus/jquery-upload-progress/tree/master) plugin too, which is exactly what I needed.  
  
Only one small problem... those pesky cross-domain javascript calls. As in, browsers do not as a rule, allow them. Then again, browsers do turn out to know how to be promiscuous. Which is to say, execute arbitrary JavaScript code handed to them by strange servers. Say wha? Yes, that is correct.  
  
Enter [JSON-P](http://remysharp.com/2007/10/08/what-is-jsonp/), which is the JavaScript Object Notation you know and love, with an extra layer of "Padding". What does the P in JSON do? Sorry, I could not resist that. Anyhow, the padding consists of a special temporary javascript function created just to handle the data callback from a server that is not in the same domain as the calling server.  
  
Here is an example from our need for upload progress tracking. A normal JSON request to the upload component, like this:  
```
   http://www.yourdomain.com/progress?X-Progress-ID=1234
```  
  
Would return JSON data like this:  
```
   new Object({ 'state' : 'uploading', 'received' : 35587, 'size' : 716595, 'speed' : 35587 })  

```  
  
But if we are using JSON-P, the request would include the name of the 'magic' callback function, so that the data returned from the cross-domain request is available to the original calling page, even though it is in a different domain, or even just subdomain.  
  
For example, this request:  
  
```
   http://uploads.yourdomain.com/progress?callback=jsonp123&X-Progress-ID=1234
```  
  
Would return the JSON-P function:  
```
   jsonp123(new Object({ 'state' : 'uploading', 'received' : 35587, 'size' : 716595, 'speed' : 35587 }));
```  
  
The calling page executes the 'jsonp123' function after the data is returned from the cross-domain request, and then the returned data is available to scripts on the original page. This is how Twitter and other Javascript API's are able to function with these cross-domain requests.  
  
So I whipped up patches for each the [apache-progress-module](http://github.com/drogus/apache-upload-progress-module/commit/20fed47119d3ea70b91ccb6a91a9338c8f127304), and the [jquery progress plugin](http://github.com/drogus/jquery-upload-progress/commit/a518b05fa85b1833bb3a8e8c2a0c8dfb9d6abaf1), and now that drogomir has accepted them, we can all enjoy the benefits of cross-domain uploads, along with JSON-P powered shiny progress indicators. Well, as long as it is a jquery based progress indicator you seek. I will try to get around to looking at the [Prototype progress plugin](http://github.com/drogus/prototype-upload-progress/tree/master), but since I am mostly working with [jquery](http://jquery.com/) now, perhaps someone else will jump into the fray.  
  
Have fun, and make some progress.