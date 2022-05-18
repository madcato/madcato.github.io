---
layout:     post
title:      "Recursively remove directories - UNIX"
date:       2011-02-04 19:14:00
author:     "Daniel Vela"
header-img: "img/post-bg-06.jpg"
lang:       en
lang-ref:   recursively-remove-directories
---

To remove directories recursively, you can use the following commnad.

{% highlight bash %}
rm -rf `find . -type d -name .svn`  
{% endhighlight %}

“- type d” is used for directories. Without it you can delete files also.

