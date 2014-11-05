---
layout: post
title: Devops Thoughts On Culture And Philosophy - Why Abstract, Automate or modularise?
tags: [devops, progamming, coding]
---
Why do we want to abstract? to simplify? To hide processes, chunks of functionality or protocols (at least until we take a look)?

It is not because we don't ever want to look at or learn the underlying process. If you think this is because you never want to RTFM, or learn a bit of assembler, or get your head around an RFC, then this is the wrong reasons.

It is however because I have a job in hand, another goal, or my automations are intending to assist someone else towards theirs. If your goal is not to learn assembler right now, and to get whatever feature, tool, project or app doing something with the least amount of pain and mess ups, then it makes sense to use higher level tools and abstractions to get on with it.

If you are a C-coder building your app, you probably would rather be thinking about and trying your algorithm, than how your compiler source looks, how your build system runs or how the ALU you are running on handles instructions. There may come a time when you will need that information, in which case its reasonable to expect an engineer to seek the help or knowledge they need for that.

I'll take the highest level language I can, until I find it won't work - in which case, it may be fixable without entirely going low level. Why - because I'll be able to do it faster, and be using abstractions I'll have used before, and will use again. 

When I am writing a system to crunch data, I'll stay high-level. If it needs to be faster, I'll profile to find the bottlenecks before rewriting in a higher level language - because in the grander scheme of things, gross architecture and duff algorithms will account for more than your calling convention overheads.
 
Don't use dev-ops because you refuse to learn about something. Don't use OO or modular code and information hiding principles because you never want to see the black box. Use them because right now, today, this is not relevant, and you are not writing that thing, but satisfying some other goal. Because remaining focused on that goal is what is important.

This is why ultra-high-level systems to build servers are handy, Juju, Docker (and perhaps Cobbler? not sure), because I want to test and deploy my app. Frankly the contents of the /etc file system are not that important to it today. It doesn't mean I cannot or I am incapable of rolling my own linux distro from source (personally I am quite familiar with the etc system, building from source and systemV stuff, systemd not so much yet). It means that today, right now, my cool shiny toy is what its about.

Keep it simple, for you and for others - if you can use the highest level abstraction, writing the least code, providing the most protection from mess ups, you will do so and save time. Don't fear the lower levels - be prepared to dive in should you need to.

<hr>
There is a caveat - don't make abstractions convoluted, complex, nebulous and billowy - if they obfuscate the task instead of simplifying it - you've got it wrong. If it leads you to repeating information in many places, writing the same code n times, it may not be the tool you are looking for. That's fine - change it. It you are actually wearing a devops or automation hat, you will want to have a fairly wide and early adopter attitude to tools, while being comfortable with the ancient and sturdy ones too (on the one hand sed, on the other Juju). This way you have a good mental repertoire to throw at the problems.
 