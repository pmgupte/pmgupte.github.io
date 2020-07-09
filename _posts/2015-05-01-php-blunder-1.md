---
layout: post
title: PHP Blunder - 1
date: 2015-05-01
type: post
parent_id: '0'
published: true
password: ''
status: publish
tags:
- boolean
- comparison
- 'null'
- var_dump
author:
  login: pmgupte
  email: prabhas.gupte@gmail.com
  display_name: pmgupte
  first_name: ''
  last_name: ''
---
>PHP is one of those most popular web programming languages, but it do have some serious mistakes. Here's one of them.

PHP have a predefined value 'null'. And, it can be compared with numeric values. As anybody else would, you would expect null to have a constant value, right? But that's where PHP have a problem. Look at the code below, and execute it on your system if you want to check.

{% gist 8025297 %}

The `null == 0` evaluates to true. So does `null < -1`. How can some predefined value be equal to 0 and lesser than -1 at the same time?!
