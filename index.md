---
layout: page
title: ODM Solutions
description: Who we are and what we do
---
{% include JB/setup %}

Established in 2010 as a consultancy for automation of processes involved in software development, testing and delivery. 

We believe that time consuming and repetative tasks should be automated, freeing developer, test and integration teams to spend time on improve processes instead of merely repeating them, and to spend time of course on delivering the best software they can.

What things are worth automating? The following list is not exhaustive:

Build and delivery, repetative (not exploratory) testing, endurance (soak) testing, test reporting, other reporting related to software process (including usage tracking and field error reporting), software resource usage visualisation, source control commit validation (does it build? is it broken?), enhancing bug reports with additional data - or automatically reproducing failed tests using builds with instrumentation.


# Contacting us

The easiest way to contact ODM Solutions is to email <a href="mailto:danny@odmsolutions.co.uk">danny@odmsolutions.co.uk</a>.

# Recent Articles

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

# About Danny Staple

Danny is the Director of ODM Solutions, and a skilled IT professional.

## DevOps

Danny has been involved in Dev Ops for over 10 years, being part of early initiatives to embed source control into organisations as early as 2005, to create automated test infrastructure from 2009. He has since then been involved in all stages of software delivery, creating tools to compile software, to improve it's quality and to provide systems to run this.

### Environment Automation

Danny has used docker containers both as a convenient developer aid, and with systems deploying a connected set of containers, in test, staging and live deployments.

Danny has also used Vagrant to create development environments where docker may not be available, getting developers running quickly with the same software, libraraies and set up as their team mates. He is also familiar with the python Virtual Env system for lighter weight local test environments.

He has experience using a collection of tools for automating deployments. Ansible for installing packages, configuring systems and setting up a base layer. Gitlab CI for testing, and automated deployment stages, or using Github actions for deploying built artefacts to an S3 bucket.

### CI/CD Automation

ODM have been working in automation for continuous integration systems with Sky, Cisco and Synamedia since 2010. This is automation of software builds, software testing and delivery into test/integration teams.

ODM has been using Hudson/Jenkins since 2009 and have made contributions to some of the public plugins for the system, as well as being involved in the JIRA/mailing list communities. This includes system admin, extending with Jelly, and building jobs with it.

## Python

Danny been using Python professionally since 2008, both in the workplace with ODM, and in robotics with the Raspberry Pi, having authored the Python book "Learn Robotics Programming".

ODM has used it to build or enhance many things including the automation systems below, Django apps for managing DB data, data file transformation and reporting, hardware monitoring, site-to-site synchronisation.

Other familiar python tools include: Flask, Requests.

See more on how Danny Staple is also using Python to work with robots at <a href="http://orionrobots.co.uk">OrionRobots</a> - stuff with Raspberry Pi and Arduino.

## Test automation

Danny is a test-infected, or even test-obsessed developer, and has been working
closely with a number of automated testing methods:

* Automatic unit testing - mocking, stubbing, optimizing where tests need speeding up.
* Integration testing - bringing components together and testing sections of a full system.
* Full Stack Testing - Testing on hardware.

ODM has experience with the S3 StormTest system since 2010 for testing full stack on STB's.
Danny is familiar with Pythons Unittest, Micheal Foords Mock, VirtualEnv, Pytest and Nose for testing python systems.
Prior to starting ODM, Danny built a system for automating testing of ActionScript with a syntax inspired by Jasmine.js (similar to Mocha) and automated by integration with Hudson (now Jenkins).

He has used Selenium to automate testing of websites and web apps. 


## Build automation

ODM Solutions is able to consult on single step build processes for complex builds involving multiple languages and technologies. This includes working with CI/CD systems to run build, test and deployment steps in a pipeline:

* Gitlab CI
* Jenkins
* Github Actions
* Travis

And a little experience with appveyor. He has built git hook based systems further in the past, but would not recommend this over one of the above systems now.
In terms of supporting builds, he is able to work with:

* Invoke task.py
* Makefiles
* Bash Scripts
* Various scripting languages for transformation.
* GCC

## Report automation and visualisation

