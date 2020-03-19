+++ 
title = "rails performance scripts profiler benchmarker"
date = "2008-11-20"
slug = "2008/11/20/rails-performance-scripts-profiler-benchmarker"
tags =["Performance", "Rails", "Ruby"]
+++

<p>
There are several ways you can measure your rails application's performance. The techniques range from filling your code with "puts" statements - :p - to fancy ones like <a href="http://www.newrelic.com/">NewRelic</a> - which is quite nice, I must say.<br><br>But what many people don't know is that rails ships with a handful of scripts to help you out. One of which is called <strong>profiler</strong>, located under your application's <strong>scripts/performance</strong> directory.<br><br>By default it uses the standard ruby profiler but if you want more speed - and additional reporting options - , consider installing the <a href="http://ruby-prof.rubyforge.org/">ruby-prof</a> gem.<br><br>So if you execute it without params, you'll get a clue of how it works:<br><br><pre lang="bash"><br>$ script/performance/profiler<br>Usage: ./script/performance/profiler 'Person.expensive_method(10)' [times] [flat|graph|graph_html]<br></pre><br><br>Pretty self explanatory, right?<br><br>As a sample code, I have in my rails app a dumb model with a really dumb method I wanna profile:<br><br>

<div class="code">
  <pre><code class="language-ruby">
  class Article
    def self.find_all_with_delay
      sleep 10
      self.find(:all)
    end
  end
  </code></pre>
</div>
<br><br>Clearly this method doesn't perform well and is a bottle neck in our super application! But let's see what rails' profiler tells us:<br><br><pre lang="bash" line="1"><br>$ script/performance/profiler 'Article.find_all_with_delay' 1 graph > text_graph.perf<br>Loading Rails...<br>Using the ruby-prof extension.<br>Thread ID: 109440<br>Total Time: 10.147995<br><br>  %total   %self     total      self      wait     child            calls   Name<br>--------------------------------------------------------------------------------<br> 100.00%   0.00%     10.15      0.00      0.00     10.15                1     Global#[No method] (/Users/leo/projects/test/vendor/rails/railties/lib/commands/performance/profiler.rb:24}  /Users/leo/projects/test/vendor/rails/railties/lib/commands/performance/profiler.rb:24<br>                     10.15      0.00      0.00     10.15              1/1     Object#profile_me<br>--------------------------------------------------------------------------------<br>                     10.15      0.00      0.00     10.15              1/1     Global#[No method]<br> 100.00%   0.00%     10.15      0.00      0.00     10.15                1     Object#profile_me ((eval):1}  (eval):1<br>                      0.00      0.00      0.00      0.00              1/1     Class#const_missing<br>                     10.15      0.00      0.00     10.15              1/1     <Class::Article(id: integer, name: string, content: string, created_at: datetime, </p>

