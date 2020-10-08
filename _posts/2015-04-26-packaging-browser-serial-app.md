---
layout: post
tags: [software, packaging, node]
title: Windows Software Frustration
---
I am working  on a project involving a browser based component, requiring some access to desktop services - 
serial ports and the file system.

In terms of requirements I have the following:
1. Must have a relatively recent browser embed (IE 5/6 won't cut it, forget default browser embedded object).
2. Must have serial port access
3. Must have filesystem access
4. Should be a simple setup (close to zero-install) on windows.
5. Works on Linux and Mac too.
6. (optional - but preferred) - user can edit some of the definition files.
7. (really helpful) - CI builds in the cloud.

This rules out a .net app pretty quickly with the final requirement. This app has two target audiences. 
Requirement 4 - for an audience with little, no computer experience and potentially a fairly averse IT setup. 
We are talking 32 bit, and possibly XP only, poor IT support if any, and unpriviledged to install - unzipping and running an exe. 
This is a smaller audience, but the ones that are set to gain the most from the project.

Requirement 5 - is for a larger audience, since the project is intended for microcontrollers, and could do with programmers, having 
the Linux and Mac port make it far more accessible to them. Plus it also means it could potentially run on a PI (although I may have to 
think carefully about the embed choice).

I've tried three methods so far - each with a major shortcoming:

* .net wrapper with CEF (Chrome embedded framework) inside- this is windows only, recent windows at that. Can be built in the cloud on the microsoft VS setup. Rules out the PI, rules out requirement 5.
* chrome app - this works, has far less code that the .net app, and is what I'm currently working with. It works on all the platforms, but requires chrome. Doesn't really work on the PI (that's a really low priority nice to have), can definitely do CI builds. The Chrome installation may make option 4 an issue - the target audience may not be able to install Chrome.
* Node JS Electron- This packages the app as a Node backend, with a CEF frontend. In theory - should satisfy ALL requirements, but in practice, the node SerialPort module, and making a 32 bit windows build seem to be confounding the whole thing. Getting a CI build of this is turning out to be easier said than done - although APpVeyor and MSVS may be options. 

Currently, I'm adding features to the second option - as to move from the second to the third doesn't require much to change in the code. The UI will use the same code, only the SerialPort and Saving code would need to be modified inside the app, and these can be arm's length abstractions.

# Compiling serialport for electron on Windows.

This has been my sticking point. The theory here is that I can ship a directory of resources, modifiable in the way requirement 6 suggests, and 

