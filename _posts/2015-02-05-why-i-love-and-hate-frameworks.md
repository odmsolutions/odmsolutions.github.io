---
layout: post
title: Why I Love and Hate Frameworks
tags: [programming, libraries, frameworks, rants]
---
I love frameworks, and I hate frameworks. I think in many cases, most developers should try and use them, but they can be a double edged sword and introduce unwanted problems. This applies also to libraries, tools, suites of stuff and other-peoples-code in general. On the whole - this mostly applies to Open Source frameworks, but some principles apply to closed source tools too.

# Why I Love Frameworks - Building on the shoulders of giants

Frameworks and Libraries can mean that you save hours or months of work. Reinventing the wheel is generally a bad thing, and trying to solve what is a many-times-solved problem is a waste of time and resources. And I hate duplication. Unless you know the problem domain well - you may end up building a poor mans copy, a shadow of what the real domain is, or a very crude implementation.

# Why I hate frameworks - square peg, round hole

One gotcha is that problem space may not be an exact match of yours. You may find that it is a close fit, but a little outside what you really intended.

# Why I love frameworks - reusable skills

If you use a framework that is widely known, you can take your knowledge and use that framework to solve it again. You will be able to find other people with skills in that framework. This is something that would take time for someone to learn for your own implemenetation of a domain.

# Why I hate frameworks - upgrades and api changes

This can be nightmarish cold sweat. You need some feature or bug fix they have, but an upgrade requires system wide changes in your code to accomodate the changes in philosophy that the framework developers have made. If you are lucky they will backport really important fixes, or really useful parts. But don't count on it.

# Why I Love Frameworks - They Have solved a bug you've yet to find

A framework that is maintained by a community, and has a certain amount of time and experience in developing would have found, investigated, tested and solved bugs you may never have found. 

# Why I hate frameworks - They can introduce bugs of their own

The developers on the framework have a working knowledge of code you've barely seen. A change you make may actually behave differently in that code from the way you expect,and it may take diving deeper than you wanted to into that code to fix it.

# Why I love frameworks - Solve a bug once

If you track a bug down to a bit of code in the framework, and submit a fix, then it is fixed for all users of the framework when they upgrade (see above) to it. This means many people benefit.

# Why I hate frameworks -  Bloating, nebulous complexity

Sometimes a framework is just to heavy, complex and slow for what you need - it is massive overkill. Some start off small and sweet, and grow into Baroque structures. 

# Why I love frameworks - The solution you'd not considered

It takes a lot of effort to find elegance in code, simplicity and brevity for expressing a concept does not come naturally, and a great deal of code I've seen from other people (including in some frameworks and libraries) is very much a brain dump into a single source file or function. But the best frameworks have resulted from people arriving at a very neat way to express things, a way of make 3 lines of code do what 500 used to do. While the 500 lines is still there buried int eh frameworks implementation, many 3 line snippets will use it. 

For the most part you can treat the other bit as a black box - the very reason that in computing the means of abstraction, and the means of composition are fundamental.

# Contribute code

If you have a neat idea, a way of expressing things that makes more sense than what you've seeen, or a way to enhance a framework, then pelease do publish it. If you know you can write code better than the code in the frameworks, then you should be writing frameworks. If you know you trust your hand assembled code in all the places you'd use a compiler - you should consider being a compiler writer. Frameworks are not the "best code ever written", and some very far from it, but they are a product of knowledge pooled and shared - by far the best way in which humans progress.
