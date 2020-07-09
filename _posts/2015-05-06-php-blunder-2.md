---
layout: post
title: PHP Blunder-2
date: 2015-05-06
type: post
parent_id: '0'
published: true
password: ''
status: publish
tags:
- boolean
- comparison
- echo
- equality
author:
  login: pmgupte
  email: prabhas.gupte@gmail.com
  display_name: pmgupte
  first_name: ''
  last_name: ''
---
Here is another 'oops!' moment for PHP. Do you remember the rule of transitivity? A related to B, and A related to C, implies that B is related to C. Right? Now apply this very understanding to the code below.

{% gist 8037523 %}

Now, foo equals true, and foo equals zero. So, according to this rule of transitivity, true equals zero?!
