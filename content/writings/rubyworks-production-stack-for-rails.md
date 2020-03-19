+++ 
title = "rubyworks production stack for rails"
date = "2007-12-01"
slug = "2007/12/01/rubyworks-production-stack-for-rails"
tags =["Rails", "Ruby"]
+++

<p>
Well, we all know how hard, or at least cumbersome, it can be to set up a production environment to deploy your applications. Besides all the hardware stuff like storages, links, routers you are still left with a huge amount of software configuration to handle. This often includes configuring things like clusters, load balancing and services monitoring - Including notification of interested parts in case of any failure. Pieces of software you have to tie up and make them work together.<br><br>But hey, ruby lovers, you may have a better way to get this going! Released by <a href="http://www.thoughtworks.com/" title="TW's web site">ThoughtWorks</a>, <a href="http://studios.thoughtworks.com/rubyworks" title="RubyWorks">RubyWorks</a> is, as quoted from their website, a production application stack for <a href="http://www.rubyonrails.org/" title="Ruby On Rails">Ruby On Rails</a> applications. I decided to give it a try and I really enjoyed it.<br><br>First of all I didn't want to mess with my actual configuration so I installed a new vm with <a href="http://www.virtualbox.org/" title="Virtual Box">Virtual Box</a>. It has Ubuntu 7.10 on it, with 256MB of memory.<br><br>After installing RubyWorks - instructions on their website -, you get a new skeleton rails app up and running, being served by 4 <a href="http://mongrel.rubyforge.org/" title="Mongrel">mongrels</a> that defaults to production environment! Impressed? There is more. A <a href="http://haproxy.1wt.eu/" title="HAProxy">HAProxy</a> is also set up in front of your mongrel servers acting as a load balancer.<br><br>Well, you probably want to monitor all that stuff huh? A <a href="http://www.tildeslash.com/monit/" title="Monit">monit</a> web interface is waiting for your call on port 2812! It monitors all your mongrel servers - four by default - and your HAProxy, allowing you to measure CPU and Memory usage, among other things.<br><br>The coolest thing here is that all these softwares you would have to setup by hand are already working together, ready for production! Well, is it?<br><br>Going a little deeper, I deployed a database backed application to test this stack's performance.<br><br>I used <a href="http://www.joedog.org/JoeDog/Siege" title="Siege">Siege</a> to stress the app and I am very happy with the results! I compared it with a single mongrel running on production env and no proxy at all.<br><br>It is worth mentioning that having 4 mongrels running took my vm to 77% of memory usage, while a single mongrel took it to 38%.<br><br><!--more--><br><br>The test was made simulating 200 concurrent users on a simple listing page, lasting 1 minute. And the results are:<br>[code]<br>RubyWorks - 77% memory usage<br>--------------<br>Transactions: 1511 hits<br>Availability: 100.00 %<br>Elapsed time: 60.45 secs<br>Data transferred: 3.32 MB<br>Response time: 4.65 secs<br>Transaction rate: 25.00 trans/sec<br>Throughput: 0.05 MB/sec<br>Concurrency: 116.33<br>Successful transactions: 1513<br>Failed transactions: 0<br>Longest transaction: 15.85<br>Shortest transaction: 0.01<br>[/code]<br>[code]<br>Mongrel - production environment - 38% memory usage<br>-----------<br>Transactions: 1460 hits<br>Availability: 100.00 %<br>Elapsed time: 67.96 secs<br>Data transferred: 3.20 MB<br>Response time: 7.33 secs<br>Transaction rate: 21.48 trans/sec<br>Throughput: 0.05 MB/sec<br>Concurrency: 157.57<br>Successful transactions: 1460<br>Failed transactions: 0<br>Longest transaction: 17.78<br>Shortest transaction: 0.01<br>[/code]<br><br>Wow!<br><br>That is a big difference! In less time, with less resources - remember the 77% against 38%? - the out-of-the-box RubyWorks setup was able to handle more requests at a time, and with a lower response time! Even in a machine with very low resources (256MB)!<br><br>This result actually was expected but it was awesome to show that this stack is powerful without touching it and is a very good starting point to tailor your environment, without having to worry about configuring all this stuff. Just focus on fine tuning it, if you need!<br><br>Oh, and by the way, I didn't even put an apache in front of that, which is highly recommended for a prod environment!<br><br>See you on the next post!<br><br>UPDATE 12/1 - 4:25 PM : I fogot to mention that besides all this configuration, it installs ruby and its dependencies as well.
</p>
