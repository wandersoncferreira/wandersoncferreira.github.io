---
title: "emacs - automation don't need to look pretty"
author: ["Wanderson Ferreira"]
tags: ["blog"]
draft: false
---

One of the great strengths of Emacs for me is that my configuration file is
****mine**** and I can do whatever I want to it. I understand the value of sharing
ideas and contributing to other peoples issues and desires but there is an
intrinsic anxiety associated with it.

You don't want people thinking you are stupid or sloppy!

In this post I want to share the most used function I have in my current config
file. This is how I start every single new demand at my current work. Let's look
at what I want to automate:

1.  Create a new Emacs tab
2.  Fetch any updates in the `main` branch
3.  Create a new branch
4.  Create a worktree in a folder in the same level as the main project
5.  Run some shell scripts to decrypt secrets and perform additional setups
6.  Move to a file inside the project
7.  Ask if I want to start my REPL or not

Considerable list of things! Let's see how I did it.

{{< figure src="/images/my-project-worktree.png" >}}

Clunky, huh?

Before looking at what each of these lines, let's make some general remarks:

-   hard codes, rely on undocumented inner variables of other packages, hacks to
    synchronize async calls, hacks to move data around in very optimistic fashion,
    and so on.

And in the end, I never had to change a single line of this code in 6 months.

Let's break it down to see what is going on

{{< figure src="/images/my-project-worktree-commented.png" >}}

1.  hard-code of directory structure and important some useful names
2.  I started to use `tab-bar-mode` recently, so I want a new tab to every worktree now
3.  Magit calls in the most obvious and possibly wrong way. I got public interactive function and called it
    1.  Basically did `C-h k` to find what functions was bound to the keybindings I was used to and pasted it here
    2.  Read the `magit` codebase to find `magit-this-process` and add a lock to synchronize my process
4.  Ask myself for a branch & worktree name and then create it
5.  Run some shell scripts, ones are async and others sync
6.  I noticed that `shell-command` added some extra windows so I delete every other one without any checks
7.  Assume everything went ok and we are in the project root! ask me for a new file to visit
8.  Should I start my Clojure REPL? most of the time is YES.

This is one of the workflows I have coded in Elisp that helps me avoid
unnecessary manual intervention during my day. This is by far not the prettiest
function I ever wrote, but it gets the job done.

Sometimes we only want to accomplish what we want and move on...
