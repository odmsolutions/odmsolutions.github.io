---
layout: post
description: Tip for Dealing with Duplicate Files
tags: [software, linux, tips, duplicate_files, python]
title: Tip for Dealing with Duplicate Files
---
{% include JB/setup %}

Lint, that useless stuff that accumulates in pockets, the bottom of backpacks and ladies handbags. Its annoying, and you computer appears to grow it too.

I was going through my computer, trying to find an ancient document, but because it had not been in any way version controlled (with something like Subversion), there were a few editions, variations and copies. In fact, many of my documents have ended up like that, along with my photo collection and even some of my stored music. This accumulated rubbish was really annoying me. I didn't know which duplicate I should take as the master, or for that matter how many duplicates were simply wasting disk space, and were going to come back and haunt me with a reversion to a change I had made on another copy.

So I was looking at building a python script to find, and list duplicate files. This was during a lack of internet brought on by a misbehaving broadband company, and progress was slow. While the lint annoyed me, it was not enough for me to make this a high priority project.

So, on the day I got internet back, the first thing I did was Googled to see what was out there, and I came across a rather neat tool named fslint. FSlint does what it says on the tin - it finds the lint on your FileSystem (FS). It find duplicates (by name or more importantly size), and it can also find temporary files, as well as empty dirs and badly named files.

FSLint is a gnome based GUI app, so it is relatively easy to use. It was also written with python. At this point I abandoned my attempts and used this, and it turns out that it is pretty good. I don't think it does a real byte by byte comparison, it would be nice if it did a simple first few bytes to be a bit cleverer, but its good enough, and it meant it took only a few minutes to clean up what I had. As it is python on gnome, it can probably be ported to run on windows and mac. I was running it on Linux.

FSLint also has a command line client, and is free, open source and licensed under the GPL. It is adaptable and scriptable. If I ever have an itch to deal with more duplicates, I may even enhance it with the ability to compare the first few bytes.

Enjoy it!

# Links

* <http://www.pixelbeat.org/fslint/> - FSLint project home - Where you can download FSLint
* <http://directory.fsf.org/All_Packages_in_Directory/fslint.html> - Free Software Foundation Directory entry on FSLint
* <http://www.gnomefiles.org/app.php?soft_id=77> - FSLint on GnomeFiles repository
* <http://ubuntu.wordpress.com/2005/10/08/find-duplicate-copies-of-files/> - Ubuntu Blog on Finding Duplicate Copies Of Files

