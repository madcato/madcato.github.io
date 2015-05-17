---
layout:     post
title:      "iPhone - Splash screen"
date:       2011-02-09 16:03:00
author:     "Daniel Vela"
header-img: "img/post-bg-01.jpg"
---

Declaration(.h):

{% highlight objective-c %}
UIImageView *splashView;  
{% endhighlight %}

Implementation(.m):

{% highlight objective-c %}
splashView = [[UIImageView alloc] initWithFrame:CGRectMake(0, 0, 320, 480)];  
splashView.image = [UIImage imageNamed:@"Default.png"];  
[window addSubview:splashView];  
[window bringSubviewToFront:splashView];  
// Do your time consuming setup  
[NSThread sleepForTimeInterval:2.1];  
[splashView removeFromSuperview];
{% endhighlight %}