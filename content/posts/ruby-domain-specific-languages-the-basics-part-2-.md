---
title: 'Ruby Domain Specific Languages - The Basics (Part 2)'
date: 2006-11-08T12:29:00.000-08:00
draft: false
url: /2006/11/ruby-domain-specific-languages-basics_08.html
tags: 
- domain specific languages
- ruby
---

[![](http://photos1.blogger.com/blogger/4812/3999/200/240px-Circus_Lion_Tamer.jpg)](http://photos1.blogger.com/blogger/4812/3999/1600/240px-Circus_Lion_Tamer.jpg)Previously, I was [exploring the basics of DSL creation using Ruby](http://deadprogrammersociety.blogspot.com/2006/11/ruby-domain-specific-languages-basics.html). This post continues sharing my lessons learned while developing a prototype of a domain specific language in the mortgage industry. Since I cannot share the actual code itself belonging to my client, I will continue to extract the useful concepts into these simple examples.  
  
Last time we created a simple Animal DSL class. The important part of that class is this bit that makes sure our DSL like syntax works for the declarative methods:  
```
  
class Animal  
 attr\_accessor :number\_of\_legs  
   
 def self.number\_of\_legs(number\_of\_legs)    
  @number\_of\_legs = number\_of\_legs   
 end  
  
 def initialize  
  self.class.instance\_variables.each do |var|  
   instance\_variable\_set(var, self.class.instance\_variable\_get(var))  
  end  
 end  
end  

```  
Now we will create a Person class that can interact with the Animals. Each Person will have a temperament (either mean or nice), and will be carrying some kind of food in their pocket to feed their pet. We will define people using our DSL as follows:  
  
```
  
class Dorothy < Person  
 temperament :nice  
 food :sunflower\_seeds, :carrot\_juice  
end  
  
class Witch < Person  
 temperament :mean  
 food :cheetos, :soda  
end  

```  
  
The implementation is very similar to the basic Animal class  
```
  
class Person < Animal  
 attr\_accessor :temperament  
   
 def self.temperament(type)  
  @temperament = type  
 end  
   
 def self.food(\*types\_of\_food)  
  @food ||= \[\]  
  types\_of\_food.each do |food|  
   @food << food  
  end  
 end  
   
 def has\_food?(type\_of\_food)  
  @food.include?(type\_of\_food)  
 end  
end  

```  
  
Since we are working with an array, the self.food method has a variable number of parameters, represented using the asterisk in front of the parameters list. The cool little idiom @food ||= \[\] returns with the current @food variable, or if it is nil, returns an empty array. There is also a has\_food? method to tell us if a person is carrying a certain type of food.  
  
Now let us introduce the Pet. We will use the power of Ruby blocks to tell each pet the rules about when it likes a person, or not. Here is the DSL we want to use for the Pets:  
```
  
class Toto < Pet  
 friend\_test do |person|  
  true unless person.temperament == :mean # I like anyone who is not mean  
 end  
  
end  
  
class Tweety < Pet  
 friend\_test do |person|  
  true if person.has\_food?(:sunflower\_seeds) # I like anyone who has sunflower seeds  
 end  
end  
  
class Slugworth < Pet  
 friend\_test do |person|  
  true # I like anyone  
 end  
end  

```  
  
And now the implementation of the Pet class:  
```
  
class Pet < Animal  
 def self.friend\_test(&test)  
  @friend\_test = test  
 end  
   
 def is\_friend?(person)  
  @friend\_test.call(person) == true  
 end   
end  

```  
  
The friend\_test method stores a block containing the test for that Pet, and the is\_friend? method tests to see if a Pet will be friendly toward a particular Person.  
Last, we put it all together with some simple code to display the interactions between the People and the Pets:  
```
  
dog = Toto.new  
bird = Tweety.new  
snail = Slugworth.new  
  
person = Dorothy.new  
puts "#{dog.class.name} is a friend of #{person.class.name}: #{dog.is\_friend?(person)}"  
puts "#{bird.class.name} is a friend of #{person.class.name}: #{bird.is\_friend?(person)}"  
puts "#{snail.class.name} is a friend of #{person.class.name}: #{snail.is\_friend?(person)}"  
puts  
  
person = Witch.new  
puts "#{dog.class.name} is a friend of #{person.class.name}: #{dog.is\_friend?(person)}"  
puts "#{bird.class.name} is a friend of #{person.class.name}: #{bird.is\_friend?(person)}"  
puts "#{snail.class.name} is a friend of #{person.class.name}: #{snail.is\_friend?(person)}"  

```  
  
The result of running this code is:  
```
  
Toto is a friend of Dorothy: true  
Tweety is a friend of Dorothy: true  
Slugworth is a friend of Dorothy: true  
  
Toto is a friend of Witch: false  
Tweety is a friend of Witch: false  
Slugworth is a friend of Witch: true  

```  
Using this simple Ruby DSL approach, it is very easy to add a new Person or Pet, just by entering the rules that define its behavior. As the objects in a system become more complex, one of the best ways to manage that complexity is to create an abstraction that hides the ugly bits.  
  
Here is the full code for this example:  
```
  
class Animal  
 attr\_accessor :number\_of\_legs  
   
 def self.number\_of\_legs(number\_of\_legs)    
  @number\_of\_legs = number\_of\_legs   
 end  
  
 def initialize  
  self.class.instance\_variables.each do |var|  
   instance\_variable\_set(var, self.class.instance\_variable\_get(var))  
  end  
 end  
end  
  
class Person < Animal  
 attr\_accessor :temperament  
   
 def self.temperament(type)  
  @temperament = type  
 end  
   
 def self.food(\*types\_of\_food)  
  @food ||= \[\]  
  types\_of\_food.each do |food|  
   @food << food  
  end  
 end  
   
 def has\_food?(type\_of\_food)  
  @food.include?(type\_of\_food)  
 end  
end  
  
class Pet < Animal  
 def self.friend\_test(&test)  
  @friend\_test = test  
 end  
   
 def is\_friend?(person)  
  @friend\_test.call(person) == true  
 end   
end  
  
  
class Toto < Pet  
 friend\_test do |person|  
  true unless person.temperament == :mean  
 end  
  
end  
  
class Tweety < Pet  
 friend\_test do |person|  
  person.has\_food?(:sunflower\_seeds)   
 end  
end  
  
class Slugworth < Pet  
 friend\_test do |person|  
  true  
 end  
end  
  
class Dorothy < Person  
 temperament :nice  
 food :sunflower\_seeds, :carrot\_juice  
end  
  
class Witch < Person  
 temperament :mean  
 food :cheetos, :soda  
end  
  
  
dog = Toto.new  
bird = Tweety.new  
snail = Slugworth.new  
  
person = Dorothy.new  
puts "#{dog.class.name} is a friend of #{person.class.name}: #{dog.is\_friend?(person)}"  
puts "#{bird.class.name} is a friend of #{person.class.name}: #{bird.is\_friend?(person)}"  
puts "#{snail.class.name} is a friend of #{person.class.name}: #{snail.is\_friend?(person)}"  
puts  
  
person = Witch.new  
puts "#{dog.class.name} is a friend of #{person.class.name}: #{dog.is\_friend?(person)}"  
puts "#{bird.class.name} is a friend of #{person.class.name}: #{bird.is\_friend?(person)}"  
puts "#{snail.class.name} is a friend of #{person.class.name}: #{snail.is\_friend?(person)}"  

```