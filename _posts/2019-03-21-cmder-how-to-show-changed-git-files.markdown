---
layout: post
title:  "Cmder: how to show changed Git files"
date:   2019-03-21 15:25:00 +0100
categories: 
---

From the [cmder website](https://cmder.net/):

> Cmder is a software package created out of pure frustration over the absence of nice console emulators on Windows. It is based on amazing software, and spiced up with the Monokai color scheme and a custom prompt layout, looking sexy from the start.

Cmder is my favorite terminal emulator for Windows, and my use has been born out of the benefits it provides over using the standard `cmd` and `powershell` terminals.

However, Cmder is a tad spartan when it comes to showing the amount of changes when you're in a directory holding a Git repository.

Note: this does not apply to `powershell` terminals.

# Showing Git changes
## Default behavior

When adding a file and removing a file from the working directory, the terminal prompt shows that _something_ has changed (and on which branch).

![adding-and-removing-a-file-default](https://imgur.com/download/3d9KIpP)

This could benefit from showing a bit more information. For instance, it would be great if our terminal window would also indicate _what_ has currently been changed.

## Improved behavior

Using a gist [I found on GitHub](https://gist.github.com/nielsabels/2958e8128e63f9c76020efcd21c968f1), more insight can be gained about the changes in the current working directory.

![adding-and-removing-a-file-improved](https://imgur.com/download/bRxEshC)

With the addition of the script, we're looking at the amount of files changed. Specifically, in green, we see which files have been added (+), modified (~), deleted (-) from the current index (read: _staged for commit_).

In red, we see the same numbers regarding added, modified and deleted files. These changes are scoped to the currently _untracked_ files in the working directory.

## How it works

The [following line in the script](https://gist.github.com/nielsabels/2958e8128e63f9c76020efcd21c968f1#file-git_peek-lua-L356) executes a command using the standard Git command-line tooling:

```
git -c color.status=false status --short 2>nul
```

The output of the command is translated into the graphical representation on the command prompt. Look below to see them in action simultaneously.

![git-c-and-status-example](https://i.imgur.com/EMjpvht.png)

## How to apply the script

Save the contents of the script into a file (e.g. `git_peek.lua`).

Find the directory where Cmder is installed, and place the file into `/config`.

You're done! The script will be executed when Cmder starts up.

# Credits

This script was not written by me and credits go to the original author. I'd like to [thank the author](https://gist.github.com/mattdkerr) for [the gist](https://gist.github.com/mattdkerr/23db4db40c276b1481b01b0fa26de009) that the above post is based on.
