---
title: "emacs - automation don't need to look pretty"
author: ["Wanderson Ferreira"]
date: 2022-01-11T00:00:00-03:00
tags: ["emacs"]
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
2.  Fetch any updates in the `master` branch
3.  Create a new branch
4.  Create a worktree in a folder in the same level as the main project
5.  Run some shell scripts to decrypt secrets and perform additional setup
6.  Move a file inside the root project
7.  Ask if I want to start my REPL or not

A considerable list of things! Let's see how I did it.

{{< figure src="/images/my-project-worktree.png" caption="Figure 1: Function my-project/worktree displaying 8 blocks required to perform the bullet itens above." >}}

Clunky, huh?

Before looking at what each of these lines, let's make some general remarks:

-   hard codes, rely on undocumented inner variables of other packages, hacks to
    synchronize async calls, hacks to move data around in very optimistic fashion,
    and so on.

And in the end, I never had to change a single line of this code in 6 months.

Let's break it down to see what is going on

{{< figure src="/images/my-project-worktree-commented.png" caption="Figure 2: Function my-project/worktree displaying 8 explicitly segmented blocks required to perform the bullet itens above." >}}

1.  hard-code for the directory structures and important useful variable names
2.  I started to use `tab-bar-mode` recently, so I want a new tab to every worktree now
3.  Magit calls in the most obvious and possibly wrong way.
    1.  I basically did `C-h k` to find what functions was bound to the keybindings
    2.  Paste the interactive functions in desired sequence
    3.  Read the `magit` code base to find `magit-this-process` and added a lock to synchronize
4.  Ask myself for a branch & worktree name and then creates it
5.  Run some shell scripts, ones are async and others sync
6.  I noticed that `shell-command` added some extra windows so I delete every other one without any checks
7.  Assume everything went ok and we are in the project root! ask me for a new file to visit
8.  Should I start my Clojure REPL? most of the time is YES.

This is one of the workflows I have coded in Elisp that helps me avoid
unnecessary manual intervention during my day. This is by far not the prettiest
function I ever wrote, but it gets the job done.

Sometimes we only want to accomplish what we need and move on...
