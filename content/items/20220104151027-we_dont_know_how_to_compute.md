---
title: "we dont know how to compute"
author: ["Wanderson Ferreira"]
date: 2022-01-04T00:00:00-03:00
tags: ["software"]
draft: false
---

These are some thoughts after watching [We Really Don't Know How to Compute!](https://youtu.be/Rk76BurH384) from
Gerald Sussman.

Sussman is intrigued by how bad we build our systems today, basically when a
problem to be solved changes we need to change the software too. Ideally we
would add more code to deal with new requirements but often even a small change
in the problem domain will represent a huge amount of code that needs to be
shifted around.

Nature does not work that way. If we think about the human genome it has about 1
GB of code. This code is capable to adapt to pretty different environments, to
changes in requirements, and it's a lot flexible too if you tweak 10% you create
a **cat**, 15% a **mouse**, 20% a **cow**, etc (1). We definitely don't know how to compute.

Earlier this year, we had a [Strange Loop](https://www.youtube.com/watch?v=YDQmbT62eZk) chat with Sussman and Chris Hanson
about their new book: [Software Design for Flexibility](https://mitpress.mit.edu/books/software-design-flexibility). Great news, one more
addition from the wizards of MIT. If you want a preview, this lecture about [The
Power of Generic Operations](https://www.youtube.com/watch?v=cblhgNUoX9M) provides a good proxy for the kind of material
available in the book.

**WARNING**: Scheme and lots of parenthesis in the resources above.

I am already past chapter 3, but I would like to talk about two properties we
desire in our systems to achieve more flexibility: **adaptability** and **degeneracy**.


## Adaptability {#adaptability}

We build our **systems** with a large amount of custom-made highly specialized
components and this leads to a very brittle system - if we add a bit of noise in
the input of the program it's enough to break it. We need systems that can make
**reasonable decisions** facing a new situation.

In the **Power of Generic Operations**, Sussman talks about an auto-pilot module for
aircraft that was programmed to be turned off when any failure happens, however
the module had a lot of information available to make better decisions.

However, as designers of systems we can build something like that today, but we
would lose a very important aspect of today's software: **correctness**. Can we give
up the feeling of total control over the system and predictability in name of
adaptability? How about liabilities?

> The first thing we do, let's kill all the lawers - Henry VI, Part 2, Act IV, Scene 2 - Shakespeare.

There are also standard practices that does not contribute to this notion of
adaptability, for example, I believe the Java-style **oop** that is widely practiced
to be complicated to cope with adaptability. When we think about a problem to be
solved and immediately try to reduce our attention to only the "core concepts"
to lock them inside a class we are already imposing lots of limitations to our
code that will be run against the real world, not our simplification of it.

I find funny that it's often said in OOP lectures that we don't want to
replicate all the details of the problem domain in our classes, however every
single day you add a new "discovered" detail about the same problem domain but
eventually you see a hidden relationship that invalidates all previous
assumptions that you created in your ''fake domain''. Gj, time to hire.


## Degeneracy {#degeneracy}

In Software design is common to talk about redundancy but not degeneracy.
**degeneracy** is the ability to have many different ways to achieve the same
requirement.

We have access to a lot of computational power nowadays, we can execute several
pieces of code in parallel that should achieve the same answer and then we can
think about strategies for how to move forward:

1.  do we want to return the answer as soon as we get one?
2.  do we want to compare their results because this is critical operation?
3.  do we want to randomly return possible answers?

{{< figure src="/ox-hugo/_20220104_152344screenshot.png" >}}

This a theoretical relationship between biological properties that are important
to evolution. Seems like if we want to improve our game and start building
software that follows our ever changing needs we need to borrow more concepts
from this incredible system called **nature**. The concept of degeneracy is not so
distant for our current capabilities. We just choose not to do it.

As pointed out by Sussman we have additional constraints to achieve flexible
systems that does not live in the technological realm such as regulations and
liabilities. I would include economical factors too because time to market is
paramount to businesses today. Imagine yourself explaining that you need four
times more time to think and implement these concepts in your program.

Many reports about the cost of software maintenance indicates that it represents
60% to 90% of total cost for the full lifecycle . Also, the majority of the
maintenance is due to changes in requirements.

We definitely can improve our tooling around flexibility, but would that be
enough?

(1) Assuming a mechanistic view of the world.