Rendering HTML, PDF, Excel or email reports based on test results or other datasets. 

Making single file sharable reports, or dynamic HTML reports from a live backend. This can be dynamic graph systems like Kibana (in the ELK stack), Zabbix, Graphite/Grafana or more static but more elaborate graphs using matplotlib. He has also made 3d visualisations using VPython.

This includes combining elements to make dashboards/wallboards and high visibility displays of data.

## Installation monitoring and management

Tools to monitor automation systems including:

* Django webapps (including CSS + JS with no-refresh screens).
* Zabbix.
* Mysql DB - under Django and raw.
* Familiar with Linux - both Debian and Redhat flavoured distributions.

We are able to install this in a local context at your site, or in a cloud context like AWS.

## Industry participation

Danny Staple is a member of the BCS (British Computer Society), and specifically the following special interest groups there:

* SPA - Software Practice Advancement
* Advanced Programming
* Testing Specialists

Danny has attended PyCon Uk since 2012, and turn up at London Python Group events along with Skillsmatter events.

Danny participates in STEM education support through Orionrobots.

<a href="http://github.com/dannystaple">Danny Staple Public Contributions On Github</a>

## Industry experience

Danny Staple has expert knowledge in the realm of developing software for broadcast and media usage, including applications on Set Top Boxes (DVB - T,S,C), Connected TV Platforms (including Samsung Widgets, Yahoo Widgets) and server side support for these - such as EPG Servers, VOD Metadata servers, usage tracking systems and others.

This includes not only developing apps on these systems, but incorporating automated testing and Continuous integration into our strategies enhancing code quality and confidence. ODM are not only users of BDD, TDD and unit testing frameworks, but actively researching and contributing to this aspect of Software Practice Advancement.

Although Python is Danny's main language, he has developed tools, apps and games in C++, C, ActionScript, Ruby, PHP and Perl - and is able to adapt to languages or tools as needed (at least those that have documentation). ODM's focus is on well designed, maintainable and clean code, with a view to portability given that some apps may need to be run on diverse technologies.


<div class="simplybusiness-insurance-badge" style="width:200px;min-width:200px;max-width:200px;margin:0;padding:0;float:none;-moz-osx-font-smoothing:grayscale;-webkit-font-smoothing:antialiased">
<div style="margin:0;padding:0;border:0;background:none;padding:20px 0;background:#fff;border:1px solid #535353;border-radius:14px 14px 0 0">
<a href="https://www.simplybusiness.co.uk/insurance/public-liability/?source=popBadge" target="_blank" style="margin:0;padding:0;border:0;background:none;text-decoration:none;text-transform:none;text-shadow:none;display:block;text-align:center;text-decoration:underline;font:14px/17px Arial, sans-serif;color:#00827F">
<img alt="Simply Business" height="60" src="https://quote.simplybusiness.co.uk/assets/ci5/sb/badge_logo.png" width="58" style="margin:0;padding:0;border:0;background:none;display:block;margin:0 auto">
</a>
<p style="margin:0;padding:0;border:0;background:none;margin:16px 0 12px;padding:0 15px;text-align:center;font:14px/17px Arial, sans-serif;font-weight:normal;color:#535353;text-transform:none;text-shadow:none">Professional indemnity & public liability insurance provided through Simply Business.</p>
<a href="https://quote.simplybusiness.co.uk/certificate/policy-overview/kV52MG69e57nebG8z2Gwbg/?source=popBadge" target="_blank" style="margin:0;padding:0;border:0;background:none;text-decoration:none;text-transform:none;text-shadow:none;display:block;text-align:center;text-decoration:underline;font:14px/17px Arial, sans-serif;color:#00827F">
View our insurance details
</a>
</div>
<a href="https://www.simplybusiness.co.uk/?source=popBadge" target="_blank" style="margin:0;padding:0;border:0;background:none;text-decoration:none;text-transform:none;display:block;font:14px/35px Arial, sans-serif;font-weight:normal;text-shadow:none;text-align:center;color:#fff;background:#535353;border-radius:0 0 14px 14px">
www.simplybusiness.co.uk
</a>
</div>
