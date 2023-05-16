---
title: 'Ruby Domain Specific Languages - The Basics (Part 4)'
date: 2007-01-12T16:00:00.000-08:00
draft: false
url: /2006/11/ruby-domain-specific-languages-basics_27.html
tags: 
- domain specific languages
- ruby
---

[![](http://files.dogster.com/pix/dogs/90/194290/194290_1147718709.jpg)](http://files.dogster.com/pix/dogs/90/194290/194290_1147718709.jpg)In the [previous three entries](http://deadprogrammersociety.blogspot.com/2006/11/ruby-domain-specific-languages-basics_19.html) in this series of postings, I have been exploring the basics of creating domain specific languages using Ruby. Since I cannot disclose details of my big financial service client's DSL, I am using this made up example to illustrate the techniques that are useful when building your own Ruby DSL. So far we have created a "PetShop" domain that allows us to interact with the Pets. Defining the behavior of new Pets is the purpose of this DSL.  
  
For example, let's say we now want each Pet to be able to do some trick, when called on to do so. When you are defining behaviors, it is very useful to define a recipe-like syntax in a DSL.  
  
Here is an example:  
```
  
 pet "Toto" do  
  when\_performing\_tricks do  
   sit  
   speak  
  end  
 end  

```  
  
This is just a description or recipe of what the animal is supposed to do when asked to perform it's trick. When we really want our Pet to perform, we simply say:  
```
  
  pet.perform  

```  
  
This produces the following output:  
```
  
Toto will now perform...  
Toto is sitting...  
Toto says 'Woof!'  
Let's hear some applause for Toto!  
Slugworth will now perform...  
Slugworth is sitting...  
Let's hear some applause for Slugworth!  
Tweety will now perform...  
Tweety is sitting...  
Tweety says 'I thought I saw a putty tat!  
Tweety is flying...  
Let's hear some applause for Tweety!  

```  
  
The Pet will do whatever tricks it knows, using this little simple bit of Ruby magic:  
```
  
 def self.when\_performing\_tricks(&routine)  
  @routine = routine  
 end  
  
 def perform  
  puts "#{name} will now perform..."  
  @routine.call  
  puts "Let's hear some applause for #{name}!"  
 end  
  

```  
The "when\_performing\_tricks" method simply stores the block, and executes it only when the time comes to "perform".  
  
So how does the Pet know what is entailed in each trick? I have put the "sit" trick into the base Pet class (every Pet knows how to sit):  
```
  
 def self.sit  
  puts "#{name} is sitting..."  
 end  

```  
  
We can also more importantly define custom tricks per type of Pet. A simple bit of Ruby metaprogramming goodness helps us out:  
```
  
 def self.define\_trick(name, &trick\_definition)  
  singleton\_class.class\_eval do  
   define\_method name, &trick\_definition  
  end  
 end  
  

```  
  
The "class\_eval" methos lets us evaluate the inside expression in the context of the class object, not just a particular instance of the object. Another bit worth noting is the helper method that I have added to the DSLThing base class called "singleton\_class" that looks like this:  
```
  
 def self.singleton\_class  
  class << self; self; end  
 end    

```  
This is just a short cut to get to the class instance object, known better to Rubyists as the "singleton\_class".  
  
Lastly, the "define\_method" method then lets us define a new method for the trick. When we want to define a new trick for a particular Pet, we can simply define it like this:  
```
  
  define\_trick "speak" do  
   puts "Toto says 'Woof!'"  
  end  

```  
  
Putting it all together, here are our new definitions of the tricks our Pets can do:  
```
  
 pet "Toto" do  
  when\_performing\_tricks do  
   sit  
   speak  
  end  
    
  define\_trick "speak" do  
   puts "Toto says 'Woof!'"  
  end  
 end  
  
 pet "Tweety" do  
  when\_performing\_tricks do  
   sit  
   speak  
   fly  
  end  
    
  define\_trick "speak" do  
   puts "Tweety says 'I thought I saw a putty tat!"  
  end  
    
  define\_trick "fly" do  
   puts "Tweety is flying..."  
  end  
 end  
  
 pet "Slugworth" do  
  when\_performing\_tricks do  
   sit  
  end  
 end  

```  
  
One other interesting technique of note is that we are actually defining a new type of Pet by dynamically declaring a new class based on the Pet class. Otherwise, our custom tricks for one type of Pet might interfer with the custom tricks of another. The solution to this is using the "Object.const\_set" and "Object.const\_get". Here is the code I used:  
```
  
 def self.pet(name, &blk)  
  @pets ||= Hash.new  
  klass = Class.new(Pet)  
  Object.const\_set(name, klass) if not Object.const\_defined?(name)  
  p = Object.const\_get(name).new  
  p.name = name  
  p.class.class\_eval(&blk) if block\_given?  
  p.copyvars    
  @pets\[name\] = p  
 end  

```  
  
In this posting I have used the DSL recipe technique, and created dynamic methods and classes. Combining these techniques can allow for a very powerful and yet concise syntax when creating your own Ruby domain specific languages.  
  
Here is the complete listing of the code from this post:  
```
  
class DSLThing  
 def copyvars  
  self.class.instance\_variables.each do |var|  
   instance\_variable\_set(var, self.class.instance\_variable\_get(var))  
  end   
 end  
   
 def self.singleton\_class  
  class << self; self; end  
 end    
end  
  
class PetShop < DSLThing  
 attr\_accessor :pets, :people  
   
 def self.create(&block)  
  f = PetShop.new  
  f.class.instance\_eval(&block) if block\_given?  
  f.copyvars    
  return f  
 end  
   
 def self.pet(name, &blk)  
  @pets ||= Hash.new  
  klass = Class.new(Pet)  
  Object.const\_set(name, klass) if not Object.const\_defined?(name)  
  p = Object.const\_get(name).new  
  p.name = name  
  p.class.class\_eval(&blk) if block\_given?  
  p.copyvars    
  @pets\[name\] = p  
 end  
end  
  
class Animal < DSLThing  
 attr\_accessor :name  
   
 def initialize(name=nil)  
  @name = name  
 end  
end  
  
class Pet < Animal  
 def initialize(name=nil)  
  @name = name  
  super  
 end  
   
 def self.when\_performing\_tricks(&routine)  
  @routine = routine  
 end  
  
 def self.define\_trick(name, &trick\_definition)  
  singleton\_class.class\_eval do  
   define\_method name, &trick\_definition  
  end  
 end  
  
 def perform  
  puts "#{name} will now perform..."  
  @routine.call  
  puts "Let's hear some applause for #{name}!"  
 end  
  
 def self.sit  
  puts "#{name} is sitting..."  
 end  
end  
  
shop = PetShop.create do  
 pet "Toto" do  
  when\_performing\_tricks do  
   sit  
   speak  
  end  
    
  define\_trick "speak" do  
   puts "Toto says 'Woof!'"  
  end  
 end  
  
 pet "Tweety" do  
  when\_performing\_tricks do  
   sit  
   speak  
   fly  
  end  
    
  define\_trick "speak" do  
   puts "Tweety says 'I thought I saw a putty tat!"  
  end  
    
  define\_trick "fly" do  
   puts "Tweety is flying..."  
  end  
 end  
  
 pet "Slugworth" do  
  when\_performing\_tricks do  
   sit  
  end  
 end  
end  
  
shop.pets.each\_value do |pet|  
 pet.perform   
end  

```