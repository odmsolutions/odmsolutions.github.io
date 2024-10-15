---
title: The Campaign for Stable Software
date: 2024-1014
tags: [software, devops, testing, releasing, CICD, quality]
author: Danny Staple
---
This started as a joke.
People reading this may have heard of CAMRA, the CAMpaign for Real Ale.
It's a British pub culture organisation, who look to verify the quality of beers in pubs and their authenticity as real ale, kept well.
Pub's get badges or plaques to put up when they do it well.

I've lamented how buggy software is - glitches, poor releases, unexpected behavior, undocumented stuff that makes no sense.
Things that mean many people have little faith in software, and for good reason.
I joked, why not a Campain for Stable Software - CfSS. However, instead of a buncha people discussing beer, we talk about what is wrong with lots of software.

As I talked about it with a freind, we wondered if this should be a real thing.
So it starts here.
With a post.
This is not about certification, ISO numbers or management styles.
It's about trying to go so fast that software ends up being released buggy.
With lots of features that are half baked.

I'm going to collect examples. And what could be done about them. What I would do about them!

Look we get it, it's difficult not to have issues.
Software is not, and can never be perfect.
Waiting for perfect is not really ideal, software needs to be released.
However, slowing down to check sily things is a great idea.


## What kinda problems are we talking?

This is Non-exhaustive.
I'm sure it will grow.
I'll also try to cook up (possibly half-baked) solutions and ideas to make things better.

### Glitches

You update a thing, and the authentication stops working.
Or you change a style, and the document does something odd.
The kind of stuff perhaps that should have been caught in testing.
Big websites/apps showing 502 errors directly to consumers, or worse yet 500 errors, because something got broken in prod.
Maybe it was expect behaviour, somewhere in the docs...

## Documentation

Docs say one thing, software does another.
I get it, it is hard to keep documentation up to date.
I am therefore a big fan of executable documentation, or automated validation for docs.
When software is updated (like a staging release is made), testing the documentation against it would be a great idea.
Easier said than done, but this might be a great AI use case.

### Problems collected today

This is always gonna be a shorter list than I really saw. But let's try it.

## Dependabot

Dependabot is awesome for keeping dependancies up to date in a predictable way.
Having dependencies flap about updating without any testing is at best optimistic and at worst a dangerous way to waste time on unexpected faults.
Having a set of validations and tests means that we should be able to put dependency updates in a PR and have it validated.
We can then merge that when it's good, knowing that it should work (depending on the quality of our validation).

Dependabot is far from perfect.
It has issues. 
Todays was it's Nuget feed issue.
If you add a new nuget source to dependabot for nuget, the default nuget.org source, which is usually implied, is no longer present.
This means that you'll not see bumps, or worse still bumps with packages it cant find as dependencies, until the default nuget.org feed is added back in.

```yaml
  nuget-myorg:
    type: nuget-feed
    url: https://nuget.pkg.github.com/myorg/index.json
    username: x-access-token
    password: ${{secrets.my_org_dependabot_token}}
  nuget-org:
    type: nuget-feed
    url: https://api.nuget.org/v3/index.json
```

### Windows 10 Update

Ok - this is now out of date, and replaced.
I'm looking after my sons laptop, which he doesn't update.
Logged in as him, a non-admin user.
I click the "Update" button when updates are available.
Nothing happens.

The problem is he's not admin and can't do that.
My problem with that is windows didn't make that very clear.
Either the button should be greyed out, with tool tip saying "you need admin to do this",
or the silghtly worse idea of having it pop up a dialog saying "You need admin to do this" after clicking the button.

Nothing just leaves people scratching their heads.
This is perhaps a dodgy UI choice? Or is it a glitch?

A ticket somewhere (not sure where) could fix this, but again, it's dated.
However, his computer (a Surface Pro 3) will never support Windows 11. I'm not a great fan of throwing away hardware which is otherwise working well.
I may be looking at a Steam compatible Linux distro for him when updates dry up.

### Github issue filtering and documentation

The documentation at 
[Understanding GitHub Code Search syntax - GitHub Docs](https://docs.github.com/en/search-github/github-code-search/understanding-github-code-search-syntax#is-qualifier) doesn't match the experience. Adding "is:archived" to a search shows all repos, and "NOT is:archived" filters them all.
```
org:my-org NOT is:archived topic:org-topic
```
Will result in no repos.
```
org:my-org is:archived topic:org-topic
```
Still shows archived repos.
This maybe because private archived is something else again from archive? Either way, this isn't quite right.

However, in the issues documentation, [Searching issues and pull requests - GitHub Docs](https://docs.github.com/en/search-github/searching-on-github/searching-issues-and-pull-requests#search-based-on-whether-a-repository-is-archived), "archived:false" works for PR's and issues.

I've raised a ticket with Github to reword that is:archived area.
