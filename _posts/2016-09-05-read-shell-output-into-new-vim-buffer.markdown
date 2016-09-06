---
layout: post
title:  "Read Shell Output Into New Vim Buffer"
date:   2016-09-05 18:06:20 -0600
categories: vim
---
While in vim, you may want to run an external command and use the output. One way is to do the following.

{% highlight vim %}
:new | r !ls
{% endhighlight %}

The `!ls` runs the external command `ls`. The `r` reads the output of the command and places it under the cursor. The `new` creates a new buffer in a split window, and places the cursor there.

The result is a split window containing the output of the external shell command.

This was done using Ubuntu 16.04 LTS and Vim 7.4.
