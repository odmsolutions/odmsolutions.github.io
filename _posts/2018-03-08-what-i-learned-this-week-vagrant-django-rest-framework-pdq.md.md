---
layout: post
description: Django rest Framework - Slow Browseable API, PDQ DNS Changes
tags: [django, django-rest-framework, python, pdq, windows, vagrant]
title: Django rest Framework - Slow Browseable API
---
# Django Rest Framework - Browseable API

Today I was working with a Django Rest Framework API, and upon testing an endpoint in a browser, found that this one 
request generated thousands of queries!

I went down a rabbit hole with this, looking at the Serializer to see what lookups it was doing, and which of those may be responsible.

However, the real culprit was that in the browseable API, which the rest framework serves up by default when you go to it with a browser,
the framework places a POST form for you to test with.

The model in question has a Foreign key referencing a table with a large row count.

When this causes the Django Rest Framework Browseable API to do is create a drop down, and then for each item in the dropdown it 
was rendering in such a way that did lookups of other tables - not set up with select_related or prefetch at all.

The dropdown here was not particularly useful. So what I needed to was set the widget it generated here to a text field.

Once I knew what I needed - this was actually surprisingly small as a change - a one liner. 

The serializer was based on a ModelSerializer which provides automatic fields for all models.
What I needed to do was override a serializer with a specific field type.

In my model serializer I added:

    fieldname = serializers.SlugRelatedField(
      queryset=models.ForeignKeyModel.objects.all(),
      slug_field=id, # choose a field here that is easy to paste in - id's work well here.
      style={'base_template': 'input.html'} # It's this line that gives you a text input
    )
    
# PDQ DNS Settings

Another thing I learned this week was about setting the DNS on a Windows Server in PDQ.
We needed to set a couple of nameservers ona  named interface on each host. It being named helped.

This required creating a PDQ package using the `netsh` command in most current versions of windows. Netsh is a tricky beast with many sub-commands.

However, here is the code to modify it from within a windows shell (cmd or powershell):

    netsh interface ip set dns "<Interface name>" static 10.209.62.1
    netsh interface ip add dns "<interface name>" 10.209.62.253 index=2
  
Substitute your own interface names, and 1st/2nd nameserver choice. Note that the first is a `set` and the second `add`. 
I was able then to put this in a PDQ package and run across many servers in our inventory.

# Vagrant

This is more of just a positive rant. If you aren't using Vagrant (or docker) in your project, please do so. I had to replace a laptop 
recently due to a broken screen.

If you have ever been through the process of getting all manner of complex developer tools and dependancies running on a new laptop,
you'll know it can take a long time and much pain.

This time, because the majority of the projects at my client now have a vagrant file, it was a matter of installing Virtual Box, Vagrant, and
then typing "vagrant up && vagrant ssh" in a project to be working with it already. It saves a huge amount of time in getting the laptop
back up to speed. In the case of the Django Rest Framework stuff above - I really didn't have to consider much at all to have that framework
running again for me to develop on with the new laptop. Frankly - it took more effort to pull in my email settings.



