---
layout:     post
title:      "Xcode breakpoints disabled in Release mode"
date:       2011-02-02 15:19:00
author:     "Daniel Vela"
header-img: "img/post-bg-05.jpg"
---

In the last version of xcode (3.2.5) breakpoints are disabled when debugging the Release version.

To solve this problem go to the Preferences, then Debugging, and uncheck "Load symbols lazily". This fix the issue.  

![Xcode preferences](img/Xcode breakpoints disabled in Release mode.png)