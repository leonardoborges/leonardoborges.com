+++ 
title = "eclipse tip debugging non wtp projects"
date = "2009-02-01"
slug = "2009/02/01/eclipse-tip-debugging-non-wtp-projects"
tags =["Java"]
+++

<p>
This is a very useful tip I shared a while ago at the office and turned out to be extremely useful.<br><br>If you work with java and use eclipse as an IDE you know that eclipse has something called WTP, which stands for Web Tools Platform. It's a set of tools and API's to aid in the development of web and JEE projects.<br><br>That means that if you have a WTP project in your workspace, you can deploy, run and debug it straight from the IDE. But what happens if your project is not of a WTP nature?<br><br>Back at the office we have a coupe of really old Java project. WTP didn't exist back then but we do use Eclipse as our IDE of choice.<br><br>So, how do we debug a deployed project that we don't actually deploy from the IDE? As long as you have the source, it is quite simple:<!--more--><br><br>First you need to add a new server form the Server window, if you don't have one already:<br><br><a href='/assets/images/launch_config.png'>{% img /assets/images/launch_config-300x239.png %}</a><br><br>From this window you can add the sources of the project you want to debug. Once done, just drop a breakpoint in your source file and start your server in debug mode.<br><br>You're good to go!
</p>

