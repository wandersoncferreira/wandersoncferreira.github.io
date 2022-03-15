---
title: "developers aiming to the wrong target"
author: ["Wanderson Ferreira"]
tags: ["general"]
date: 2022-03-15T00:00:00-03:00
draft: false
---

## The Introduction {#the-introduction}

I set a personal journey to understand software development in a more
fundamental level.

What is this activity that I like so much to do? How to explain the
unease feeling that most of my discussions with other practitioners
are meaningless?

The meaningless arises from my perception that discussing technical
aspects of a problem has a strong [diminishing returns](https://en.wikipedia.org/wiki/Diminishing_returns) component to
it. For example, programming language choices.

Everybody has an opinion about Python, PHP, Java, and Ruby also why we
should use each. However, most of the arguments I see is related to
technical aspects e.g. lack of native support for multithreading
programming, several historical inventions to overcome language
limitations through the usage of "Established Patterns", some
definition of "Fun", etc.

As valid as they can all be, this is not enough for me. If you think
careful about these aspects, once you are over some basic high-level
concepts in programming languages threshold then any option is a good
option.

For the general case.

Therefore, I've been trying to avoid these traps and trying to define
what is really important to me on the craft. For example, programming
language choices.

I trully believe that [Language changes the way we think](https://www.gofluent.com/blog/how-language-affects-the-way-we-think/):

> Languages don’t limit our ability to perceive the world or to think
> about the world, rather, they focus our attention, and thought on
> specific aspects of the world.

With that in mind, I'd like to find world views more aligned with my
beliefs and if possible some similarities between the problem I'm
trying to work with and the imposed view carried by the language.

So far so good, but now I have a major issue to think about.

Would be easy if we were focusing too much on disliking parenthesis
and over praising "hireability" because the world runs on Javascript
in detriment of a well suited World view discussion of our craft.

However, the problem here is that Real World have many more actors
participating in the game: there are business people, regulations,
customers, physical limitations, people mood, politics, power
relationships, and so on.

We quickly enter the realm of social sciences.

And here probably I'll loose the technical person that made thus
far.

The feeling of joining a "hard science" to avoid "people interactions"
was fading away and I felt cheated.

Those blog posts about how we implemented micro-services using Kafka
and Kubernetes to **fix all the problems** is very seductive. The rage
towards your manager because he chose bad libraries or because we
chosen language X to implement service Y and all was terrible and
doomed to failure is very seductive.

But let's attempt to dive deeper.

What really is software development?


## The Naive {#the-naive}

There is a naive view that software development is the production of
programs. This is called "Production-view". What? and What is it then?

In fact we do this:

1.  There is a problem to be solved
2.  The problem is described in terms of necessary programs
3.  Programmers write programs
4.  A program is a set of instructions
5.  A instruction is a set of symbols written in text
6.  The text is interpreted by the computer
7.  The computer executes the instruction

Fair enough. Now, the naive view of software development advocates
that we only need to define the **right instructions** that needs to
be coded in the computer to solve a problem.

That's it.

This view is great to foster all sorts of shallow discussions: i) this
is cheap labour as we can replace the programmer easily as anyone can
follow specifications; ii) leave the programmer to discuss only the
best forms to translate the programs into instructions; iii) removes
any ethical responsibility from the programmer about the consequences
of running such programs; and so on.

There are more assumptions to justify the so called "Production-View"
of software development:

-   There is a given reality "out there" which we come across during software development
-   By analyzing the facts of this reality, we obtain requirements for the software
-   It is possible to separate the production of software from its use
-   Software production is based on models representing reality. Models should map reality correctly
-   Communication should be restricted and regular via fixed interfaces
-   The division of production into linear phases

The view is well sounded and pretty much how we operate nowadays. But
my personal experiences doesn't match exactly with this model.

A small detour here to bring back the debate on "Which Programming
Language to choose?". If there is a given reality "out there" as
practitioners of production-view said then there is no point in
discussing the choice of languages other than strict technical
aspects. But if we acknowledge the sudden fall into a diminishing
return point when only technical aspects is relevant, then this
discussion is basically a undecidable problem.

However, if we agree that languages help us to shape and perceive
reality in a different way, would this change your language
candidates?  Perhaps we need this new line of argument the next time
we face this decision. In what ways the real world will change if we
keep re-estructuring reality into given "Design Pattern" instead of
embracing its raw form in a more loosen fashion?

Programs often emerge out of a specific context, the person behind the
code matters a lot because the ideas shared to construct the solution
is very hard to grasp without a deep imersion in that particular
context and all the background knowledge provided by the coder. Often
inputs from non-programmers are major drivers for technical decisions.

