---
layout: post
title: Graceful Degradation and Progressive Enhancement
date: 2015-04-30
type: post
parent_id: '0'
published: true
password: ''
status: publish
tags:
- graceful degradation
- progressive enhancement
- web app
- website
author:
  login: pmgupte
  email: prabhas.gupte@gmail.com
  display_name: pmgupte
  first_name: ''
  last_name: ''
---
These two terms are of pretty much importance when it comes to developing web apps or sites. Both, graceful degradation and progressive enhancement consider how the web site or app works when the browsers and devices vary.But the main difference is between where they focus.

**Graceful degradation** is the practice of building your web functionality such that it provides a certain level of rich user experience on modern browsers and devices, but it will also degrade gracefully to a working lower level on older browsers and devices. This working lower level is of course not a nice-to-have for your app/site users, but it still provides basic functionality so that things won't break for them.

**Progressive enhancement** is quite similar, but it goes the other way around. You start by establishing a basic level of user experience that all browsers/devices will be able to provide when rendering your web page, but you also build more advanced functionality that will be automatically be available to browsers/devices that can use it.

In simple and short words, graceful degradation is starting with higher experience quality and trying to fix it for lesser experience; whereas, progressive enhancement is starting with basic, working functionality and allowing for extension for future environments.

Degrading gracefully means looking back where as enhancing progressively means looking forward while standing on firm ground.

## Example of Graceful Degradation v/s Progressive Enhancement

Let's take a simple example of "Print This" link. As such, links that allow users to print the page are useless because the user can do the same by using browser's 'Print' button. Perhaps, letting users trigger this from within the page gives a feel of having completed the process by themselves. Think of ticket booking system to visualize this, where you yourself hit the print link or icon when you are done with all the formalities to book the ticket.

You need Javascript for that. The window object of the browser have a print() method available, which you would call and trigger the print dialog. But, what would happen when Javascript is disabled on the browser? Your code will simply not work! And, that would create very bad impression about your page because you had promised that functionality!

With graceful degradation, you would take these steps to handle this:

1. Add a link to print the page.
2. Add `<noscript>` tag, which shows its contents only when Javascript is not available, and use it to suggest some alternative to print this page. Something like "Printing this page requires Javascript enabled. Either turn it ON, or use File > Print menu."

But this also requires your user to know what Javascript is, and how to enable it. Also, we are assuming that Javascript is available.
  
On the other hand, with progressive enhancement, you would take following steps to handle the same situation:
  
1. Show a simple message like "Please take a print of this page to keep on your records". Use the id attribute to identify this message container.
2. Using Javascript, check if type of `window.print` is `function`. And, if it is so, create a button element having `Print Now` value and append it to the above message.

See how defensive this code will be. Here, we aren't assuming anything.This will work for every user regardless of how the environment is.

It can be said that both - graceful degradation and progressive enhancement - try to do the same thing: keep our web site/app useful to every user. Progressive enhancement is more sophisticated and at the same time a stable way of assuring that, but it also takes more time and efforts. Graceful degradation can be used more easily as a patch for already existing page, but it also means harder maintenance later on, but requires lesser initial work.
