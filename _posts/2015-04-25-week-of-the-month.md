---
layout: post
title: Week of the Month
date: 2015-04-25
type: post
parent_id: '0'
published: true
password: ''
status: publish
tags:
- date
- floor
- month
- strtotime
- week
author:
  login: pmgupte
  email: prabhas.gupte@gmail.com
  display_name: pmgupte
  first_name: ''
  last_name: ''
---
In my project work, I needed to find out whether the given date falls in 1st, 2nd, 3rd, 4th or 5th week of the given month. As usual, I googled for this solution and found many functions. http://www.hotscripts.com/forums/php/37900-week-number-month.html, http://stackoverflow.com/questions/5853380/php-get-number-of-week-for-month and http://mybroadband.co.za/vb/showthread.php/66311-Calculating-the-week-in-the-month-(PHP) are some of them. But, being lazy, I thought those functions were too complex, and there could be a simpler solution to this. So I spent some time and came up with this function. Here is the code.

{% gist 5796418 %}
