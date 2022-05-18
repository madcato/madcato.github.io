---
layout:     post
title:      "To solve retain cycle leak using self inside blocks"
date:       2015-07-06 01:50:00
author:     "Daniel Vela"
header-img: "img/post-bg-05.jpg"
---

{% highlight objc %}
__weak id weakSelf = self;
[someObject someMethodWithBlock:^{    
[weakSelf someOtherMethod];
}] 
{% endhighlight %}