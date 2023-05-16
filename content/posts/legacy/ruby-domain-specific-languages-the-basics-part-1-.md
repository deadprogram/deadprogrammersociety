---
title: 'Ruby Domain Specific Languages - The Basics (Part 1)'
date: 2006-11-04T16:36:00.000-08:00
draft: false
url: /2006/11/ruby-domain-specific-languages-basics.html
tags: 
- domain specific languages
- ruby
---

[![](http://www.artandmind.org/wamfestival/Images/Domain%20Field%20pic%20web%201.jpg)](http://www.artandmind.org/wamfestival/Images/Domain%20Field%20pic%20web%201.jpg)  

I have been working on a prototype of a Ruby domain specific language for one of my clients, a very large financial services company. I have learned a whole bunch of really interesting lessons, which I will share over a short series of posts as I make more progress.  
  
The first thing I tried to do was create a basic bit of DSL tastiness like this:  

```
  
class Dog < Animal  
 number\_of\_legs 4  
end  
  
class Bird < Animal  
 number\_of\_legs 2  
end  
  
class Snail < Animal  
 number\_of\_legs 0  
end  

```  
  

  
My first implementation of the Animal class looked like this:  
  

```
  
class Animal  
 attr\_accessor :number\_of\_legs  
  
 def self.number\_of\_legs(number\_of\_legs)  
  @number\_of\_legs = number\_of\_legs  
 end  
end  

```  

  
  

  
Just looking at this bit of code, it seems like it should work. However, when trying this, it doesn't work as expected.  
  

```
  
pet = Dog.new  
p pet.number\_of\_legs # prints nil  

```  

  
  

  
In Ruby EVERYTHING is an object. This includes the class objects themselves, not just the instances of class objects! This means that when the number\_of\_legs method is called, it is actually being called before the actual instance object itself has been created. We need to get to our instance variable, and one way is to copy the class-level instance variable to the instance itself when the actual instance is being initialized like this:  
  

```
  
class Animal  
 attr\_accessor :number\_of\_legs  
  
 def self.number\_of\_legs(number\_of\_legs)  
  @number\_of\_legs = number\_of\_legs  
 end  
  
 def initialize  
  instance\_variable\_set("@number\_of\_legs", self.class.instance\_variable\_get("@number\_of\_legs"))  
 end  
end  

```  
  
Now the class works as expected:  
  
```
  
pet = Dog.new  
p pet.number\_of\_legs # prints 4  

```  
  

  

  
As you add new things to your DSL, having to copy each variable manually is boring. The final change is to copy every class instance variable automatically at initialization, as follows:  
  

```
  
class Animal  
 attr\_accessor :number\_of\_legs  
   
 def self.number\_of\_legs(number\_of\_legs)  
  @number\_of\_legs = number\_of\_legs  
 end  
   
 def initialize  
  self.class.instance\_variables.each do var  
   instance\_variable\_set(var, self.class.instance\_variable\_get(var))  
  end  
 end   
end  

```  
  
This is a lot cleaner, and is much more maintainable code.