---
title: "emacs - projectile and perspective"
author: ["Wanderson Ferreira"]
tags: ["emacs"]
date: 2022-02-13T00:00:00-03:00
draft: false
---

I'd like to have one workspace for each project I work on. The desired
workflow is simple:

1.  Use `projectile-switch-project`
2.  Choose a project
3.  Automatically create a new workspace with the project name
4.  Switch to the new workspace
5.  Open file in the new workspace
6.  Commands like `ido-switch-buffer` needs to recognize only buffers of this workspace

Great! To accomplish this I am using [projectile](https://github.com/bbatsov/projectile) and [perspective](https://github.com/nex3/perspective-el).

Simply enable projectile and perspective:

```elisp
(require 'perspective)

(persp-mode t)

(require 'projectile)

(projectile-mode +1)
```

Projectile has a nice hook called
`projectile-before-switch-project-hook` which seems exactly what I
need i.e. before switching to the project, create the new perspective!

However, there is a single problem. How can we get the name of the
selected project? The function `projectile-project-root` will return
an outdated value if you call it inside our hook because the hook is
called before the chosen project name is used by projectile.

Not a problem, let's hack it!

```emacs-lisp
(defvar bk--projectile-target-project nil
  "Hold the target projectile name.")

(defun bk/projectile-switch-project-by-name (projectile-switch-project-by-name &rest args)
  (setq bk--projectile-target-project (->> (split-string (car args) "/")
                                           (-drop-last 1)
                                           (-last-item)))
  (apply projectile-switch-project-by-name args))

(advice-add #'projectile-switch-project-by-name :around #'bk/projectile-switch-project-by-name)
```

The advice will extract the chosen project name and keep it in
`bk--projectile-target-project` so we can use it later on. Keep in
mind that collisions can happen if you have two projects with the same
name in different folders.

And finally, we can use our hook

```emacs-lisp
(defun bk/new-persp-for-project-switch ()
  (persp-switch bk--projectile-target-project))

(add-hook 'projectile-before-switch-project-hook #'bk/new-persp-for-project-switch)
```

Easy!

Now, every time you switch a project using projectile a new
perspective will be created.
