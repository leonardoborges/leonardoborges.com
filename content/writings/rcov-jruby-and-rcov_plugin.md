+++ 
title = "rcov jruby and rcov_plugin"
date = "2009-05-05"
slug = "2009/05/05/rcov-jruby-and-rcov_plugin"
tags =["JRuby", "Rails", "Testing"]
+++

<p>
The <a href="http://github.com/commondream/rcov_plugin/tree/master" target="_blank">rcov_plugin</a> project is a rails plugin for <a href="http://eigenclass.org/hiki.rb?rcov" target="_blank">rcov</a> that adds some useful rake tasks to your application.  And since I'm currently working in a JRuby project it made sense to use this plugin.<br><br>The thing is, among other stuff, an rcov report from a JRuby project includes some files that shouldn't be there at all, plus you also need to change the way you call rcov as such. Thus, I thought I'd contribute these changes to the plugin and my pull request was approved this morning - just install the latest version and you should be good to go.<br><br>It was useful for us here, hope it might be useful for you too.<br><br>Enjoy :)
</p>

