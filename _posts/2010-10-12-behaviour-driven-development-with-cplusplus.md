---
layout: post
description: Behaviour Driven Development With C++
tags: [programming, bcc, c++, development, software, behaviour driven development,
  unit testing, tdd]
title: Behaviour Driven Development With C++
---
{% include JB/setup %}
C++ is still considered one of the most powerful and flexible tools for making fast software, especially where other systems like Python, Java or Ruby are not available.

Behaviour Driven Development is a current practice in programming that is changing the way coders are thinking, bringing testing, coding and design closer together, the theory being that things get done right and work sooner, instead of nearly working, being not quite what anybody wanted, and having very little to measure against.

A set of Behaviour specifications, such as the type built with the tool Rspec, growing as functionality is schedule to be introduced to a product, gives a specification that can be run against the code, show where it is deficient, and when other features, or changes are introduced, can quickly highlight a regression. A regression caught as it was created should be relatively easy to find. A regression caught a few months later in end-of-product testing will be much harder to fix, when there is nearly no time left to fix it.

So Behaviour Driven Development is about quality, about confidence in the code doing what it should, about clear communication about what it should be doing so that the tester, coder and designer are all talking in the same language.

C++ is currently less developed in this realm than Ruby or Java, but it is catching up. These tools are being created, and probably need to borrow a little from each other as well as support from both the C++, BDD and Test Driven Development community to start to flourish. They will need to be linked up with CI systems like Hudson or Cruise Control to really fly, but as they are, embryonic, CppSpec and Igloo can both give value to a product.

For more information, a comparison and tutorial, see [C plus plus Behaviour Driven Development tools](http://www.squidoo.com/cplusplus-behaviour-driven-development-tools).
