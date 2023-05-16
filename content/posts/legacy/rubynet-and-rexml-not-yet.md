---
title: 'Ruby.NET and REXML: Not Yet'
date: 2007-02-14T11:15:00.000-08:00
draft: false
url: /2007/02/rubynet-and-rexml-not-yet.html
tags: 
- ruby.net
- ruby
---

[![](http://1.bp.blogspot.com/_SgxaAaUGqzY/RdNloUZWleI/AAAAAAAAAAY/nx3lpWuG9Iw/s200/IMG_0879_w589.jpg)](http://1.bp.blogspot.com/_SgxaAaUGqzY/RdNloUZWleI/AAAAAAAAAAY/nx3lpWuG9Iw/s1600-h/IMG_0879_w589.jpg)I finally had a chance to play around with the latest download of the [Gardens Point Ruby.NET compiler](http://plas.fit.qut.edu.au/ruby.net/). At first, I was excited, as my little DSL test application was able to run perfectly. Blocks, instance\_eval, singleton classes all worked fine for me. Very cool!  
  
Then I decided to experiment with the REXML ruby parser. I did so despite the fact that the compiler authors have stated in their project goals that "We do not however plan to implement the other Ruby libraries that commonly ship with the Ruby distribution, such as CGI and DBM (except for those implemented 100% in Ruby)". Since REXML is however completely implemented in Ruby, I thought I would give it a try. Unfortunately, I discovered that the Ruby.NET authors did not lie when they said that "Implementation is not yet complete but we have now implemented the vast majority of Ruby's builtin classes and modules. We have fixed large numbers of existing bugs, but many still remain."  
  
I tried to run the simplest possible REXML sample:  
  
```
  
require "rexml/document"  
doc = REXML::Document.new File.new("mydoc.xml")  

```  
  
But here was my result:  
  
```
  
loading rexml/document  
  loading rexml/element  
    loading rexml/parent  
      loading rexml/child  
        loading rexml/node  
          loading rexml/parseexception  
          finished loading rexml/parseexception  
        finished loading rexml/node  
      finished loading rexml/child  
    finished loading rexml/parent  
    loading rexml/namespace  
      loading rexml/xmltokens  
      finished loading rexml/xmltokens  
    finished loading rexml/namespace  
    loading rexml/attribute  
      loading rexml/text  
        loading rexml/entity  
          loading rexml/source  
            loading rexml/encoding  
            finished loading rexml/encoding  
          finished loading rexml/source  
        finished loading rexml/entity  
        loading rexml/doctype  
          loading rexml/attlistdecl  
          finished loading rexml/attlistdecl  
        finished loading rexml/doctype  
      finished loading rexml/text  
    finished loading rexml/attribute  
    loading rexml/cdata  
    finished loading rexml/cdata  
    loading rexml/xpath  
      loading rexml/functions  
      finished loading rexml/functions  
      loading rexml/xpath\_parser  
        loading rexml/syncenumerator  
        finished loading rexml/syncenumerator  
        loading rexml/parsers/xpathparser  
        finished loading rexml/parsers/xpathparser  
      finished loading rexml/xpath\_parser  
    finished loading rexml/xpath  
  finished loading rexml/element  
  loading rexml/xmldecl  
  finished loading rexml/xmldecl  
  loading rexml/comment  
  finished loading rexml/comment  
  loading rexml/instruction  
  finished loading rexml/instruction  
  loading rexml/rexml  
  finished loading rexml/rexml  
  loading rexml/output  
  finished loading rexml/output  
  loading rexml/parsers/baseparser  
  finished loading rexml/parsers/baseparser  
  loading rexml/parsers/streamparser  
  finished loading rexml/parsers/streamparser  
  loading rexml/parsers/treeparser  
    loading rexml/validation/validationexception  
    finished loading rexml/validation/validationexception  
  finished loading rexml/parsers/treeparser  
  
Unhandled Exception: System.MissingMethodException: Method not found: 'System.Ob  
ject Ruby.Eval.ivar\_defined(System.String)'.  
   at Ruby.Compiler.AST.PROGRAM.ExecuteMain(PEFile Assembly, String\[\] args)  
   at Ruby.Compiler.RubyMain.Main(String\[\] args)  

```  
  
Oh well! Maybe next month's release will be ready for REXML...