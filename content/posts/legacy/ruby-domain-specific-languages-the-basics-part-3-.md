---
title: 'Ruby Domain Specific Languages - The Basics (Part 3)'
date: 2006-11-19T15:00:00.000-08:00
draft: false
url: /2006/11/ruby-domain-specific-languages-basics_19.html
tags: 
- domain specific languages
- ruby
---

[![](http://www.grandtline.com/images/marketville/pete.jpg)](http://www.grandtline.com/images/marketville/pete.jpg)This is another installment in a series about creating domain specific languages with Ruby. In [part 1](http://deadprogrammersociety.blogspot.com/2006/11/ruby-domain-specific-languages-basics.html) and [part 2](http://deadprogrammersociety.blogspot.com/2006/11/ruby-domain-specific-languages-basics_08.html) of this series, I created a simple Ruby [DSL](http://en.wikipedia.org/wiki/Domain_Specific_Language) to describe the relationship between Pets and Persons. Now I will extend the DSL, and use some cool Ruby metaprogramming tricks to demonstrate the power and benefits of using Ruby to create an [internal DSL](http://www.martinfowler.com/articles/languageWorkbench.html#InternalDsl).  
First, I want to simplify the syntax for declaring things in our DSL. Getting rid of the class definition stuff can make it a lot easier for domain experts to read. A simple, cool declarative style like [Rake](http://rake.rubyforge.org/) is what we want to end up with, something like this:  
```
  
person "Dorothy" do  
   temperament :nice  
   food :sunflower\_seeds, :carrot\_juice  
end  

```  
Furthermore, I want to extend our DSL to put all of the descriptions of Pets and Persons together into a PetShop. Here is our PetShop DSL:  
```
  
shop = PetShop.create do  
   pet "Toto" do  
      friend\_test do |person|  
         true unless person.temperament == :mean  
      end  
   end  
  
   pet "Tweety" do  
      friend\_test do |person|  
         person.has\_food?(:sunflower\_seeds)  
      end  
   end  
  
   pet "Slugworth" do  
      friend\_test do |person|  
         true # I like anyone  
      end  
   end  
  
   person "Dorothy" do  
      temperament :nice  
      food :sunflower\_seeds, :carrot\_juice  
   end  
  
   person "Witch" do  
      temperament :mean  
      food :cheetos, :soda  
   end  
end  

```  
One interesting technique used is declaring the "pet" within the "do-end" block for the "petshop" object:  
```
  
shop = PetShop.create do  
   pet "Toto" do  
      friend\_test do |person|  
         true unless person.temperament == :mean  
      end  
   end  
  
...  
end  

```  
The little bit of DSL niceness is achieved using the class\_eval method. The block of code within the "do" block is called in the context of the newly created object. Here is the Ruby code that achieves this for a new Pet:  
```
  
def self.pet(name, &blk)  
   @pets = Hash.new  
   p = Pet.new(name)  
   p.class.class\_eval(&blk) if block\_given?  
   @pets\[name\] = p  
   p.copyvars  
end  

```  
  
Now that we have declared all of the Pets and Persons in to the context of a PetShop, we can test the relationships between Pets and Persons is a more general purpose way then in my previous post. The older, more fragile code was this:  
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
puts  

```  
The new, cleaner code is like this:  
```
  
shop.people.each\_value do person  
   shop.pets.each\_value do pet  
      puts "Is #{pet.name} a friend of #{person.name}? #{pet.is\_friend?(person)}"  
   end  
end  

```  
And here is the output when we run the program:  
```
  
Is Toto a friend of Witch? false  
Is Slugworth a friend of Witch? true  
Is Tweety a friend of Witch? false  
Is Toto a friend of Dorothy? true  
Is Slugworth a friend of Dorothy? true  
Is Tweety a friend of Dorothy? true  

```  
We have simplified the syntax of our domain specific language, and added some additional functionality. We have also been able to reduce the amount of Ruby code required at the same time.  
  
Here is the final version of the code:  
```
  
class DSLThing  
 def copyvars  
  self.class.instance\_variables.each do |var|  
   instance\_variable\_set(var, self.class.instance\_variable\_get(var))  
  end   
 end  
end  
  
class PetShop < DSLThing  
 attr\_accessor :pets, :people  
   
 def self.create(&block)  
  f = PetShop.new  
  f.class.class\_eval(&block) if block\_given?  
  f.copyvars    
  return f  
 end  
   
 def self.pet(name, &blk)  
  @pets ||= Hash.new  
  p = Pet.new(name)  
  p.class.class\_eval(&blk) if block\_given?  
  @pets\[name\] = p  
  p.copyvars    
 end  
   
 def self.person(name, &blk)  
  @people ||= Hash.new  
  p = Person.new(name)  
  p.class.class\_eval(&blk)  
  @people\[name\] = p  
  p.copyvars    
 end  
end  
  
class Animal < DSLThing  
 attr\_accessor :name  
   
 def initialize(name=nil)  
  @name = name  
 end  
end  
  
class Person < Animal  
 attr\_accessor :temperament  
   
 def initialize(name=nil)  
  super  
 end  
   
 def self.temperament(type)  
  @temperament = type  
 end  
   
 def self.food(\*types\_of\_food)  
  @food = \[\]  
  types\_of\_food.each do |food|  
   @food << food  
  end  
 end  
   
 def has\_food?(type\_of\_food)  
  @food.include?(type\_of\_food)  
 end  
end  
  
class Pet < Animal  
 def initialize(name=nil)  
  super  
 end  
   
 def self.friend\_test(&test)  
  @friend\_test = test  
 end  
   
 def is\_friend?(person)  
  @friend\_test.call(person) == true  
 end   
end  
  
shop = PetShop.create do  
 pet "Toto" do  
  friend\_test do |person|  
   true unless person.temperament == :mean  
  end  
 end  
  
 pet "Tweety" do  
  friend\_test do |person|  
   person.has\_food?(:sunflower\_seeds)   
  end  
 end  
  
 pet "Slugworth" do  
  friend\_test do |person|  
   true # I like anyone  
  end  
 end  
  
 person "Dorothy" do  
  temperament :nice  
  food :sunflower\_seeds, :carrot\_juice  
 end  
  
 person "Witch" do  
  temperament :mean  
  food :cheetos, :soda  
 end  
end  
  
shop.people.each\_value do |person|  
 shop.pets.each\_value do |pet|  
  puts "Is #{pet.name} a friend of #{person.name}? #{pet.is\_friend?(person)}"   
 end  
end  

```