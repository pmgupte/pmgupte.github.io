---
layout: post
title: 6 points you need to know to develop Jenkins plugin
date: 2017-08-13
type: post
parent_id: '0'
published: true
password: ''
status: publish
tags:
- jenkins
- plugin
- resources
author:
  login: pmgupte
  email: prabhas.gupte@gmail.com
  display_name: pmgupte
  first_name: ''
  last_name: ''
---
**This blog post is to help you with resources to get you started with Jenkins plugin development. This is NOT a plugin development tutorial. I do not wish to repeat any of the contents which are already available online. This blog post should be seen as a pointer towards those various contents which could help you develop your first Jenkins plugin.**

## General idea

As part of my integrations development duties, I needed to work on Jenkins plugin development. The idea was simple: the plugin should work as post-build step, and pull some report from a cloud based system. This plugin is supposed to be used in CD/CI pipeline.

## What you need to know to develop Jenkins plugin?

1. Maven.
2. Setting up your development environment.
3. Plugin project structure.
4. Java.
5. Groovy script.
6. Extension points to use in your plugin.

Since I had no prior experience with developing any plugin with Jenkins, I had to start right from the scratch. First obvious step was to start reading and trying out some code. 
This [Jekins wiki page](https://wiki.jenkins.io/display/JENKINS/Plugin+tutorial) is really helpful getting started. It shows how to setup your development environment, how to test run your code, how to debug, and how to package your plugin.

Its better if you already know how to use Maven, but that is not any hard and fast requirement. Even if you haven't used it earlier, you can still work with that. With help of Maven archetype, you would be generating your starter code. Instructions for that are also given in that Jenkins wiki page. It generates a simple Builder step.

Point # 6 above is Extension points. There are several classes exposed by Jenkins - called as extension points - which you will be extending or implementing to provide your plugin functionality. For example, to do something after build is completed, you need to extend Notifier class. Whichever class you annotate with `@Extension` annotation, Jenkins will load at appropriate time - depending on which class you are extending or implementing.

If you are going to support only freestyle project, you would mostly need to implement SimpleBuildStep class.

## Supporting pipelines

As mentioned on [Jenkins pipeline page](https://jenkins.io/doc/book/pipeline/#overview), its a suite you use for continuous integration/delivery. If you need to support pipeline project, SimpleBuildStep may not be the correct choice for you. AFAIK, you need to implement AbstractStepImpl to provide same functionality as a pipeline step. However, this class is marked deprecated and anytime down the line it could be discontinued.

Having said that, I did not find any other alternative to use for pipeline which is as simple as SimpleBuildStep. But, [this blog post](https://jenkins.io/blog/2016/05/25/update-plugin-for-pipeline/) was very helpful in refactoring the SimpleBuildStep-based code to support pipeline.

## Further reading

1. [Plugin development basics](https://www.youtube.com/watch?v=azyv183Ua6U)
2. [How to write Jenkins plugin](http://code.hootsuite.com/how-to-write-a-jenkins-plugin/)
3. [Custom Jenkins plugin development webcast](https://www.youtube.com/watch?v=0tOxGOOZAmE)
4. [post-completed-build-result-plugin](https://github.com/jenkinsci/post-completed-build-result-plugin/blob/master/src/main/java/org/terracotta/jenkins/plugins/postcompleted/PostCompletedRunListener.java)
5. [How to set build result in pipeline](https://support.cloudbees.com/hc/en-us/articles/218554077-How-to-set-current-build-result-in-Pipeline)
