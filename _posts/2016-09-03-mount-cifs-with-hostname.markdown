---
layout: post
title:  "Mount.cifs With Hostname"
date:   2016-09-03 15:05:07 -0600
categories: jekyll update
---
You have a windows share named _sharename_. You know the ip address and you want to mount it.

{% highlight shell %}
$ sudo mount -t cifs //192.168.0.10/sharename /media/sharename \
-o username=windows-username
{% endhighlight %}

Works perfectly! But you like to use hostnames and have the ip mapped in your /etc/hosts:

{% highlight conf %}
192.168.0.10 windows.pc
{% endhighlight %} 

You unmount then try to remount using the hostname.

{% highlight shell %}
$ sudo umount /media/sharename 
$ sudo mount -t cifs //windows.pc/sharename /media/sharename \
-o username=windows-username
{% endhighlight %}

But you receive the following error!

{% highlight shell %}
mount error(5): Input/output error
Refer to the mount.cifs(8) manual page (e.g. man mount.cifs)
{% endhighlight %}

Not the most descriptive error if you ask me. But, as they suggest, if you refer to the manual page, the answer is there.

{% highlight text %}
vers=
   SMB protocol version. Allowed values are:

   ·   1.0 - The classic CIFS/SMBv1 protocol. This is the default.

   ·   2.0 - The SMBv2.002 protocol. This was initially introduced in Windows Vista Service Pack 1, and Windows Server 2008. Note
       that the initial release version of Windows Vista spoke a slightly different dialect (2.000) that is not supported.

   ·   2.1 - The SMBv2.1 protocol that was introduced in Microsoft Windows 7 and Windows Server 2008R2.

   ·   3.0 - The SMBv3.0 protocol that was introduced in Microsoft Windows 8 and Windows Server 2012.

   Note too that while this option governs the protocol version used, not all features of each version are available.
{% endhighlight %}

So you try again with the vers option.

{% highlight shell %}
$ sudo mount -t cifs //windows.pc/sharename /media/sharename \
-o username=windows-username,vers=3.0
{% endhighlight %}

Huzzah! It works!

This was done connecting Ubuntu 16.04 LTS to a Windows 10 pc. No guarantee that this will work in other scenarios, but I imagine that it would.
