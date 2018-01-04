---
layout:     post
title:      "Save custom objects in NSUserDefaults"
date:       2011-07-04 13:29:00
author:     "Daniel Vela"
header-img: "img/post-bg-03.jpg"
---

To store objects in **NSUserDefaults** must use the class **NSKeyedArchiver**:

{% highlight objc %}
+(void)saveCustomObject:(NSMutableArray*)object forKey:(NSString*)key  
{  
    NSUserDefaults *prefs = [NSUserDefaults standardUserDefaults];  
    NSData *myEncodedObject = [NSKeyedArchiver archivedDataWithRootObject:object];  
    [prefs setObject:myEncodedObject forKey:key];  
    [[NSUserDefaults standardUserDefaults] synchronize];  
} 

+(NSMutableArray*)loadCustomObjectWithKey:(NSString*)key  
{  
    NSUserDefaults *prefs = [NSUserDefaults standardUserDefaults];  
    NSData *myEncodedObject = [prefs objectForKey:key ];  
    NSMutableArray *obj = (NSMutableArray *)[NSKeyedUnarchiver unarchiveObjectWithData: myEncodedObject];  
    return obj;  
}
{% endhighlight %}