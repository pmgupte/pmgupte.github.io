---
layout: post
title: How to get plain text inside any XML tag using python
date: 2017-08-17
type: post
parent_id: '0'
published: true
password: ''
status: publish
tags:
- elementtree
- fromstring
- iterator
- itertext
- plaintext
- print
- xml
author:
  login: pmgupte
  email: prabhas.gupte@gmail.com
  display_name: pmgupte
  first_name: ''
  last_name: ''
---
While coding in python, if you need to get plaintext inside a particular tag in XML, you can make use of text iterator provided by [ElementTree](https://docs.python.org/2/library/xml.etree.elementtree.html#module-xml.etree.ElementTree). You can call [itertext()](https://docs.python.org/2/library/xml.etree.elementtree.html#xml.etree.ElementTree.Element.itertext) on any XML element, and it returns an iterator which will walk you through text of each tag inside your current element.

{% gist d16f47691d9055417e70637a5c6bc25c %}

The code is simple and self explanatory. You iterate over the text iterator, concatinating text of each element inside given element to some string variable. At the end of the loop, you return the combined text.
