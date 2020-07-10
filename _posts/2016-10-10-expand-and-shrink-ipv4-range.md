---
layout: post
title: Expand and shrink IPv4 range
date: 2016-10-10
type: post
parent_id: '0'
published: true
password: ''
status: publish
tags:
- array
- array_unique
- asort
- count
- exception
- explode
- implode
- ip2long
- is_array
- is_string
- list
- long2ip
- strpos
author:
  login: pmgupte
  email: prabhas.gupte@gmail.com
  display_name: pmgupte
  first_name: ''
  last_name: ''
---
Few months ago, I had written [this blog post]({% post_url 2015-12-14-chunk-ipv4-range-into-multiple-sub-chunks %}) about chunking IPv4 range into multiple sub-ranges. Soon thereafter arouse requirement to have something to expand or shrink given IPv4 range. And, I came up with this code.

{% gist 25deaa92d2b11e85aafb4ab726eb75a8 %}

There are two functions written - one expands given IPv4 range and other shrinks it. Let me explain each of them one by one.

### The [expand_range()](https://gist.github.com/pmgupte/25deaa92d2b11e85aafb4ab726eb75a8#file-expand_shrink_ip_range-php-L18) function

The input IPv4 range could be a comma-separated list of IPv4 addresses or a proper range (e.g. 10.10.10.10-10.10.10.155) or a mix of both. Objective of this function is to provide a list of ALL IPv4 addresses that are part of given range. This function starts with exploding the input based on comma. For each element in resulting array, it checks whether its a single IPv4 address or a range having a dash (-) character. If it contains a dash, it further explodes it to get start and end IPv4 addresses, and converts them to long using [ip2long()](http://php.net/manual/en/function.ip2long.php). Then, it simply runs a for loop to generate all the long values in between them and adds them into output array. If its a single IPv4 address, that is added as it is to output array. Finally, it sorts the output array, removes duplicates using [array_unique()](http://php.net/manual/en/function.array-unique.php), and converts each element mach to IPv4 address using [long2ip()](http://php.net/manual/en/function.long2ip.php). Based on optional second argument, it either returns array or a string representation of expanded IPv4 range.

### The [shrink_range()](https://gist.github.com/pmgupte/25deaa92d2b11e85aafb4ab726eb75a8#file-expand_shrink_ip_range-php-L47) function

Here, the input IPv4 range could be either a string representation or an array, similar to one output by `expand_range()` function. Objective of this function is to shorten the given IPv4 range. So, if input is 10.10.10.10,10.10.10.11,10.10.10.12,10.10.10.13 then it should shorten it to 10.10.10.10-10.10.10.13. The function starts with creating an array out of given IPv4 addresses. If first argument itself is array, it just copies it. And it then takes [count()](http://php.net/manual/en/function.count.php) of array elements so that it can loop over them. In the loop, it keeps on checking IPv4 address and current index as well as next index. It converts both of them into log and calculates difference between them by subtracting current index's long value from next index's long value. If that difference is 1, it means the next IPv4 address is in sequence with current IPv4 address. And, that also means that we are getting into a range which can be shortened. The function then sets a flag to remember that, and starts building string for this short range. Else, its either a standalone IPv4 address OR we have possibly reached end of short range. So it checks if the flag is still ON. If yes, it ends the short range, and copies the short range string into output array. If we aren't preparing any short range, it simply adds current IPv4 into output array. Finally, based on optional second argument, it either returns array or string representation of shrunken IPv4 range.
