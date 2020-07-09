---
layout: post
title: Grep - before and after
date: 2015-05-13 12:23:40.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
tags:
- after
- before
- command
- count
- grep
- linux
author:
  login: pmgupte
  email: prabhas.gupte@gmail.com
  display_name: pmgupte
  first_name: ''
  last_name: ''
---
The `grep` is a command line utility for searching plain-text data sets for lines matching the given regular expression. And those using Linux (or some or other flavor of this OS), must have used this command. Here are two useful options of this command: `-A` for After and `-B` for Before. Both take a number as their value.

As their names suggest, `-A` gives you matching line and `N` lines after the matching line, similarly, `-B` gives you matching line and `N` lines before the matching line.

You can also combine both these options into single command. And, if your `-A` and `-B` values are same, then you can simply use `-C` option. C stands for Count.

{% gist 6317849 %}
