+++
title = "codebases as communication"
author = ["Wanderson Ferreira"]
lastmod = 2022-05-22T08:30:00-03:00
tags = ["bookmark", "raw-page"]
draft = false
+++

## Computer Things {#computer-things}

Conventionally we communicate programming ideas with talks, papers, and
blog posts. But we can also communicate ideas with entire codebases. If
someone finds a security exploit, she'll sometimes publish a proof of
concept to prove the exploit isn't just theoretical.

Now let's say the exploit PoC comes with a ton of command-line flags:
verbose mode, configuration options, output formats, the whole works.
Now the writer is communicating something subtly different: not just
that the exploit exists, but she wants you to _experiment_ with it.
She's making it as easy as possible for you to play with the exploit
yourself and come up with variations and consequences.

This makes codebases like any other kind of communication medium. There
are different styles you can use to say subtly different things. There
are also different “genres”, or overt things you use the codebase to
say. Some examples:


### Of Genres {#of-genres}

This is by no means exhaustive. A codebase can:

-   Normalize cross-language comparisons.
    [TodoMVC](https://github.com/tastejs/todomvc/) showcases the
    differences between frontend frameworks, and I run
    [Let's Prove Leftpad](https://github.com/hwayne/lets-prove-leftpad/)
    to sorta do the same with formal methods.
-   Platform a technique. A simple business app with lots of well-designed
    property tests shows people how to use property testing. A codebase
    can show what a “proper” Rails application looks like. You can also
    add a complication to the codebase to show how the technique handles
    it.
-   Make a technical statement. Show that code written in a certain style
    is likely to have bugs. Or data from two different json formats,
    showing what queries are easier in each format.
-   Make a _political_ statement. Consider an NLP project that matches
    writing styles of anonymous Gab accounts with verified Twitter
    accounts, or one that does sentiment analysis on
    [dev.to](https://dev.to/) comments of male- vs female-authored
    articles.
-   Show the viability of an idea. A codebase that transforms a TLA+
    specification into a fixed testing suite won't be directly useful to
    anybody, but it can inspire other people to try making their own
    versions. A codebase doing lots of fun things with Word2Vec will
    inspire people to play with Word2Vec.
-   Be funny. [Kevin Kuchta](https://kevinkuchta.com/) is the undisputed
    master of this, with things like a
    [compile-time spellchecker](https://github.com/kkuchta/TSpell) and
    [CSS-only chat](https://github.com/kkuchta/css-only-chat).

<!--list-separator-->

-  Of Styles

    Styles are qualities inside a codebase that encourages certain kinds of
    reader responses. Done right, they also signal intentionality, that you
    intend for those responses. Again, not exhaustive.

    -   Well-commented code encourages the reader to understand something. The
        _something_ could be the problem domain, the solution, a used library,
        or the language itself.
    -   You can write code to encourage _extraction_, where the reader adapts
        part of the code to their own projects. You can also write it to
        encourage modification, so that people fork your project and make
        their own changes.
    -   A good UI encourages _use_ of the code. A set of well-documented CLI
        flags, along with
        [programmable
        completion](https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion.html), signal that you want people to actively use your
        codebase.
    -   A programming “flourish” showcases your own skill. A small utility
        script written in Idris, a library with a Clojure transducer, a
        codebase with a formal spec. When used sparingly, it shows you're both
        competent and _judicious_. You can do cool things but aren't compelled
        to.

    Repeated style patterns across codebases can communicate fundamental
    values. If a company releases a lot of open source, and many of them
    have a single flourish, it shows that engineers at the company get to
    work with exciting technology. If everything uses TDD, it shows that the
    company treats TDD as a fundamental part of the development process.

    Like other forms of media, a codebase style can show unintentional
    things about the author. What does it say about a programmer when their
    favorite test string is “boobies”?


#### Considerations {#considerations}

For a codebase to communicate well, the message needs to be easy to
understand. So the code layout needs to be very simple. Most production
code doesn't communicate well because it's split across files in nested
folders. That's hard to navigate. Try to have only a few files and make
the most important ones clear.

Boilerplate code hampers communication by adding noise to the code. If
you're trying to communicate something that's language-agnostic, use
low-boilerplate languages for the codebase.

[Science
code](https://www.hillelwayne.com/how-do-we-trust-science-code/) is often bad at communicating because it's a spaghetti mess
([example](https://gist.github.com/adiamb/79750cb13aea84c9a55c3bf95b69cc1f)).
At the same time, lots of abstractions and indirection tax the reader's
working memory. The code needs to be organized but not _too_ organized.

If you have an intentional genre and style, you should make that clear
in a project readme. Better overexplain than underexplain. I think it
also makes sense to talk directly _to_ the reader. Call out specific
lines, go into detail.

Unlike in regular programs, redundancy helps with communication.
Presenting the same thing in increasingly complex ways, or show
variations and their consequences.

All this means that communicative codebases will look different from
other kinds of code. Genre definitely; production code can also have
styles, but it'll be harder for the casual reader to notice them.


#### Questions I have about this {#questions-i-have-about-this}

-   What other genres and styles are there?
-   What are some good communicative codebases that already exist? I only
    know of examples in the comparison and joke genres.
-   Are there different techniques for writing communicative code?
-   While production code isn't communicative, can you have communicative
    carveouts? Like a complex app that calls attention to one particular
    file with a technical flourish.
-   How do we distinguish between intentional and unintentional stylings?
    What about conspicuousness: where the author _wants us_ to notice her
    style?
-   What would a code sharing platform that specializes in communicative
    code look like? Some common features like issues are less important,
    some rare features like discussion boards or code annotations would be
    more important.
-   What would a language designed for communicative projects look like?
    It might seem like communication is too complex to support with
    general features, but that's not true: “less boilerplate” is generally
    better for communication. So what other features would help? A really
    good CLI library? A powerful DSL builder? Are there things that would
    be footguns for 100-file codebases that would be beneficial for 3-file
    codebases?
