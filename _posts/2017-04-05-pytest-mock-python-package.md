---
layout: post
description: Hiding mock traceback innards in pytest
tags: [python, pytest, mock, mocking, testing, unittest]
title: Pytest-mock Python Package
---
When unit testing in python, and using the package mock - which is rather awesomely useful, you sometimes end up with long and
quite unpleaseant traceback. This includes the innards of the mock library when using "assert_called_once_with" or similar mock checks. This is even more unhelpful if the line numbers shown are those at the innards of mock, and it's quite hard to then get back to the actual test that failed.

However, there is a really easy fix for this. The python package "pytest-mock" will cause pytest to treat this all as inner library code, so you get a briefer traceback, showing your mismatch and the lines in your test instead. This makes it far easier to work with. 

  pip install pytest-mock
  
 I'd suggest adding it to your tests/requirements.txt file if you are using pytest and mock, so everyone, and the automation systems running it, produce the simpler tracebacks. It's not impossible you may want to dive into the innards of the mock package, but fairly rare.
 
 
[pytest-mock on PyPi](https://pypi.python.org/pypi/pytest-mock)
