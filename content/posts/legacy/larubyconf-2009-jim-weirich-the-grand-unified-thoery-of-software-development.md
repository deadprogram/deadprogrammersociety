---
title: 'LARubyConf 2009 - Jim Weirich - "The Grand Unified Thoery of Software Development'
date: 2009-04-08T10:12:00.000-07:00
draft: false
url: /2009/04/larubyconf-2009-jim-weirich-grand.html
tags: 
- los angeles rubyconf
- keynote
- larubyconf2009
- larubyconf
---

[![](http://homepage.mac.com/michaelrevans/photos/tetron-cluster-front.jpg)](http://homepage.mac.com/michaelrevans/photos/tetron-cluster-front.jpg)As the 2009 [Los Angeles Ruby Conference (LARubyConf)](http://www.larubyconf.com/) drew to a close, our keynote speaker [Jim Weirich](http://onestepback.org/) took the podium. I have seen Jim speak several times, and he is both intelligent, as well as down to earth, which is a rare combination indeed.  
  
The subject of his keynote would be anything but down to earth. In fact, it would have to be one of the most ambitious talks I have ever seen at a Ruby conference. Only Jim could have pulled it off as he did, with both humor and insight.  
  
One thing Jim does is have to conduct Tech Interviews. One question he always asks is "What do you look for in a good design?" Most people's answer: "UMMMMMM..."  
  
Then Jim seemingly shifted themes abruptly, to physics. Specifically, subatomic particles.  
  
It is known that particles that are charged the same repulse each other. Furthermore, every time you change electric field, there is a changing magnetic field at 90 degree angle.  
  
[James Clerk Maxwell](http://en.wikipedia.org/wiki/James_Clerk_Maxwell)  
Maxwell discovered 4 equations that describe relation between electrical and magnetic fields. By describing these two entirely separate forces, combines into single force. Maxwell's work probably greatest contribution to science.  
  
Then, along came [Ernest Rutherford](http://en.wikipedia.org/wiki/Ernest_Rutherford)'s famous [electron experiment](http://en.wikipedia.org/wiki/Geiger-Marsden_experiment). The one where electrons were supposed to evenly deflect onto a screen, but instead occasionally would deflect wildly. As a result, we now know that matter was mostly open space.  
  
There are four known forces  
\- electromagnetic  
\- gravity  
\- strong nuclear  
\- weak nuclear  
  
The search for the "Unified Field Theory" in physics is a search for a single explanation that accommodates all four forces.  
  
This is very much like the search for a single explanation for software design.  
  
Some Commonly Accepted Software Design Principles  
\- [SOLID](http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod)  
\- [Law of Demeter](http://en.wikipedia.org/wiki/Law_of_Demeter)  
\- [DRY](http://en.wikipedia.org/wiki/Don%27t_repeat_yourself)  
\- [Small Methods](http://clintshank.javadevelopersjournal.com/smallmethods.htm)  
\- [Design by Contract](http://en.wikipedia.org/wiki/Design_by_contract)  
  
Lots of ideas about how to write software, but no grand unified theory.  
  
"The Grand Unified Theory of Software Development"  
  
[Composite/Structured Design](http://www.amazon.com/Composite-Structured-Design-Glenford-Myers/dp/0442805845)  
\- Glenford J Meyers - 1978  
  
Coupling & Cohesion - from best to worst  
\- no coupling  
\- data coupling - local data, simple  
\- stamp coupling - local data, structured  
\- control coupling  
\- external coupling - global data, simple  
\- common coupling - global data, structured  
\- content coupling - when you reach inside of modules and mess with them from outside  
  
control coupling  
\- method has flag parameter  
\- flag control which algorithm to use  
  
Symptoms  
\- word OR in description  
  
Example:  
```
Array.instance\_methods(true)
```and  
```
Array.instance\_methods(false)
```  
  
Which one lists only private methods?  
  
Another example, Rails does this:  
```
Customer.find(:all)
```vs.  
```
Customer.find(:first)
```  
  
Myers' classification were OK, however failed to extend well to objects and dynamic languages  
  
Meilir Page-Jones's book ["What Every Programmer Should Know About Object-Oriented Design"](http://www.amazon.com/Every-Programmer-Should-Object-Oriented-Design/dp/0932633315/ref=sr_1_2?ie=UTF8&s=books&qid=1239585961&sr=1-2) has 3 sections, two of which are not too useful, but the third is very interesting. It talks about the idea of Connascence in software design.  
  
Connascence - when two things are born and grow up together  
Two pieces of code share Connascence when a change in one module requires a corresponding change in the other.  
  
CoN - Connascence of Name  
\- when code linked by name  
\- can also apply to databases  
\- class name is NOT, but parameters are  
  
Locality Matters  
\- if you have things grouped together, there is stronger connascence.  
\- as dist increase, you reduce connect between them  
  
Connescence of Position  
\- when the order of the params matters  
  
Low/high degree of CoP  
  
When you encounter CoP it is better to transform it to CoN  
  
Degree Matters  
  
CoP in test data example  
```
  
  User.find(:first)  

```  
  
CoM - Connescence of Meaning  
\- when two bits of code have to agree on the meaning of data  
  
When you encounter CoM it is better to transform it to CoN  
  
Contranesence is when things have to change opposite to each other  
\- for example, collision of class names in two different modules  
\- solution is to use namespaces  
  
Another Example?  
\- do not monkeypatch unless you have to, and if so use namespaces  
  
Connascence of Algorithm  
\- Two methods that do different things, but that are bound together by algorithm. For example, two different bits of code in two different languages that have to talk to each other. JavaScript client, Ruby server is good example.  
  
CoA -> CoN  
\- also known as DRY  
  
CoT - Connascence of Timing  
\- for example, a race condition  
  
Summary  
\- Connascence is the 'quark' of software design  
\- Not really any tools to analyze code  
\- Seems like there is a relation between connascence and design patterns  
  
Wow! Jim had taken us all the way from subatomic particles, to a start towards a unified theory of software design, and tied it all together nicely. And made it fun! It was a tremendous cap on an excellent conference, and we all had really appreciated Jim's contribution.