And to be honest, there must have a better way....


## The Theory {#the-theory}

I came across [Peter Naur, Programming as Theory
Building](https://pages.cs.wisc.edu/~remzi/Naur.pdf) paper and it was
illuminating to me. I still can't make justice to such text without
distorting its intent but basically the general idea is that
programmers should be viewed as developers of theories.

The *Theory Building View* states that the output of the programming
activity is not symbols in text form but rather a theory about the
nature of that translation.

The word **theory** here has a different connotation than our daily
usage today but it includes the abilities to:

-   **explain** the program on **why** and **how**.
-   identity how new modifications can be expressed in terms of the
    theory of the program

We can simplify even further by introducing the idea of a
**metaphor**. What is the initial metaphor used to code the program?
Let's see an example:

-   We work in the Financial Industry with Loans
-   We have a particular business issue to solve
-   After endless discussions with all parties involved we arrive at
    the idea to treat the Credit Contract the same way a Marketplace
    treats a SKU.
-   We are making a parallel about Credit Contract &lt;--&gt; Marketplace SKU

This might fix the problem elegantly. Very clever solution. However,
what all the programmers involved in coding did was not to type the
program but to make the metaphor alive. And their jobs is to keep the
metaphor alive and add new features respecting the constraints imposed
by the initial metaphor.

And here we start to have problems, if all the developers that made
the metaphor possible left the company then we are in trouble. There
are often many ways to implement a change, but only a few options will
not distort the initial metaphor and make the program less prone to
bugs, performance issues, and the famous **re-writes**.

Coming back to our Marketplace metaphor above, even if we attempt to
describe that we are making this conceptual leap we are not guaranteed
to transmit the theory forward. New programmers may have a totally
different notion of what a Loean, Credit Contract, Marketplace, and
SKU even means.

What Naur is suggesting is that we should focus on how to
communicate and keep the **theory** alive not the implementation
details. In his paper, Naur's suggest that is not possible to convey
this information in any written form. This is something we learn by
doing and by interacting with the original theory owners.

I tend to agree to some extent, in the book [Software Development and
Reality Construction
(SDRC)](https://www.amazon.com.br/Software-Development-Reality-Construction-Christiane/dp/3642768199),
Donald Knuth has a chapter called "Learning from our Errors" where he
agrees with Naur's point of view but disagrees that documentation is
not enough to pass the theory along.

I'm still unsure about this because TeX is a pretty technical product
nonetheless and in the business environment we might have more complex
theories being built that rely on contradicting domain knowledge
information.

As far as I really like this idea, I think Naur's theory lacks more
explanation on the process and the use of software itself.

So I kept digging...


## The Design and the Future {#the-design-and-the-future}

As I mentioned the book SDRC is a nice entrypoint if you want to
explore more the relationship between social sciences and software
development.

I'm still become aware of Christiane Floyd's idea of **software
development as an insight-building process**. I'd like to quote three
paragraphs that I've been digesting for sometime:

> By design, we mean a specific type of insight-building process that is
> geared to producing feasible and desirable results within a particular
> domain. The domains in question may differ widely. We normally only
> speak of design when there are concerns we wish to fulfil, limited
> resources at our disposal, and different implementation options open
> to us.
>
> Design in software development is of a distinct nature and subject to
> special conditions. Software is characterized by an interplay of
> several unusual features, relating to both the nature of the product
> and its embedding in human contexts of meaning. Software exhibits an
> extreme degree of complexity, thus calling for equally complex
> construction processes. It consists of a uniform, abstract building
> material, is therefore plastic and, in principle, of unlimited
> revisability. It must be machine-processable, i.e., complete down to
> the last detail, consistent and formally free from error. It is not
> amenable to sensory perception and can therefore, in the last
> analysis, only be evaluated once in use. It creates social contexts
> for human actions, which are shaped by the technical properties of the
> product.
>
> Design thus links different worlds: the social world of the
> application in question, the technical world of the means of
> implementation, and the formal world of methods and concepts.

I like her description and coverage of this *design* definition. These
notions has the potential to redefine everything we take for granted
today in software development like tooling, interview processes,
performance assessments, skillset required for a role, new roles,
vanishing old roles, and so on.

So far my quest for a definition for "What is software development?"
lead to a happy realization that there is a lot more to it than mere
text production and a enthusiastic realization that I am far from
getting a definitive answer.

I hope in my next endeavors fixing problems with software, I can
come quickly to a point of diminishing returns about the
trivialities of which framework our team will use and spend a good
chunk of time discussing the hard questions about what we do with
computers.

More to come...
