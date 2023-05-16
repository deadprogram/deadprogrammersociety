---
title: 'RubyConf 2008 - Future of RubyVM - Koichi Sasada'
date: 2008-11-10T10:13:00.000-08:00
draft: false
url: /2008/11/rubyconf-2008-future-of-rubyvm-koichi.html
tags: 
- rubyconf2008
- ruby vm
- rubyconf 2008
---

[![](http://www.atariage.com/2600/hacks/screenshots/s_YarVsYar_Hack_3.png)](http://www.atariage.com/2600/hacks/screenshots/s_YarVsYar_Hack_3.png)The first session I attended at RubyConf 2008 was called "Future of RubyVM", and it began my ascent into "VM Wonkiness" as I started to call it. [Koichi-san](http://en.wikipedia.org/wiki/YARV) is responsible for leading the team of Ruby 1.9 implementers, and is the authoritative source of info on its status. I was hoping to learn a few things, as well as to run into new acquaintance [Nobuyoshi Nakada](http://rubyforge.org/users/nobu/), one of the core team members.  
  
Techniques for VM Performance  
\- Simple techniques  
\- C level VM  
  
\- Advanced techniques  
\- Dynamic code generation  
\- Native compilation  
\- JIT compilation  
\- Polymorphic inline cache  
\- Selective inlining  
  
\- Online feedback opt.  
\- Hotspot JIT  
\- Tracing JIT  
  
Pros/Cons of JRuby/IronRuby  
\- Using an awesome VM  
\- Pros  
\- Many clever people working on the project  
\- No code is good code  
\- Many libraries already exist on each environment  
\- Easy to use parallelism  
\- Cons  
\- Not only focused on ruby, so there is a semantics gap.  
\- Cannot use C ext direct  
  
Pros/Cons of [Rubinius](http://rubini.us/)  
\- Most code in ruby  
\- Pros  
\- Ruby in Ruby  
\- Says this is the \*best way\* to improve performance in the long run because we can easily analyze and make specific performance improvements.  
\- Cons  
\- Still a LONG way to get a high performance VM  
  
Pros/Cons of C Ruby  
\- Pros  
\- Portability, using GCC  
\- C is well known language already  
\- Extensibility  
\- Performance improvement  
\- Easy to write simple extensions.  
Cons of C Ruby  
\- Extension libraries are written in C  
\- GC problem  
\- Inlining problem  
\- Limitations on program analysis  
  
Our Performance Policy  
\- CRuby is not best solution, but it is a GOOD one  
\- They continue to improve the CRuby implementation  
\- It is a pragmatic, practical selection  
\- It will be the main implementation still for at least several years  
  
Keywords for Success  
\- Embedding  
\- Parallelism  
  
Research  
The team is working on taking advantage of C some projects are running  
\- Hidden optimization techniques on YARV  
\- Ricsin  
  
Hidden Optimization Techniques  
\- turned off in 1.9.1 by default  
\- Tail call optimization  
\- Optimizing using unification  
\- Stack caching  
  
\- Left easy optimizations  
\- Efficient method caching  
\- Efficient fiber implementation using platform dependent way suvh as makcontext()  
\- These optimizations will be merged in 1.9.2  
  
Ricsin; Mix-in C Ruby  
\- Embed part of a C program into ruby  
\- Like a RubyInline, but directly embedded  
\- Usage  
\- Use C libs direct  
\- Replace all built-in classes and methods  
\- Test Ruby C API  
\- Continuous performance improvements  
  
Ruby to C AOT Compiler  
\- Translate Ruby scripts to C code ahead of time  
  
Related work  
\- [ruby2c](http://rubyforge.org/projects/ruby2c/)  
\- [yajit](http://d.hatena.ne.jp/rubynews/20080525/1211730562)  
\- [yarv2llvm](http://github.com/miura1729/yarv2llvm/tree/master)  
  
Atomic-Ruby project  
\- Issue: ruby is too fat  
\- EMBEDDED  
\- Embedded system can have special problems, such as resource limitations  
\- Application embedded ruby  
\- Some applications need just a Ruby DSL engine, not the full ruby distribution.  
\- We need a slim Ruby interpreter  
\- Utilize CRuby portability  
\- 3 subprojects  
\- Plugin/out  
\- Precompilation  
\- Swift core features  
  
Auto-write barrier detection  
\- write barrier needed for several GC algorithms.  
\- automatic WB detection system  
  
Generational GC  
1 but ref count  
  
Multi-VM (MVM) Project  
\- Multi VM in 1 process  
\- Watch runs in parallel  
\- High speed inter VM communication  
\- Sponsored by Sun  
  
Summary  
\- CRuby/YARV is not "best solution", but it is best for right now. But eventually, Rubinius is the future. Which just so happened to be the next session I attended...