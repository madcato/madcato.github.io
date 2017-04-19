---
layout:     post
title:      "How to make a rebase with Source Tree creating only one new commit with new message"
date:       2017-04-19 18:00:00
author:     "Daniel Vela"
header-img: "img/post-bg-02.jpg"
---


If you want to merge two branches- but don't want to keep a separated banch and fixing the messages of branch-, you can use a **interactive rebase**. 

Using **rebase** branches aren't keeped in the repository. Using rebase you can move one branch to the top of another.

![original]({{ site.url}}/assets/original.png) ![rebase]({{ site.url}}/assets/rebase.png)

But **git-rebase** has another fantastic feature **interactive rebase**. With this type of **rebase** you can edit commit messages, even mix several commits into only one. This is very usefull to keep a well documented **git log** without noise.

![feature]({{ site.url}}/assets/feature.png)

To use this method, first checkout the branch you want to rebase(the secondary branch). Then select the last commit of destination branch(the main one). 

![interactive]({{ site.url}}/assets/interactive.png)

**To avoid merge conflicts is very, very important to apply command "Squash with previous commit..." always on top of the commit list after rebase. After all the **Squash** the commits must by ordered**

![squash]({{ site.url}}/assets/squash.png)

[Additional info from atlassian web](https://www.atlassian.com/blog/sourcetree/interactive-rebase-sourcetree)

*In git we trust*
