---
layout: post
description: Bash strict mode and logical experessions
tags: [bash, shell, linux, unix, macos]
title: Bash strict mode and logical experessions
---
TLDR; In strict mode `command a && command b` will *not* exit if `command a` produces a non-zero exit code, unless you put brackets around it!

## Strict mode - a bit of background

When writing shell scripts to process things, I feel it is important to ensure that the script does not continue trying to process anything if assumptions you've made about your environment are incorrect, or if a command produces an unexpected error code.

It is for this reason that I often add the following at the top of a script:

```bash
set -eu -o pipefail
```

The `-e` means that bash will exit on error. `-u` means that trying to expand from a variable that doesn't exist is considered an error. `-o pipefail` means that these options persist in pipe or subshell statements.

I do this as a defensive coding stance. I've seen some pretty bad things happen from code that assumed variables were set or a previousline was ok when it wasn't. Sure, you could expect people to remember to check every return code, and every variable. But they would forget.

## The unexpected behaviour

It's not uncommon to see a command sequence `command a && command b`. This should be read as:

```pseudocode
run command a
if command a didn't fail:
  run command b
```

For this purpose, it will perform as expected. However, the following script has a subtlety:

```bash
set -eu -o pipefail

false && echo "ran this bit"
echo "Still here"
```

The comamnd `false` always produces a non-zero exit code. So we can definitely expect that `echo "ran this bit"` will not run. But the question is, with `set -e` in play, do we expect the output `Still here` to be produced?

In this case, you should expect that output. What has happened is that the condition has effectively "handled" the error code, so it is a handled error condition, so the script will not exit.

## But I want it to exit?

To make this exit, you can contain the expression in a subshell. The following script demonstrates the variations on this:

```bash
#!/bin/bash

set -eu -o pipefail

# This line will continue
false && echo "ran this bit"
# This line would die
(false && echo "ran this bit")
# This line will also die
false; echo "ran this bit"

echo "Hello"
```
