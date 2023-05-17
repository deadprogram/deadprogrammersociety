---
title: 'LARubyConf 2009 - Aaron Patterson - "Journey Thru A Pointy Forest, or You Suck At XML"'
date: 2009-04-05T08:49:00.000-07:00
draft: false
url: /2009/04/larubyconf-2009-aaron-patterson-journey.html
tags: 
- ruby
- los angeles rubyconf
- xml
- larubyconf2009
- larubyconf
---

[![](http://1.bp.blogspot.com/_W1ueYt1O3xs/R0xGYiwAJNI/AAAAAAAAClQ/b7vhHdsJIG4/s320/Ice-covered%2BWillow%2BTrees.jpg)](http://1.bp.blogspot.com/_W1ueYt1O3xs/R0xGYiwAJNI/AAAAAAAAClQ/b7vhHdsJIG4/s320/Ice-covered%2BWillow%2BTrees.jpg)

The second presentation of the day at [Los Angeles Ruby Conference 2009 (LARubyConf)](http://www.larubyconf.com/) was [Aaron Patterson](http://tenderlovemaking.com/), XML maniac. I had a run at hardcore XML/XSL a few years back, and it has been a while since I walked the razor's edge of the angle bracket. But Aaron is not just an aficionado, he is genuinely obsessed. Given that he is the maintainer of the [Nokogiri](http://github.com/tenderlove/nokogiri/tree/master) and [Mechanize](http://mechanize.rubyforge.org/) gems, this makes me happy.  
  
He covered four areas related to XML:  
\- XML Processing  
\- HTML Processing  
\- Data Extraction  
\- HTML Correction  
  
The XML Processing section was as thorough a synopsis of XML as one could possible fit into just a few minutes. He went over the four main XML processing styles:  
\- SAX  
\- Push  
\- Pull  
\- DOM  
  
SAX parsers are fast, and low on memory use. However, searching is hard, doc handlers are verbose, and programmer expense high.  
  
Push Parsing works the same as SAX, the difference is the programmer controls document IO. Has low memory use, fast, fine control over IO.  
  
Pull Parsers are handed XML, and yield a node object. They work like cursors, moving thru the document, so you only get one chance to process data without starting over from the beginning again.  
  
DOM Interface is what most programmers are familiar with. Given XML, they build an in-memory tree. They can then be easily searched using XPath. DOM parsers provide easy data extraction, are programmer friendly, but have high memory use, and you pay a serious speed penalty.  
  
HTML Processing is just like XML parsing, but it limited to the HTML DOM.  
  
Data Extraction in XML can be done two different ways:  
\- CSS selectors  
\- XPath queries  
  
XPath basics:  
```
  
  //foo <!-- start at absolute root -->  
  .//foo <!-- start a relative root -->  
  //foo\[@bar\] <!-- has bar attribute -->  
  //foo\[@bar = 'baz'\] <!-- has bar attribute with a value of 'baz' -->  

```  
Here is an example of a problem for parsers that support either CSS and XPath selector as parameter, like Hpricot:  
```
  
p\[b\]  

```  
The problem is that it is both valid XPath AND CSS. Nokugiri has separate methods for searching CSS or Xpath, so as to avoid this problem.  
  
XML Namespaces use URL's to remain globally unique, to avoid collisions between XML formats taht are different, but use the same node name. Here is an important point: XML Namespaces are as important as tag names.  
  
HTML Correction is taking some invalid HTML, and "fixing" it. For example, making sure that all tags are properly nested.  
  
Aaron wrote a tool called [tree\_diff](http://github.com/tenderlove/tree_diff/tree/master), that compares XML trees, cause "they are interesting". With this tool he was able to process many HTML files with multiple HTML correctors/parsers, then compare the results to see if they matched. In many cases, they did not!  
  
Fonts are hard  
Attributes are harder  
  
29% of the time it works all of the time  
  
Seems like after all that, I will never use anything but Nokogiri for XML parsing again!