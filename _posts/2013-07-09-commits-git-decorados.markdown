---
layout:     post
title:      "Commits de git decorados"
date:       2013-07-09 20:27:00
author:     "Daniel Vela"
header-img: "img/post-bg-04.jpg"
---


Para ver los commits de un repositorio git de forma molona.

{% highlight bash %}
git log --graph --decorate --pretty=oneline --abbrev-commit --all
{% endhighlight %}