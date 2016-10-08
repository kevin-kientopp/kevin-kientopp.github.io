---
layout: post
title:  "Unfreeze Ubuntu on Wakeup"
date:   2016-10-07 21:08:30 -0600
categories: ubuntu
---
Lately, I have been experiencing freezes in ubuntu. I am not 100% sure, but they seem to occur after waking the computer after sleep.

A workaround I have found that seemed to work is to:

1. Switch to a text VM.
2. Login and run pm-suspend.
3. Wake up the computer.
4. Switch back to the VM running X.

Now, a bit more detail on how each step is done.

You can switch to a text VM with ctrl+alt+f1 through f6. Each function key is a separate VM. Note, this make take a while.

Login and run:

{% highlight shell %}
$ sudo pm-suspend
{% endhighlight %}

Your computer should go to sleep.

Wake the computer up, then switch back to the VM running X with ctlr+alt+f7.

No idea if this will work every time, but it just worked for me.

This was done connecting Ubuntu 16.04.
