---
layout: post
description: VSCode - My Current Favourite Editor
tags: [python,programming,editors,ides,tools,vscode]
title: VSCode - My Current Favourite Editor
---
{% include JB/setup %}

# Overview 

Every now and again, I find new tools that I really like. I've been through many editors, Vim and Emacs, I can use Nano where I must. I prefer Notepad++ over notepad, can deal with Leafpad and IDLE.

The last few years, I'd settled on a few favourites for Windows, Mac and Linux in UI. PyCharm was what I used when I needed a full-blown Python IDE - it's a very excellent tool and I highly recommend it. For lightweight stuff, Vim, Notepad++ and Gedit were my selection of tools.

However, I've recently discovered VSCode - Visual Studio Code and it's taken over. It is from Microsoft, and it is fully open source - the code is all on Github.  It's multiplatform - runs on Windows, Linux and Mac. I'm not so sure about older versions of Windows, I've been using on 7 and 10.

# What I like about it

First it is fast. It starts up fairly quickly - about as fast as Notepad++ did. This meant it got reached for more often than Pycharm which can have a massive startup cost.

You can start it up from a terminal with "." to just open the current folder as a project. PyCharm and Textmate both did this. It has git integration that is reasonable too.

Then it's extensible - the whole system is based around Javascript - running in the Node powered Electron (which I've been using for an Orionrobots project). This means that you do not need a compiler to start creating stuff - the plugins are really simple. I've grabbed a few useful ones for Python, Vagrant, file templates while working with it. It comes with decent syntax highlighting anyway, but I've now got click-through code navigation, tab completion that is like intellisense and some refactoring tools. You can debug problems in those plugins by using chrome-developer tools from Electron - also built in.

The configuration and preferences are just json - with a neat side by side editor allowing you to copy the default into your user or workspace preferences and edit them there. These are well documented. You can add task runners via another tasks.json file. This is also well documented too. 

Interaction is via a tool-palette and well documented shortcuts. The tool palette is summoned to run many different command types, and is the default way to find how to do things - if you are familiar with Launchy, Spotlight or the Windows search button - this will be a similar interface.

There is a build in terminal that is reasonably decent.

# It's not perfect

It has a few quirks - the multi-monitor story is a bit awkward at the moment if you want files from the same project on different screens. 

I had to interact with an older SVN project, and the integration was a bit poor there - but this is in an extension - so it will not stay this way.

# Worth trying

I'll perhaps come back with more on the editor - but I would like to suggest trying it if you've not done so, it's fairly refreshing.
My feeling is because it is open source and extensible, quirks like this will be rapidly ironed out. 

The strong leaning to plain old json and not strange complicated preference files and extensions keep this really accessible and it exudes hackability.

# Links

[Download and Try Vscode](https://code.visualstudio.com/download)

