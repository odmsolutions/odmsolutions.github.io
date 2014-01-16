---
description: Bulk renaming files in Windows and other GUI's
tags: [windows, xp, svn, subversion, bash, sed, cygwin, cvs, gui, osx]
title: Bulk renaming files in Windows and other GUI's
layout: post
---
{% include JB/setup %}

One shortcoming of working in a Windows environment is not being able to bulk rename files as easily as in unix, or even DOS. I am also not even sure Gnome or KDE have really taken great measures to sort this out.

In unix, the use of sed with a little shell magic gave full regular expression file renaming, and can be linked with most other tools - including Subversion (SVN) and CVS. In DOS, the ren command could deal with wild card replacement, however, the standard windows explorer bulk rename, which consists of highlighting a group of files, and renaming one of them, was extremely weak, allowing the initial name and then every repeat name being the same with a bracketed auto-numeric expression.

So I hit the web to find a serious renaming tool, and found a little cache of freeware tools to do the job:
[List of multiple file renaming tools.](http://www.freewarehome.com/System_Utilities/File_Management/Multiple_File_Renaming_t.html)
   

After looking around, I tried 1-4a rename, a simple but powerful tool with reasonable pattern matching and replacement, autonumbering (with padding), and it has possibilities of hex numbering (handy for some programming situations), case changing, and song pattern naming for media collections.

The only shame really is that the tool does not link with SVN, and that the source control UI's for windows do not have any kind of bulk rename. Maybe Tortoise SVN or Rapid SVN could consider adding one to their arsenal, which would increase their usefulness when looking at directories full of image files or similar items that may need renaming. Its not an operation that one should plan to do often, but it also need not be so painful.

For those unix bods - here is an example shell script to do this (which I ended up using in Cygwin bash in the end because it had to happen with SVN):

    for currentfile in blah*.bmp
    do
      newname=`echo $currentfile | sed 's/blah/something_else_/;s/_\([0-9]\)\./_0\1\./'`
      echo ${currentfile} \-\&gt; ${newname}
      svn rename ${currentfile} ${newname}
    done

The Windows scripting host may offer another (equally non user-friendly) way to do this without Cygwin.

GUI tools for these would be nice, although regular expressions are not user friendly. What ideas are there for giving such pattern matching power in a user friendly manner? I would love to hear some, and I hope somebody somewhere is juggling the concept of it.

The best I have seen is the Apple OS X Automator. I am not sure if SVN actions can be placed in it, but user friendly expression base renames can most definitely be put in. Perhaps Gnome and KDE will follow suit there, and eventually we will see something similar in Vista.

# Links

* [Freeware Windows renaming tools list](http://www.freewarehome.com/System_Utilities/File_Management/Multiple_File_Renaming_t.html)
* <http://svn.tigris.org> - Subversion home on Tigris, including info on Rapid SVN and Tortoise
* <http://www.1-4a.com/rename/> - 1-4 Rename (Windows bulk renamer) home
* <http://www.cygwin.com> - Cygwin home
* <http://www.apple.com/macosx/features/automator/> - Information on OSX Automator


