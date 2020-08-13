---
layout: post
description: How PDQ Could Be Made Dev-Ops Ready (2017)
tags: [windows,automation,devops,tools,scm,git,ansible, pdq]
title: How PDQ Could Be Made Dev-Ops Ready (2017)
---

# Dev Ops Story

In Dev-Ops, it's not uncommon to have many worker nodes. In a particular case, although the majority of my client's system is Unix based, a segment of test nodes require Windows.

Dev-Ops makes much use of automation, thinking like a developer/software engineer by expressing things with code. It also requires ways to configure many nodes to be consistent.

That means dev-ops workers tend to want tools that integrate somewhat with the way they work with code and tools for manipulating their source code.

Automating in Linux has a set of tools. Chef, Puppet and Ansible are some cases. At this particular site, they use ansible for the Linux systems due to ansible being python-based and matching the majority of the site code. The site also benefits from ansible's ability to be used without the target system requiring the installation of an agent, and to a lesser degree the galaxy roles ecosystem.

# What Is PDQ

PDQ is an automated installation and configuration system for multiple Windows nodes. It uses a central server to manage many nodes and uses Windows-specific mechanisms for secure remote access - the equivalent of a secure shell on Linux machines. 

PDQ will install packages in quiet/UI free modes (it can not point and click on UI's). It can run PowerShell or other commands to make changes. 

It also stores installers in a package repository - an advantage over ansible where you'd need a separate system like Artifactory to store those. 
PDQ's installation steps, wizard-driven, will automagically whizz the file over to the target system before running the setup command. 

It has some conditionals and is 32/64 bit aware, so PDQ can run different tasks when things don't match up.

Like ansible, it has an inventory management system with a UI tool to set this up. Running things is done through a different UI, where steps can be configured and targeted at systems.

# Where it could be improved

## Source control/versioning

Ansible scripts are plain-text scripts - they are YAML files, resource files and the rare python extension.
As such, the whole setup can be version controlled in git (pick source control of your choice here). Version control makes it
easy to have an audit of changes, to pick up older versions and
use commits to infer why a specific change was made and when.

Adding the ability to store the configuration (not perhaps the database of exe's and zip's accompanying this) and scripts in git, svn or a choice 
of source control tools would make this a tool much more compatible with a dev-ops way of working.

## Editors

There is a built-in spot for adding PowerShell and other scripts. This editor is useful, as being able to make ad-hoc scripts part of a deployment is essential.
However, the editors are not particularly developer friendly - they appear to be simply notepad.
Embedding something like scintilla, VSCode components, or one of the other familiar editor tools would make a difference. They would have syntax highlighting, understand block-indenting (selection of a chunk of lines and indenting or dedenting the lot) and a few of the standard IDE manipulations.

## File manipulations

Ansible has some simple things like "line in file" and modules specifically for dealing with this. Since some software comes with an existing configuration file, having some quick tools to perform these would save a bit of repetition. These tools could perhaps follow the wizard style of the rest of PDQ, As it stands - you will need to build your own, probably using PowerShell or similar, which would be great if it interfaced with version control.

## Conditionals

As mentioned above, there are simple conditionals based on 32/64 bit and the presence of a file. Some more comprehensive conditions would help though.

A starting point would be "if pattern is in file" - detecting a text pattern in a file, regex capable.
Another would be to base it on what the last step did. Perhaps if the previous step made a change. My ansible experience may be influencing this, where a step can register a "changed" result, and then a later step can use this result to determine if it will run as well. A very common example, suitable also to the windows experience would be "if this file was modified, then restart service <n>".

## A simple text representation

Text representation is a biggie. Wizards are useful - they are a handy way to throw stuff together and reduce a learning curve quickly. However, dev-ops, being development/code-oriented do like to be able to use text-editor to fine-tune things. Having a plain-text representation for the system makes this possible.

Text/code-as-config also feeds into the first point about source control - plain text works well with source control systems. It can be diff'd; it can have lines associated with a particular source control commit.

I would suggest some system like YAML, TOML, JSON or XML. Although INI files could do this - they are perhaps a little simplistic to represent the rich activity configuration available in PDQ. Round tripping between the two would allow workers to stay in their comfort zone, although text usually allows for operations more advanced than a UI would be able to represent.

# In Conclusion

PDQ is a powerful tool and is simple to use. It appears that some pure ops/IT/admin workers like this tool and use it.
It is not a free tool, and perhaps there are free tools that better suit the dev-ops way of doing things. Chef, Puppet and Ansible have some windows support.
The chocolatey package manager may eliminate having to fuss around finding the installers for at least common free-to-download packages. 

Since ops prefer this system, making it perhaps more developer-friendly will allow the two groups to work more closely together or curse each other less, and continue to use the PDQ tool throughout. Which is perhaps the point of Dev-Ops?
