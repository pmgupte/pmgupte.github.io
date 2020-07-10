---
layout: post
title: Chunk IPv4 range into multiple sub-chunks
date: 2015-12-14
type: post
parent_id: '0'
published: true
password: ''
status: publish
tags:
- array
- array_chunk
- array_pop
- array_shift
- count
- explode
- floor
- ip2long
- list
- long2ip
- range
author:
  login: pmgupte
  email: prabhas.gupte@gmail.com
  display_name: pmgupte
  first_name: ''
  last_name: ''
---
One of my non-programmer-but-in-IT friends came to me last week, asking help to chunk a range of IPv4 addresses into N small chunks. And, here's the PHP code I came up with within 10 mins.

{% gist e84d5cc4daed1c9699ed %}

What it simply does is, explode the input range, and convert start and end IP address into long, using `ip2long()`. Then, using `range()` expand it into a whole list. Once that is done, then decide number of elements that should go into each chunk - remember, the optional argument to this function tells how many chunks are to be prepared. the formula is there on code line number 11.

Once you have this number, call `array_chunk()` to create chunks. Finally, iterate over them, get start and end IP of each of them (which are still long numbers), convert them back to IPv4 address using `long2ip()` and create the range string for them.

Do you find it useful? Copy it! Have any suggestion, let me know in the comment on that gist!!
