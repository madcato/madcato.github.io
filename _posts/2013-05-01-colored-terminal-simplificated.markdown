---
layout:     post
title:      "Colored terminal simplificated"
date:       2013-05-01 13:55:00
author:     "Daniel Vela"
header-img: "img/post-bg-03.jpg"
---

Create in your $HOME directory a file named **.bash_profile** and write the following code on it:

{% highlight bash %}
export PATH=$PATH:$HOME/bin   
export CLICOLOR=1   
export LSCOLORS=ExFxCxDxBxegedabagacad   
export PS1='${debian_chroot:+($debian_chroot)}\[\033[1;32m\]\u@\h\[\033[1;31m\]:\[\033[0;36m\]\w$\[\033[0m\] '  
{% endhighlight %}

![colored terminal]({{ site.url }}/tumblr_inline_mm467uUP0m1qz4rgp.png)