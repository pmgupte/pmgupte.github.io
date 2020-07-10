---
layout: post
title: How to read attachment in servicenow scoped application
date: 2016-01-15
type: post
parent_id: '0'
published: true
password: ''
status: publish

tags:
- attachment
- getBytes
- getcontent
- GlideRecord
- GlideSysAttachment
- script
author:
  login: pmgupte
  email: prabhas.gupte@gmail.com
  display_name: pmgupte
  first_name: ''
  last_name: ''
---
While working on a servicenow application, I came across a scenario where I need to read the attachment contents (XML in my case) and parse them. Quick google search leads to code snippets using `GlideSysAttachment.getBytes()` which is no longer available to scoped applications, since Fuji patch 9. After trying for a while, I could read the attachment. Here's the code I used for this.

{% gist df835d6cdacf0345c2bc %}

The `sys_attachment` table contains the actual attachment, along with table name and table sys id to which this attachment belongs to. Query the `sys_attachment` table, providing table name (optional, because `table_sys_id` itself is supposed to be unique) and `table_sys_id`. Then, while iterating over result set, call `GlideSysAttachment.getContent()`, passing the `sys_attachment` glide record as argument.
