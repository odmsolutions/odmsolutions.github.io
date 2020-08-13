---
layout: post
title: Help and Tips For Email Software
description: How do you get the best out of your email software?
tags: [email, getting things done, thunderbird, outlook]
---
{% include JB/setup %}
Nearly everyone uses email, and many find it challenging to manage, overwhelmed by a mountain of messages in their inbox.

In this post, I discuss how to keep your inbox slim so you can see what matters. I show how to set up automatic filters to label stuff up, and how to create quick actions to get it out of the way quickly.

I will discuss different clients and some problems with them, or handy features you can use with them to get them to assist you in wading through a busy inbox. You need never fear a bulging mailbox again!

# Microsoft Outlook Tips 
## The standard business desktop email client 

Microsoft Outlook is the primary mail and calendar client in nearly every office workspace. I have been collecting small tips and tricks to make it work well for me - including things to keep it running smoothly and stuff for GTD activities inside Outlook.

## Outlook PST File Sizes
### What do you do when the dreaded "Your mailbox is too big" message arrives? 

There are two main approaches to this - archive a whole chunk of messages to a pst-file or delete a lot of it.

Deleting mail is easy if there are lots of things which are not mission-critical or covering your own back. It's also good to target messages with large attachments or items from automated services and mailing lists. Deleting is the first best option. But it takes plenty of time, which not all of us sometimes have.

The option of creating an archive PST file and storing it locally instead is an excellent measure to deal with the warning from the admin quickly, and then tackle deleting mail later. Warning - you may need to check the security policies of your workplace on using PST's.

However, when you start deleting stuff - when the archive file gets too big (older outlook version have a size limit of around 2 Gb) or you want to save a bit of disk space, you may notice that the files are not going down.

Here are some steps for successful reduction of Outlook PST Mail Archive file sizes:

* If you find an undeletable item (like a task or something), create a temporary folder, move it to the folder, and move that folder to the trash folder.
* Click on properties for the PST file in Outlook. If you click on "folder size..." you can quickly see which folders are eating the most space.
* Once in a mail view, right-click on the top of the columns, in "arrange by" and select "size". Outlook conveniently groups sizes as "Huge", "Very large", "large", "Medium", "Small" and "Tiny". Go for those "Huge" ones first - they are likely to be multi-attachment mails and Friday afternoon joke circulars.
* Once you have deleted plenty, remember to empty the deleted items folder in the archive area.
* If the file size persists, this is because Outlook tags things for deletion but does not physically remove them. To force this to compact:
  * select the folder, then click on "File". 
  * Click on "Data File Management.." - you will probably need to use the double down arrow to see all. 
  * A screen will pop up, select your data file. 
  * Click on "Settings...".
  * then "Compact Now". Compacting will take a while as Outlook rebuilds the file and its indexes. 
  * Once Outlook completes this - it should have reduced your file size only to reflect what is in the folders.

In the interest of privacy, if you do not compact folders, mail that you sent to the recycle bin and deleted from there may still be retrievable. If you have something you want to remove altogether, I suggest compacting the PST-file and then defragmenting your hard drive - which should improve its chances (but still not guarantee) of being gone. It is worth noting that it is difficult, if not near impossible, to get rid of anything sent in Outlook - as your admins will have logs and backups.

## How to set up Archive/GTD buttons in Outlook 2007 and earlier 
### Adding a button to aid in rapid organising of messages in your inbox. 

If you are interested in GTD, or just want to keep a clean inbox, you will probably be constantly filing off email. Wouldn't it be handy to have some shortcut buttons. Note - this is different in Outlook 2010.

