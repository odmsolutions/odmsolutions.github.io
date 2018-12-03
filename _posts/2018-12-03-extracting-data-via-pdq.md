---
layout: post
description: How to Run an arbitrary command on all computers in PDQ, and generate a CSV report from the combined output.
tags: [pdq, windows]
title: Getting CSV Reports From A Comand In PDQ
---
# How to Run an arbitrary command on all computers in PDQ, and generate a CSV report from the combined output.

On some of the servers I work with, the PDQ tool is the route used to automate them. While using other tools (zabbix, ansible) may lead to an easier route to extracting data, it is possible to make PDQ run an arbitrary command on your complete windows server inventory, and turn the output of this into a CSV output for extraction/processing or easy viewing. For those not familiar with it, PDQ is a non-free, Windows GUI based automation system. While I may prefer Config-as-code type tools sometimes the job requires me to make use of the tool available.

It is worth stating this is on PDQ Inventory 12r4, and may differ in newer versions.

The first thing to know is this is a PDQ Inventory operation. Although PDQ Deploy can run commands in a shell step, you will found you have to dig down into each computers run report to see the data. Not ideal for analysis or at a glance information.

To perform this you will need to use the PDQ Inventory tool. Start this up. You will then need to choose an inventory group or "All Computers" and right click on it.

Now from the context menu select Tools->Remote Command. Here you are able to run a DOS Batch or Powershell command on all of the computers in the selected inventory. For best results, try to make a command line that outputs one line of output only. Then click the run button, and you should see the command run on all the machines.

Now return to the main PDQ Inventory window. There is an item in the left tree view "Reports". We will use this to create a report to show us the output of the last command for every computer in one result.
Right click on this and select "New"->"SQL Report".

In the report window, make sure you are in the "Define Report" view. You will need the following SQL:

    select
      Computers.Name as "Computer Name",
      Computers.Description,
      RemoteCommandComputers.output
    from Computers join RemoteCommandComputers on RemoteCommandComputers.ComputerId=Computers.ComputerId
    where <ComputerFilter>
    
You should then be able to click the "Run Report" button to see a table of results showing the computer name, and the last run command. You can click "Save Data To File" to be able to output a CSV of computername, command result.
