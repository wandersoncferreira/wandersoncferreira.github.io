---
title: "Why Clojure?"
author: ["Wanderson Ferreira"]
date: 2021-08-01T23:25:00-03:00
tags: ["clojure"]
draft: false
---

For the past 5 years I have been asked this question from time to time and I
always give a bad answer. In fact let's start with why can't I answer this
question properly?

<!--more-->

---


## Background {#background}

I came from an academic background and as soon as I started in software
development a striking fact was visible: **Personal opinions are a driven force
to several important decisions**.

I'm not allowed to have a personal favorite explanation about Plate Tectonics in
Geophysics, for sure we can disagree with mainstream theory, but you need to
come up with a pretty good theory, data to support it and many researchers
independently confirming your findings. So, as you might expect this does not
happen so often with "foundational concepts".

Even to regular concepts we always have a good ruler in Geophysics: Earth.

If you shoot some electrical waves into the ground and create a new mechanism to
measure resistivity you can easily test if it works by making a hole in the
ground, get a rock sample and measure the resistivity in your lab. And this
scenario is not only true inside the academia, if you are a company like
ExxonMobil or Petrobras, you do have the same constraints and ruler. Companies
usually have rules of thumbs when science don't have established explanations to
events, but they are always validated by the same ruler.

But now, what are the core concepts of software development? Are they easily
measurable? Better yet, how does them matter inside a small company building a
pilot project to 1000 users at best?

I never went to Computer Science, but I imagine we do have good answers there,
but in corporate world we quickly get into the realm of "good practices" which
is a pile of general advices that most of the industry agreed upon. How useful
are these advices? In my opinion, not much.

If I tell you "avoid complexity", what does that mean? Of course I want to avoid
complexity, but how? and more important, how can I avoid it given the current
circumstances of **my** project, **my** company, **my** budget, **my** timeframe, and
**my** skill level?

I don't know, just avoid complexity.

Let's now add the nature of system design into that ball of uncertainty: There
are countless ways to stick together code to make something happen. How do we
break our problem into smaller pieces? How will they interact? How do we account
for changes in the future? What are the possible nature of these changes? How
can they manifest in the company?

Impossible.

The amount of issues in this picture is amazing to me.


## Your options {#your-options}

I can easily understand why a **team** chooses Java/C# to create their products.
We have so many things to think about and Java/C# has been around for ages and
it just works! Google, Amazon, Netflix, and many others have lots of Java around
(and lots of money too). We can find answers to our technical questions easily
online and we have a shared vocabulary to talk about some of the "general good
practices" of this community.

I can easily understand why a **person** chooses Java/C# to learn and to become
proficient. We have many idioms to master, we have bills to pay and due to
rationale above we have more jobs around that community too.

---

Then, why clojure?

Back in 2014 when I started programming regularly, I joined a company and we
were writing in Object-Oriented style. The amount of jargons in those days were
insane: Should we use Factory Pattern? What do you think about doing Multiple
Inheritance from X, and Y? We could create an Abstract Base class for that? I
believe Visitor Pattern will be useful here. Yeah, let's think if we are not
violating LSP over that. Maybe this relationship is not mapped correct in the
ORM, so the objects are not hydrated correctly when you call Z.

Incredible, no words about the problem domain. In fact, the business domain
became reframed to fit the established narrative. Then, eight months into the
future, the real world shows us a new scenario that completely invalidate a very
important assumption we made to keep the code "elegant".

Back to whiteboard.

Sometimes, back to re-write.

---

Clojure is terribly boring. It has very few constructs to be learned and for 90%
of the business problems out there you will never use any advanced feature. I so
far experienced codebases with better Object Oriented concepts applied written
in Clojure rather than Java/C# which is very amazing to me.

Most of the business problems nowdays are related to information processing. You
get data from source 1, you send data to recipient 2, you collect result, you
modify some stateful store or send some emails, and we respond to source 1 with
results.

The community also developed its own set of "best practices" to make developing
this kind of application as simple as possible.The consequences of that is
evident in the previous companies I worked with: **we eliminate the language from
the thinking process to solve problems**.

I never hear about Clojure when I discuss some business problem. Clojure is an
implementation detail. It's common to say: We can create a Protocol for that or
should we type check this to make sure? But its very different than waiting for
a senior developer or architect to explain that a specific set of classes cannot
be manipulated to perform X due to A, B, C, D, and E that we defined in the
past.

Of course there are bad ways to code something, you will need to interact with
existing code and make sure nothing will break. However, there are no set of
self-inflicted pain due to hard specified relationship rules about the business
entities of your problem space.

I agree that sometimes this is useful and we have ways in Clojure to add more
restriction when needed using Schemas which feels like using a "type system"
only when convenient.

The power of the Functional idiom is also too good to be ignored. The amount of
cognitive overload associated with programming in Python is amazing that we
accept and encourage that. Try to follow some code from SQLAlchemy library or
Pandas, or simply following some nested decorators, it's great. If you can, I am
sure you feel very smart to do so.

The feeling of understanding something complex is great, I miss that a lot to be
honest. Perhaps this might be the reason some codebases has lots of `macros` in
Clojure too.

---

The killer feature of Clojure to me is that a small set of individuals can
collaborate evenly in several layers of the project. Due to the boringness of
the language we can turn the team focus into:

-   shared understanding of architecture (higher level)
-   shared understanding of current capabilities
-   improving readability of code
-   improving efficiency of code (smaller level and isolated tricks)

And everybody can follow.


## What about Python, Ruby, etc? {#what-about-python-ruby-etc}

Languages like Python got a great deal of attention due to the "easiness" of use
and the speed in order to get yourself a good prototype for an idea. Python
specially became even more essential due to the advancements of the Data Science
community.

I can only talk about Python here, its a great language and I would never
recommend that you start a data science team using Clojure or F#. However, if
you are creating an engineering team, you might consider something else.

-   Python is nice for prototype, but it's difficult to get consistency across teams
    -   Python enables several idioms in same codebase
    -   Dependending on previous background you might write something I never saw
-   Waste of resources
    -   Wild range of variability in published benchmarks from 30x to 200x slower
    -   In a big team, the performance hit of Python will imply in spending more on
        servers
-   Lack of good idioms to handle concurrent problems
    -   We are in 2021
-   Stability
    -   The language itself has many features being added every release
    -   Do not have a strong community supporting backward compatibility
    -   Clojure has a very small core and any additional feature can be suplied via libraries
    -   Java libraries are very stable and battle-tested too

One of the main selling points of Python is that "machine is cheap" and the time
to get something done in Java is too expensive, so we throw away a good
foundation in the name of speed ("productivity"). Then, if our product is a
success we think about what to do later.

To be honest, the whole premise of Java/C# programmers to be "slower" can be
argued when we see the amount of money that giant enterprises put into
developing good tooling for developers.

My take on this is that Clojure provides the best of both worlds, I can use all
the incredible foundations of Java and JVM while I keep the productivity of a
Python programmer.


## In the end, ... {#in-the-end-dot-dot-dot}

But, is Clojure the only answer?

Definitely not! If I join a company with expertise in Microsoft I would never
suggest to throw everything out and embrace Clojure/JVM/Java. However, I would
definitely push forward to use F#.

I would definitely choose the functional alternative to whatever mainstream
language happen to be in place.

In the end, how does it fix the "opinionated" scenario we face in software
development? No!, no way whatsoever.

Clojure has its own set of believes and its followers too.

That's why my answers are always bad and that's why you should continue doing
whatever you want.