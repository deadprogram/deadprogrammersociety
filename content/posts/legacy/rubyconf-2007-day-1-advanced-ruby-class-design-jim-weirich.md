---
title: 'RubyConf 2007 - Day 1 - "Advanced Ruby Class Design" - Jim Weirich'
date: 2007-11-05T10:57:00.000-08:00
draft: false
url: /2007/11/rubyconf-2007-day-1-advanced-ruby-class.html
tags: 
- software architecture
- good code
- rubyconf 2007
- ruby
- rubyconf2007
- rubyconf
---

[![](http://images.43things.com/profile/59820s160.jpg)](http://images.43things.com/profile/59820s160.jpg)[Jim Weirich](http://onestepback.org/) is a very smart guy. So smart that his presentation was not about complicated classes, but about Ruby itself and how to take advantage of it to simplify things. Jim's background in computing is long and varied, something like a history lesson in programming languages. Here is the abbreviated list:  
  
FORTRAN > C > Modula 2 > C++ > Eiffel > Java  
and in parallel to this:  
LISP > FORTH > TCL > Perl  
  
Jim got started programming taking an introduction to FORTRAN class that just so happenened to be taught by [Daniel Friedman](http://en.wikipedia.org/wiki/Daniel_P._Friedman), author of "The Little LISPer". As such, they studied LISP for the first half of the semester. They did finally get around to FORTRAN, where Jim learned firsthand the adage:  
  
"A real programmer can write FORTRAN (Java) in any language"  
  
Jim took us thru three examples that illustrate some very cool techniques to use as part of elegant class design in Ruby.  
  
**Box 1. Rake::FileList**  
Everyone knows and loves Rake, right? Rake::FileList is like an array but:  
\- can init with GLOB (an array of filenames, created using a pattern match expression)  
\- has a specialized to\_s  
\- has extra methods  
\- uses lazy evaluation  
  
In his first cut, Jim derived from Array:  
```
  
class FileList > Array  
 ...  
end  

```  
Here is the first implementation for FileList:  
```
  
class FileList > Array  
 def initialize(pattern)  
  super  
  @pattern = pattern  
  @resolve = false  
 end  
  
 def resolve  
  self.clear  
  Dir\[@pattern\].each do |file|  
   ...  
  end  
 end  
end  

```  
The problem is this:  
```
  
f1 = FileList.new("\*.c")  

```  
won't work, cause we never call "resolve". What we need to do is to do some lazy loading to "auto resolve", like this:  
```
  
def \[\](index)  
 resolve if ! @resolve  
end  

```  
Lots of methods need to call resolve in this manner... which is a problem that Jim solves later using a little metaprogramming.  
  
But there is a another problem with the current implementation. This is OK:  
```
  
f1 = FileList.new('\*.rb')  
f1 + \['thing.rb'\]  

```  
But this is NOT:  
```
  
f1 = FileList.new('\*.rb')  
\['thing.rb'\] + f1  

```  
Why? Because the + method requires passing a literal array to it as an argument, not an object of class Array. If only there was a way for an arbitrary object could indicate that it wants to be treated like an array... ah, but there is! The "to\_ary" method was designed to do exactly this. The problem is you cannot call the to\_ary method on an Array. The solution is not to derive the FileList class from Array, but instead to use the "to\_ary" method to access an Array that is encapsulated into the FileList class.  
  
Another shortcut is instead of calling resolve on each method, using some metaprogramming to add the "resolve" call to every method that might need it, like this:  
```
  
RESOLVING\_METHODS = \[:this, :that\]  
RESOLVING\_METHODS.each do |method|  
 ...  
end  

```  
The big lesson here is when trying to mimic a class, use "to\_ary" and "to\_str" rather than inheritance.  
  
**Box 2 - The Art of Doing Nothing**  
Builder is a very cool library which is part of the standard Ruby library to create XMl files, but using a friendly Ruby syntax. Did I mention that Jim is the original creator of Builder? Here is an example of Builder in use, if you are not familiar with it:  
```
  
xml = Builder::XmlMarkup.new(:indent =>2)  
xml.student {  
 xml.name("Jim")  
 xmp.phone\_number  
}  

```  
Builder uses method\_missing to construct tags. This works really well... except what happens if you try to use it with a predefined method? method\_missing will not work anymore, since the method is actually there.  
  
Jim solution is to "inherit from Object without actually inheriting from Object", a class he calls BlankSlate. We want to have our Builder class inherit from BlankSlate, instead of Object.  
```
  
class BlankSlate  
 instance\_methods.each do |method|  
  undef\_method(method)  
 end  
end  

```  
That does indeed get rid of all of the methods on the class. But that does not work, because there are some internal methods that Ruby needs that we do not want to get rid of, so we extend the class to this:  
```
  
class BlankSlate  
 instance\_methods.each do |method|  
  undef\_method(method) unless name =~ /~\_\_/  
 end  
end  

```  
This is not the only problem, however. Since in Ruby classes are open, we can also extend them using Modules.  
```
  
require 'blank\_slate'  
  
module Kernel  
 def name  
  "hi"  
 end  
end  
  
xml.name("Jim")  
  
class BlankSlate  
 def self.hide(method)  
  ...  
 end  
   
 instance\_methods.each do |method|  
  undef\_method(method) unless method =~ /^\_\_/  
 end  
end  
  
  
module Kernel  
 class << self  
  alias\_method :original\_method\_added, :method\_added  
    
  def method\_added(name)  
   result = original\_method\_added(name)  
   BlankSlate.hide(name) if self == Kernel  
   result  
  end  
 end  
end  

```  
We will need to do something similar for Object, in order to avoid the same problem. So are we done? Not quite, there is still one more thing... but I didn'y quite catch what it was! I will update this when Jim puts his slides up:  
```
  
require 'blank\_slate'  
  
module Kernel  
 def name  
  "hi"  
 end  
end  
  
class Object  
 include Name  
end  
...  
xml.name("Jim")  

```  
Hint: Use #append\_features to modify open classes.  
  
**Box 3 - Parsing Without Parsing**  
ActiveRecord is a wonderful abstraction to use, but why is it that we use such a non-Ruby-like technique to select records. For example, we would use this in Rails:  
```
  
User.find(:all, :conditions => \["name = ?", 'jim'\])  

```  
Versus using a more standard Ruby language enumerable approach, like this:  
```
  
user\_list.select { |user|  
 user.name == "jim"  
}  

```  
Wouldn't it be nicer to do something like this:  
```
  
User.select { |user|  
 user.name == "Jim"  
}  

```  
Jim starts out with a naive implementation, like this:  
```
  
class User  
 def self.select(&blk)  
  find(:all).select(&blk)  
 end  
end  

```  
There are several problems, not the least of which is that the above code is far from efficient. A large set of results will use an enormous amount of memory.  
  
Jim then goes on to show a properly "magic" implementation:  
```
  
class User  
 def self.select(&blk)  
  cond = translate\_block\_to\_sql(&blk)  
  find(:all, :conditions => cond)  
 end  
end  

```  
How to implement the magic translate\_block\_to\_sql method?  
\- write a parser yourself  
\- Use Parse Tree (Ambition project)  
\- Just execute the code in the block  
  
As one might suspect, the answer is of course "just execute the code". In other words, create appropriate methods that are called when the block is executed to return the correct SQL conditions clause for the query. Let me warn you, dear reader, that I typed as fast as I could, but some of the code examples here are a little incomplete. As soon as Jim posts his slides online, I will revise and complete them.  
```
  
class User  
 def self.select(&blk)  
  cond = translate\_block\_to\_sql(&blk)  
  find(:all, :conditions => cond)  
 end  
  
 def translate\_block\_to\_sql(&blk)  
  instance\_eval(&blk) # this is not exactly the code, but I couldn't type fast enough!  
 end  
end  
  
class MethodNode < Node  
 def to\_s  
  ...  
 end  
end  

```  
OK, now what about the "==" operator?  
```
  
class Node  
 def ==(other)  
  BinaryOpNode.new("=", self, other)  
 end  
end  
  
class BinaryOpNode < Node  
 def initialize(operand, left, right)  
  @operand = operand  
  @left = left  
  @right = right  
 end  
   
 def to\_s  
  "#{@left} #{@operand} #{@right}"  
 end  
end  
  
class LiternalNode < Node  
 ...  
end  
  
class StringNode < Node # puts quotes around the string for SQL query  
 ...  
end  

```  
Do not use a case statement to differentiate between types. Instead open core classes, like this:  
```
  
class Object  
 def as\_a\_sql\_node  
  ...  
 end  
end  
  
class String  
 def as\_a\_sql\_node  
  ...  
 end  
end  

```  
Be careful how you name methods to avoid collisions.  
  
Possible problems? Literals on left, because "==" is commutative. The solution is to use "coerce" method to handle numeric operators.  
  
More possible problems?  
"&&" and "||" operators cannot be overridden in Ruby cause they have short-circuit semantics in the Ruby language interpreter itself. Perhaps & and | instead? Too bad, because we have to write "special" semantics. Also "!" and "!=" cannot be overridden in Ruby  
  
The ruby "criteria' lib already implements some of these ideas.  
  
**Conclusion**  
One important lesson to take away, is that programming languages really shape the way we approach problems. Learn the corners of whatever language you are using to take full advantage of it. Don't be afraid to think outside the box of past experience...  
  
Jim was an amazing and dynamic speaker. All I can say is [Joe O'Brian](http://objo.com/) and the people at [EdgeCase](http://theedgecase.com/) are very fortunate to have him around.