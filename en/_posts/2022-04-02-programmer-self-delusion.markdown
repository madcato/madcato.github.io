---
layout:     post
title:      "The programmer's self-delusion"
date:       2022-04-02 01:00:00
author:     "Daniel Vela"
header-img: "img/post-bg-13.jpg"
locale:       en
lang-ref:   programmer-self-delusion
---

Throughout my professional life as a programmer, I have very often come across ideas that all my colleagues defend, but none of them have asked themselves the reason for that idea. Sometimes when someone complains to me that I have programmed something wrong, they ask why we should do it that way: in most cases I didn't received an answer, in which I do, when I asked the why of the why, then there is no answer.

Richard Dawkings coined the term ["meme"](https://en.wikipedia.org/wiki/Meme) to refer to this very thing. A ["meme"](https://en.wikipedia.org/wiki/Meme) is an idea that everyone tell it, because they believe it is the truth; and it is believed its veracity, because everyone tell it that same way; that is, it is a circular explanation: A is B, because B is A, and therefore A is B. This is a fallacy in which we continually fall, due to our ease of confusing cause with effect.

It is largely motivated by social pressure, which emotionally forces us to believe and say the same thing
that everyone believes and says. There are documented psychological studies where several participants (all but one participant are part of the investigators) were asked a question, to which they answered with a very obvious lie; when asking the same question to the subject who was not an investigator, -surrounded by the investigators and having heard their answers-, he answered the same obvious lie as the rest.

If this happens to us with obviously false beliefs, what can we do with ideas that are not so easily verifiable!

I offer a couple of examples to illuminate this criticism.

Many ["lint"](https://en.wikipedia.org/wiki/Lint) tools recommend not to create code files with more than 1000 lines, or something like that. What do we programmers usually make when we find a huge file? We split it into two smaller ones by distributing the code between the new files. We don't even ask ourselves what the intention of this recommendation is, which is not to have small files for nothing, actually having very large files is an indication (note: an indication, not a certainty) that the architecture of that solution does not it is well segregated, causing the code to accumulate in a class or module. In other words, the correct solution would be to analyze if we can find a better, simpler and clearer architecture. But if we don't find it, separating the functions into two smaller files is not a solution, but another problem, since we make it difficult for the programmer to find the functions and variables within the code as they are separated.

Another example of an idea that we assume without giving it much thought is the following: "code comments should say the why of the code and not the what and how do it". Well, it is not like that, the "why" of a code is its requirements, which should never be written in the code since they are almost always changed continuously and must be available to project management members without access to the code. The "what" and the "how" is essential to understand the source code. It is evident that many projects have documentation that explains what the library or API does, as well as usage examples and guides that explain how to use them. The best, most experienced programmers all recommend documenting your code.

You will sometimes hear that well-written code is self-explanatory about what it does and how, but this is just "wishful thinking": it is something we would like to see happen, and many programmers believe they are capable of doing it, because they look at the code had just write, and they "get" it. But the truth is that the source code is always a sequence of information destined for a machine or compiler to process: trying to create code that other people understand is making your life difficult. Most programmers who claim to "understand" their newly written code are unable to really understand it after two months.

In short, we programmers suffer from an enormous lack of basic principles and scales of values ​​that allow us to make decisions. We know that it is very important to have these tools for our work, to the point that we assume apparently good principles (such as DRY, SOLID, Agile principles), without even analyzing them, and therefore without finding their many exceptions and limitations. But no, we are going to find the principles we need in a programming manual, we will probably find them in other disciplines, such as classic books, books on ethics, history, even in novels (the best of them are full of ethical codes that can help us).