---
layout:     post
title:      "Cancel button in UIActionSheet fails when touching bottom half of its frame"
date:       2011-02-03 18:07:00
author:     "Daniel Vela"
header-img: "img/post-bg-05.jpg"
---

Touching the "Cancel" button in an UIActionSheet sometimes fails. This happen when touching bottom half of its frame and also you have an UITabBar in your current view.  

To solve this problem you must add the UIActionSheet to the tabBar view, as:  

	[actionSheet showInView:[YourAppDelegate sharedAppDelegate].tabBar.view];  

...or the current tab bar.  

![]({{ site.url }}/img/tumblr_inline_mjpapsvhMb1qz4rgp.png)
