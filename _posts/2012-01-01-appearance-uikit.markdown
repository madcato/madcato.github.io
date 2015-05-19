---
layout:     post
title:      "Appearance of UIKit"
date:       2012-01-01 11:09:00
author:     "Daniel Vela"
header-img: "img/post-bg-05.jpg"
---


\* iOS 5 required

With appearance kit we can set the default attributes of any UIKit control. This attributes include tint color or background.

## Changing background

NavBar

{% highlight objective-c %}
setBackgroundImage: forBarMetrics:  
    typedef enum{  
         UIBarMetricsDefault,  
         UIBarMetricsLandscapePhone,  
    } UIBarMetrics;  
{% endhighlight %}

UIBarButtons(back button)

{% highlight objective-c %}
setBackButtonBackgroundImage: forState: barMetrics:  
{% endhighlight %}

TabBar

{% highlight objective-c %}
UIImage* tabBarBackground = [UIImage imageNamed:"tabbar"];  
[[UITabBar appearance] setBackgroundImage:tabBarBackground];  
[[UITabBar appearance] setSelectionIndicatorImage:[UIImage imageNamed:"selection"]];  


[<UIControl> appearance] "setAttributte"
{% endhighlight %}

With this invocation we can set the default attributes of any UIKit controls.

![ishop]({{ site.url }}/assets/tumblr_inline_mk0ba3zL1u1qz4rgp.png)
