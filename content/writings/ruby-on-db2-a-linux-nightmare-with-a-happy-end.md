+++ 
title = "ruby on db2 a linux nightmare with a happy end"
date = "2007-11-20"
slug = "2007/11/20/ruby-on-db2-a-linux-nightmare-with-a-happy-end"
tags =["Ruby"]
+++

<p>
Although the title might look dramatic, it's pretty close to what I've been through.<br><br>I have set up a Ubuntu 64 bits on my laptop last week to do some tests with Ruby and DB2. Oh man, it is not complicated, is it? It shouldn't be, actually.<br><br>Too sad that I found <a href="http://antoniocangiano.com/2007/11/14/guide-to-setting-up-the-ibm-ruby-and-python-drivers-for-db2-on-linux-32-or-64-bit/" title="Antonio Cangiano's Blog">this</a> so late! It's a post from a friend, <a href="http://antoniocangiano.com/" title="Antonio Cangiano's Blog">Antonio Cangiano</a>, describing the most common problems you may find trying to set up this environment (Linux + Ruby + DB2). You will probably get it working the first time, if you read it <strong>word</strong> by <strong>word</strong>. But if not, here are some extra tips that I can share with you.<br><br>- If you installed Ruby using your distribution's package manager, remove all ruby packages completely. After that, install ruby exactly as described in Antonio's <a href="http://antoniocangiano.com/2007/11/14/guide-to-setting-up-the-ibm-ruby-and-python-drivers-for-db2-on-linux-32-or-64-bit/">post</a>, typing this in the console:<br><pre class="rubycode"><code>$ sudo apt-get install build-essential<br>$ sudo apt-get install ruby-full rubygems</code></pre><br>After that, you may try again.<br><br>- Another problem I found was after getting the driver built. I have written a simple program to try the connection and got this message:<br><br><strong>Failed to load IBM_DB Ruby Driver</strong><br><br>The thing is that this error really means it was not able to find the file libdb2.so.1 in the /usr/lib directory. Issuing this command may settle things for you - it will create the missing symbolic link:<br><pre class="rubycode"><code>$ ln -s /opt/ibm/db2/V9.5/lib64/libdb2.so.1 /usr/lib</code></pre><br>Good luck!
</p>