[Add a Gmail-Like Archive Button to Microsoft Outlook - macros - Lifehacker.](http://lifehacker.com/5175347/add-a-gmail+like-archive-button-to-microsoft-outlook)

I adapted it to have "Done", "Pending", "Depending" and "Delegated" buttons as my GTD system holds - that meant a couple of scripts with similar content. Handy to have right above my preview pane.

    Sub done
      Set ArchiveFolder = Application.GetNamespace("MAPI"). _
      GetDefaultFolder(olFolderInbox).Parent.Folders("Done")
      For Each Msg In ActiveExplorer.Selection

          If Msg.FlagStatus = olFlagMarked Then
              Msg.FlagStatus = olFlagComplete
          End If
          Msg.UnRead = False
          Msg.Move ArchiveFolder

      Next Msg
    End Sub
    
If like me you want your pending items to become tasks by adding a task flag automatically then use the following:

    Sub pending()
      Set ArchiveFolder = Application.GetNamespace("MAPI"). _
      GetDefaultFolder(olFolderInbox).Parent.Folders("Pending")
      For Each Msg In ActiveExplorer.Selection

          Msg.Move ArchiveFolder
          Msg.FlagStatus = olFlagMarked

      Next Msg
    End Sub
    

Read the linked article for info on Digital Signing and adding the buttons to your toolbars.

## More on getting the best out of Microsoft Outlook 

Outlook is not just a widely used software tool, it is also very flexible with plenty of different tools and utilities. Finding your way around its feature set can be daunting, so having a guide book can really enhance your productivity when using it.

[Outlook 2010 Quick Reference](https://www.computerworld.com/article/2502795/outlook-2010-cheat-sheet--quick-reference-charts.html)

# Quick - what is GTD?
## Getting Things Done! (and keeping a tidy mailbox)

If you have many things to do in life and are a busy person, sometimes the stuff can seem overwhelming. Having a system to prioritise and quickly filter out stuff that is needing attention is an important tool in tackling it.

Email is a place where stuff to do can quickly pile up, so it is important to chop it down to size regularly. Here is the basic idea:

* Most mail clients support a concept of folders, tagging or labelling. Set up folders/tags/labels for Pending (stuff that will need more attention), Done (stuff you've dealt with), Saved (stuff you need information from) and perhaps Delegated (stuff you are waiting for someone else to do).
* If you can do it quickly - just do it, and send straight to Done.
* If it's just not relevant, delete it. If you find you are often deleting a subscription (mailing list or other), unsubscribe!
* If you know you cannot finish it now, put it in pending - but watch out for that pending becoming too big a dumping ground, I now forward my pending items to a todo list cloud app.
* If someone else can do it (ie colleague, subordinate) then send it to them and drop into your delegated folder.
* Importantly - Keep the inbox clear of all crap. Try to have a clean mailbox once a day. You will find it easier to manage if you do, and you reduce the possibility of missing important stuff.


Reducing the amount of junk clogging up your mailbox will make you feel lighter.

# Mozilla Thunderbird Tips 

Mozilla Thunderbird is by far one of my favourite mail clients. As I have used it for some time, I have got to know some of its quirks and shortcomings, and gathered info and tips to help other users as well as my own reference.

[Get Thunderbird](http://www.mozilla.com/en-US/thunderbird/?from=sfx&amp;uid=0&amp;t=177)

# Sharing a Thunderbird Mail Profile Between Windows and Linux
## Having a mail profile on the go

If you use multiple OS's, and keep Thunderbird as Portable Application on a USB drive, you may wish to share it with a Linux computer without needing to use WINE or some other kind of Windows virtualisation/emulation.

It is worth noting that Portable Thunderbird will run in Wine on recent Linux distro's with pretty much no problems.

Also - this is not the recommended way to share mail. Sharing a profile means that all mail, addons and contacts are synced, however, addons may not work across both platforms. Also, do not be surprised if this introduces issues - especially if different versions of Thunderbird get to the same profile. The recommended way to sync email between machines is to use IMAP accounts. Gmail now supports IMAP, as do many mail hosting places and means that the master list of emails is kept at a server.

If you still are keen to do this, you will need to apply the steps in the article [Sharing a profile between Windows and Linux](http://kb.mozillazine.org/Sharing_a_profile_between_Windows_and_Linux).

The main thrust of it was to copy the mail folders and basic prefs, but leave extensions (which may be OS dependent) behind.

So for future reference, here are the steps (with a few of my own refinements):

* Install Thunderbird on the target Linux machine. Chance are, you already have it, many distro's have it as standard.
* Start it once, so it creates a profile. Cancel when the create account screen is reached.
* Locate the new profile folder on your machine. It will be something like /home//.mozilla-thunderbird/.default/.
* Insert the USB drive with ThunderBird Portable on it. Locate the prefs dir - it should be under /Data/profile. A modern distro will have auto-mounted your drive.
* Symlink shared files to the new profile - this means they will only be available when the drive is plugged in, but will always be synchronised - as they are references to the same files.
** Symlink newprofile/Mail to the target oldprofile/Mail
        `ln -s /Mail Mail`
        This will link the actual mail folders - critiacal for this to work.
        `ln -s newprofile/abook.mab newprofile/abook.mab`
        This links the address books.
* Links the spam filter training with `ln -s newprofile/training.dat oldprofile/training.dat`.
* Copy the `prefs.js` file from the USB drive profile to your new profile.
* Open the new copy of `prefs.js` in a text editor. I recommend gedit unless you are happy and familiar with some other LInux text editor. DO NOT USE A WORD PROCESSOR!.
* Search for and remove any lines with `\[ProfD\]`, which are auto-generated relative paths.
* Now edit all the remaining absolute paths to ensure they use the Mail directory in the new profile.
* Save the prefs.js
* Now start Thunderbird - and all the mail, addressbook and training should be shared.

# Synchronizing Thunderird Contacts lists

If you use Thunderbird on multiple machines, you are likely to want to synchronize those contact lists.
One surefire way to do this is to use a gmail account to sync to with the Zimbra Zindus extension.

* First setup a gmail account if you do not have one
* Then download and install the [Zindus](https://addons.thunderbird.net/en-US/thunderbird/addon/zindus/) extension for Thunderbird
* Configure it to point at your gmail account
* Press the Sync button and your contacts are now synchronized

You will need to install and configure Zindus on each machine you use mail from. Having your contacts synchronized will save some time composing and sending emails on multiple machines.

# Other Thunderbird tip articles
[How to Move Spam to the Junk Folder Automatically in Mozilla Thunderbird or Netscape - About Email](http://email.about.com/cs/mozillatips/qt/et062403.htm)
