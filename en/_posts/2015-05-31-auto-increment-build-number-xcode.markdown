---
layout:     post
title:      "Auto-increment BUILDNUMBER for Xcode Projects"
date:       2015-05-31 17:28:00
author:     "Daniel Vela"
background: "/img/post-bg-01.jpg"
locale:       en
lang-ref:   auto-increment-build-number-xcode
---

This snippet was extracted from [https://gist.github.com/sekati/3172554](https://gist.github.com/sekati/3172554)

{% highlight bash %}
# xcode-build-bump.sh
# @desc Auto-increment the build number every time the project is run. 
# @usage
# 1. Select: your Target in Xcode
# 2. Select: Build Phases Tab
# 3. Select: Add Build Phase -> Add Run Script
# 4. Paste code below in to new "Run Script" section
# 5. Drag the "Run Script" below "Link Binaries With Libraries"
# 6. Insure that your starting build number is set to a whole integer and not a float (e.g. 1, not 1.0)
 
buildNumber=$(/usr/libexec/PlistBuddy -c "Print CFBundleVersion" "${PROJECT_DIR}/${INFOPLIST_FILE}")
buildNumber=$(($buildNumber + 1))
/usr/libexec/PlistBuddy -c "Set :CFBundleVersion $buildNumber" "${PROJECT_DIR}/${INFOPLIST_FILE}"
{% endhighlight %}