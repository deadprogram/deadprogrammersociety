---
title: 'Ruby Blocks, Closures, and Continuations'
date: 2007-02-14T12:00:00.000-08:00
draft: false
url: /2007/02/ruby-blocks-closures-and-continuations.html
tags: 
- ruby
---

[![](http://www.scifun.ed.ac.uk/card/images/right/moebius.jpg)](http://www.scifun.ed.ac.uk/card/images/right/moebius.jpg)Recently, while blogging about the Ruby.NET project, it was pointed out to me that I was incorrect about Ruby.NET not supporting closures. Brendan noted that in fact continuations are what is not yet supported. I quickly realized that I was not entirely clear about the differences between a closure and a continuation, except that they both used code blocks. I decided that it must be time that I figured it out.  
  
When in doubt about any aspect of Ruby, it is best to go back to Matz. I found an interview with Matz conducted back in 2003 by Bill Venners. First, let us get Matz's definition of a block:  
  

>   
> Yukihiro Matsumoto: Blocks are basically nameless functions...Basically, you can pass a nameless function to another function, and then that function can invoke the passed-in nameless function. For example, a function could perform iteration by passing one item at a time to the nameless function. This is a common style, called higher order function style, among languages that can handle functions as first class objects...In Ruby, the difference is mainly a different kind of syntax for higher order functions. In other languages, you have to specify explicitly that a function can accept another function as an argument. But in Ruby, any method can be called with a block as an implicit argument. Inside the method, you can call the block using the yield keyword with a value.  

  
  
OK, so far so good. Any beginning Rubyist has seen the fun with blocks:  
```
  
class Array   
  def find   
    for i in 0...size   
      value = self\[i\]   
      return value if yield(value)   
    end   
    return nil   
  end   
end   
  
puts \[1, 3, 5, 7, 9\].find {|v| v\*v > 30 }   

```  
The block in the above example is used to pass a function used to tell the the "find" method how to determine when the search is complete.  
  
SO what is a closure? Matz, enlighten us:  
  

>   
> Yukihiro Matsumoto: ...we can create a closure out of a block. You can pass around a nameless function object, the closure, to another method to customize the behavior of the method. As another example, if you have a sort method to sort an array or list, you can pass a block to define how to compare the elements. This is not iteration. This is not a loop. But it is using blocks...  
>   
> Bill Venners: What makes a block a closure?  
>   
> Yukihiro Matsumoto: A closure object has code to run, the executable, and state around the code, the scope. So you capture the environment, namely the local variables, in the closure. As a result, you can refer to the local variables inside a closure. Even after the function has returned, and its local scope has been destroyed, the local variables remain in existence as part of the closure object.  

  
  
Alright, so that sounds like a pretty good definition of a closure. The Wikipedia page for Ruby has a nice, simple closure example:  
```
  
\# In an object instance variable (denoted with '@'), remember a block.  
def remember(&a\_block)  
@block = a\_block  
end  
  
\# Invoke the above method, giving it a block that takes a name.  
remember {|name| puts "Hello, #{name}!"}  
  
\# When the time is right (for the object) -- call the closure!  
@block.call("John")  
\# => "Hello, John!"  

```  
So storing a block of code into a variable makes it a closure. It can then be called later on using the "call" method.  
  
So what is a continuation, then? A short perusal of the comp.lang.ruby group led me to this [video from RubyConf 2005](http://yhrhosting.com/rubyconf/FowlerAndWeirich240S.mov) where Chad Fowler and Jim Weirich explain continuations.  
  
According to them, "A continuation is whatever happens after a block is done executing". In other words, a continuation is an object that can restore the entire context of a program back to where it was when the continuation was saved. Sounds simple enough, but the ramifications can be a little brain boggling.  
  
To summarize a little from Jim Weirich’s blog on Ruby:  
  

>   
> Ruby provides continuation functionality in the form of the callcc method. The continuation is passed to a block, and within the block we can do anything we want to with the continuation. Calling it will immediately cause the callcc call that created the continuation to return the value given to the continuation.  

  
  
Jim provides a nice simple code example, too:  
  
```
  
def level3(cont)  
  cont.call("RETURN THIS")  
end  
  
def level2(cont)  
  level3(cont)  
  return "NEVER RETURNED"  
end  
  
def top\_level\_function  
  callcc { |cc|  
    level2(cc)  
  }  
end  
  
answer = top\_level\_function  
puts answer # => "RETURN THIS"  

```  
  
The block passed into the "callcc" method has a parameter which is also a block. This parameter block is a bit of code that returns control back to the original calling code, immediately after the "callcc" method was called, along with restoring the entire context from when the original call was made.  
  
For example, in the code example above, when the **level3** method hits the line with **cont.call("RETURN THIS")**, the code returns to the **top\_level\_function** to immediately after where the **callcc** method was called in the first place. The parameter passed into the **call** method within the **level3** method is returned by the **callcc** function, then returned by **top\_level\_function**. This is why "RETURN THIS" is displayed by the above code snippet.  
  
Continuation are very cool and powerful, but I can see why most people don't get them. A little search of Krugle shows very few matches for either "callcc" or "Continuation" within the Ruby projects indexed there. It would appear very few people are using them. No wonder they might be dropping them from Ruby 2.0.