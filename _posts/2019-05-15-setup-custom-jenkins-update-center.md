---
layout: post
title: How to setup custom Jenkins Update Center
date: 2019-05-15
type: post
published: true
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
## Jenkins

Jenkins is a popular open source automation tool. Many organizations use it not only to build their projects, but also to test them, and deploy to production. Some developers also use it to automate their day-to-day activities that can be scripted.

## Jenkins Plugins

Jenkins being open source is a great point, but more cool fact is that it is extensible. Yes, you can extend Jenkins’ offerings by installing the plugins available online. Most of them are open source as well. However, there may be situations when you don’t find any plugin suitable for your purpose, or you cannot use the one that is available. In such a case, your next choice could be to develop a plugin on your own! There’s really good documentation available on plugins development. This blog also has a list of [useful resources on Jenkins plugin development]({% post_url 2017-08-13-developing-jenkins-plugin %}).

So, you have developed some Jenkins plugins, which enrich the Jenkins offerings. You are using them in various jobs you have created in Jenkins, and now you want to distribute them, for various reasons. You might want to publish them, so that others outside your organization can make use of them, too! Or, you might have several Jenkins setups within your own organization, where you want to use the same plugin.

To make your plugin available for others outside your organization, you need to make it open source and so that it can be made available through Jenkins Update Center (JUC). But if you are not willing to open source your plugin, or if you only want to distribute them to your own internal Jenkins setups, then the default JUC is not the correct option. Of course, you can do the manual download-upload for plugins installation then, but that becomes cumbersome task over the time. The best choice here could be to setup a custom Jenkins Update Center.

## Jenkins Update Center

Jenkins Update Center is a site used by Jenkins to know what all plugins are available for installation. This is basically a maven repository holding all the plugin files and some JSON files which are referred by Jenkins’ update mechanism. By default, Jenkins always checks at https://updates.jenkins.io/ for plugin updates. in essence, the Jenkins Update Center contains 3 files, and a directory containing Jenkins plugins. The update-center.json file is the main file that contains information about each plugin version available from that update center site.

Since you are willing to host your own update center, you need some mechanism through which you will ask Jenkins to check your own location (in addition to the default one) and manage plugins from there. That can be done using UpdateSites Manager plugin. This plugin lets you add URLs of custom update centers (and optionally, their certificates). We will talk more on this in subsequent sections.

## Creating custom Jenkins Update Center

In order to create your own update center, you will have to generate same set of files and directories, that Jenkins would find at default JUC. The process is quite simple, though. You need followings:

1. a directory containing all your plugins to be published from this JUC
2. a checkout of [this repository](https://github.com/ikedam/backend-update-center2) by ikedam
3. a self-signed certificate, along with its key (both .crt and .key files)
4. a web server to serve static files

You can manage your plugins in that directory the way you want: you can put all of them in different sub-directories, or you can have all of them at single location in flat hierarchy.

The repository you checkout has a really good [wiki page](https://github.com/ikedam/backend-update-center2/wiki/How-to-create-your-own-Jenkins-Update-Center), which you can follow to generate your [self-signed certificate](https://github.com/ikedam/backend-update-center2/wiki/How-to-create-your-own-Jenkins-Update-Center#create-your-certificate) and the [JUC files](https://github.com/ikedam/backend-update-center2/wiki/How-to-create-your-own-Jenkins-Update-Center#generate-update-centerjson). This wiki page uses maven repository as example, but you can simply provide path to your plugins directory. The code is smart enough to run recursively through your plugins directory, detecting each plugin file. This wiki page also uses github pages as the JUC web server. Though, there is no harm using that, you might want to track your plugin downloads, and you might also want to distribute them from your own web server for branding purposes.

Once you run that, you get a couple of JSON files (`update-center.json` and `release-history.json`), and a HTML file (`update-center.json.html`). Simply upload them to your web-server’s document root along with the plugins directory. And you are half done!

As your update center site is up, you can go to `<your site server path>/update-center.json` to check the JSON is being served by your server. Observe all the plugins listed in that file, along with their versions. More importantly, note down the CA certificate mentioned at the bottom of this file. This is the same certificate that you used in command to generate update center files.

## Using your custom JUC

Now, the only remaining part is to tell Jenkins to check your update center whenever it checks for updates. This can be done using UpdateSites Manager plugin. Once you install this plugin, you can add custom update centers to Jenkins. Go to Manage Jenkins > Manage UpdateSites and you should see a form to add update center details.

You need to know:

1. URL to your update-center.json file (the one you used to verify update center is up)
2. ID of your update center (the exactly same one that you mentioned in the command to generate update center files)
3. CA certificate (the one you used to generate update center files)

Add them in appropriate fields, and save. Now go to Manage Jenkins > Manage Plugins, and you should see a “Check Now” at the bottom of the page, click that. Now, as you click that button, Jenkins is going to check default update center first, and then it will check your custom update center for all the plugins available from your site. If everything is fine, Jenkins will start showing your plugins on “Available” tab. Try installing some of them, and the installation should work just fine.
