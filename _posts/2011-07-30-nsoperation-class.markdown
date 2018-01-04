---
layout:     post
title:      "NSOperation class"
date:       2011-07-30 21:00:00
author:     "Daniel Vela"
header-img: "img/post-bg-02.jpg"
---

NSOperation is useful for asynchronous executions:

{% highlight objc %}
@interface MyOp : NSOperation  
@end  
@implementation MyOp  
-(void) main {  
// Your work goes here  
}  
@end  
{% endhighlight %}
Sample usage:

{% highlight objc %}
NSOperationQueue = [[NSOperationQueue alloc] init];  
MyOp* op = [[MyOp alloc] init];  
[queue addOperation:op];  
{% endhighlight %}

20110324.21