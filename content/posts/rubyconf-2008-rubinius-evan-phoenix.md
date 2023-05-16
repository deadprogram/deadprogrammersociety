---
title: 'RubyConf 2008 - Rubinius - Evan Phoenix'
date: 2008-11-10T21:21:00.000-08:00
draft: false
url: /2008/11/rubyconf-2008-rubinius-evan-phoenix.html
tags: 
- rubyconf2008
- Rubinius
- rubyconf 2008
- rubyconf
---

[![](http://hyperphysics.phy-astr.gsu.edu/hbase/Minerals/imgmin/rubyruf.jpg)](http://hyperphysics.phy-astr.gsu.edu/hbase/Minerals/imgmin/rubyruf.jpg)The Ruby VM wonkiness continued at RubyConf 2008 - Day 1. Next up we heard the "State of Rubinius" address on the status of the anointed heir to the Ruby federation. [Evan Phoenix](http://blog.fallingsnow.net/) is a fun guy, and it proved to be a both informative and enjoyable session.  
  
Evan says [Rubinius](http://rubini.us/) is "meta-circular-ish", and slow, but getting faster. They have a new VM that is written in C++, which is a sharp tool, and as such, it is possible to poke your eye out. However, he says it allows them to better model work. The three main advantages are:  
  
\- type safety  
\- organization  
\- architecture  
  
What is type safety, may ask many Rubyists. Well, sometimes a duck actually IS a duck. The Rubinius code just feels better with OO nature of C++, as opposed to just plain C. Also, it is possible to make the VM class hierarchy that mirrors the Ruby class hierarchy.  
  
Exporting Methods - a day in the life of a primitive operation  
  
\- things you cannot do in Ruby  
\- small example  
  
```
  
class String : Object {  
  Fixnum\* size();  
}  
  
class String  
  def size  
    Ruby.primitive :string\_size  
  end  
end  

```  
  
There was interesting question about why flatten out ala :string\_size aka no namespacing. Evan did not seem to give a definitive answer...  
  
Method Dispatch - From resolution to execution  
  
Resolution  
\- going from receiver and method name to actual method  
\- three mechanisms  
\- hierarchical lookup  
\- global cache  
\- inline cache  
  
Execution  
\- every method provide an execute function pointer  
\- each primitive is an executor  
\- Ruby methods use executor specialization  
  
Ruby Methods  
\- Specialized executors based on argument info  
\- Very simple fast version for majority of cases  
\- Slower fallback case for all cases  
  
Critical Path  
\- Populate message object  
\- Call rep over trampoline  
\- Fill in more of message object  
\- Call method executor  
  
Execution/Framing  
\- Method context objects store info about each method  
\- Chained together using refs (spaghetti stack)  
\- MethodContext creation speed is crucial  
  
\- Default contexts are allocated in special section of memory  
\- Normal execution follows simple stack pattern  
\- We can exploit to allow for fast creation and deallocation  
  
Calling to C  
Can you imaging life without ruby gems that use C extensions? For example:  
\- hpricot  
\- mongrel  
\- mysql  
\- sqlite  
Not a problem. A simple recompile == usable in Rubinius  
  
Tricky  
\- GC interaction requires indirection  
\- Uses 'quantum leap" stack jumping  
\- Allows for semi-graceful recovery from extension segfaults  
  
Performance  
Rubinius is doing well on micro-benchmarks  
\- method dispatch  
\- GC  
\- OK on macro-benchmarks  
\- Poorly on mega-benchmarks  
  
Solutions  
\- LLVM  
\- JIT  
\- AOT  
\- Improve algorithmic efficiency  
  
Rubinius is concentrating on compatibility right now, but will then address performance. Just like Koichi-san said, it is a curve of improvements.  
  
Evan ended up with a nice quote from Woody Allen - "If you're not failing every now and again, it's a sign you're not doing anything very innovative."