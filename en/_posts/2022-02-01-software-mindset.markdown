---
layout:     post
title:      "Software mindset"
date:       2022-02-01 01:00:00
author:     "Daniel Vela"
background: "/img/post-bg-08.jpg"
locale:       en
lang-ref:   software-mindset
---

There is an apparent paradox related to the software we use as programmers. Technically every programmer could create from scratch all the software he needs: but nowadays it is practically impossible to create all that software. We would have to create operating systems, programming languages, compilers, libraries: this is not possible, because it takes too much development time.

However, the opposite option to this is not advisable either. Trying to use all possible software, created by third parties, is also not a good option. First, using third-party software can cause bugs or security flaws to be introduced into your system, or even unauthorized data exploitation: especially if the software is proprietary, rather than "open source." In addition, using third-party software prevents you from learning to program: nowadays programming has become a mere "internet search".

There are many things that as developers we could do, but as engineers we should not. The main reason for this sieve is time. We cannot create everything we need: there is very complex software, such as operating systems and databases, that we must use what is already built: building them from scratch would be a huge job.

Sifting down is easy, there is a lot of base software that needs to be reused. But upwards, what is the sieve? How to differentiate those libraries that should not be used?

Here are some criteria that could be used:
- Never use a library, however convenient and famous it may be, when the operating system or development framework already has a functional alternative. An example would be to stop using Alamofire, because iOS Foundation already has URLSessions, which is more than enough for the whole network thing.
- Never use libraries that are not open source. You need to control what goes into your own project. You have to control the versions, be aware of security updates.
- Never use libraries that do not have a large community of users. This includes having good examples of use, guides and reference: without documentation there is no library.
- Never use a library that solves a key point of your business model. Third-party libraries are often more difficult to adapt and improve than your own. Every business has key needs that software must meet. These needs cause the software to be adapted or improved frequently; therefore it is essential to control software 100%. An example of this would be a sales system: here it is essential to have a shopping cart completely programmed by the company. Using a third-party shopping cart library could introduce limitations that your business cannot accept. Another reason is that, being a key point of your business, it is essential to learn how to do it well. Using third-party software prevents you from learning how to solve problems. A third-party shopping-cart must be used when your business offer other kind of product: a business that sells t-shits, must be a especialist on t-shirts, not in shopping carts; but a company that sells third-party products via an messaging bot, must handle the shopping cart software completely.