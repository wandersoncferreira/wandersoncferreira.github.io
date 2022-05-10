+++
title = "abstraction: not what you think it is"
author = ["Wanderson Ferreira"]
lastmod = 2022-05-06T13:36:00-03:00
tags = ["raw-page"]
draft = false
+++

March 28, 2022

> “Interfaces are abstractions”<br />
> --- [Olaf
> Thielke](https://codecoach.co.nz/interfaces-are-abstractions/), the "Code Coach"

<!--quoteend-->

> “Interfaces are not abstractions”<br />
> ---
> [Mark
> Seeman](https://blog.ploeh.dk/2010/12/02/Interfacesarenotabstractions/), author of <span class="underline">Code that Fits in Your Head</span> and <span class="underline">Dependency
> Injection</span>

<!--quoteend-->

> “Abstraction in programming is the process of identifying common
> patterns that have systematic variations; an abstraction represents the
> common pattern and provides a means for specifying which variation to
> use”<br />
> --- [[<https://www.dreamsongs.com/Files/PatternsOfSoftware.pdf>][Richard
>
> 1.  Gabrie]]l, author of “The Rise of Worse is Better” and \_Patterns of
>
> Software\_

<!--quoteend-->

> “[...] windshield wipers [...] abstract away the weather”<br />
> ---
> [Joel
> Spolsky](https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/), cofounder of Fog Creek Software, Stack Overflow, and Trello

Of all the concepts debated in software engineering, abstraction is at
the top. I found two separate debates about it on Twitter from the past
week.

As the quoted writers show, people do not even agree what abstraction
means. Abstraction seems to stand for a hodgepodge of different concepts
involving generality, vagueness, or just plain code reuse. These
engineering debates --- debates about whether duplications are better
than the wrong abstraction or about whether abstraction makes code
harder to read --- trickle down into heated discussions over code. But
this confusion over abstraction's basic meaning makes all such debates
doomed.

This situation is particularly sad for me as someone with a background
in PL theory. There are a lot of topics in software engineering that are
the result of accumulated intuition over decades. But we've had a pretty
good definition of abstraction since 1977, originally in the context of
program analysis, and --- I claim --- it actually translates quite well
into a precise definition of “abstraction” in engineering.

Abstraction in general is usually said to be something which helps
readers understand code without delving into the details. Yet, for many
of the concrete code examples programmers actually call “abstraction,”
they can be (and are) used in ways which add details and hinder
understanding. In opposition, I take the position that software
engineers will benefit from studying the mathematics of PL-theoretic
abstraction, understanding how it explains things they already do, and
letting this coherent definition rule their use of the term
"abstraction."

My initial goal in this post is a smaller enabling step: to give you
names for the other concepts that are often combined under the name
"abstraction" that they may be referenced, used, and critiqued
specifically, and to help you move away from the vague and contradictory
[citrus
advice](https://www.pathsensitive.com/2018/12/my-strange-loop-talk-you-are-program.html) that arises from using the same name for different things. From
there, I will proceed to provide the rigorous definition of abstraction
as it pertains to software, followed by concrete examples.

But the story does not end after separating true abstractions from their
impostors. The endless debates over what is and isn't an abstraction
shall be resolved in an unsatisfying way: almost anything can be viewed
as an abstraction, and most abstractions are useless. Yet once you learn
how to actually write down an abstraction mapping, you gain the ability
to look beyond the binary and explain the exact benefit that a given
abstraction does or does not provide a reasoner, and in doing so
rearrange the discordant intuition around abstraction into harmonic
lines of precise, actionable advice.


## Not Abstraction {#not-abstraction}

There are at least five other things that go under the name abstraction.


### Functions {#functions}

One contender for the oldest programming language is the lambda
calculus, where Alonso Church showed us that, by copying symbols on
pen-and-paper using a single rule, one could compute anything.

In the lambda calculus, making a new function is called “lambda
abstraction,” and often just “abstraction.”

By "making a new function," that doesn't mean that it's the process of
looking at two similar terms like sin(x)<sup>2</sup>+1 and 2\*x+1, and deciding
to make a function λx.x+1. That's anti-unification, described below. It
is quite literally the process of taking x+1 and changing it to λx.x+1.

And “abstraction” also refers to the output of this process, i.e.: any
lambda/function whatsoever.^1

[It's
been noted](https://cs.stackexchange.com/questions/93006/why-is-abstraction-in-lambda-calculus-called-abstraction) that this use of the word "abstraction" is quite different
from other uses. Unfortunately, this has polluted broader discussion.
Even though the lambda calculus usage is akin to adding an opening and
closing brace to a block of code, this usage leaks out into discussion
of "abstracting things into functions" and from there into extolling the
benefits of being able to ignore details and other things that closing
braces really don't let you do.

So functions are abstractions --- just in a very limited meaning of the
word with little relation to everything else under that label. Moving
on...


### Anti-unification {#anti-unification}

"[Anti-unification](https://en.wikipedia.org/wiki/Anti-unification_(computer_science))"
is a fancy term for the process of taking two things that are mostly
similar, and replacing the different parts with variables. If you
substitute those variables one way, you get the first thing back; else
you get the second. If you see x\*x and (a-b)\*(a-b) near each other in a
codebase and extract out a square function, then you've just done an
anti-unification (getting the pattern A\*A with the two substitutions [A
↦ x] and [A ↦ a\*b]).

(Its opposite is
[unification](https://en.wikipedia.org/wiki/Unification_(computer_science)),
which is comparatively never used in programming. Unless you're writing
Prolog, in which case, it's literally on every single line.)

This probably looks familiar: virtually all of what goes under the Don't
Repeat Yourself label is an example of anti-unification. Perhaps you
would describe the above as "abstracting out the square function"
(different from the previous definition, where "abstracting" is just
adding curly braces after the variables are already in place).

In fact, Eric Elliott, author of <span class="underline">Composing Software</span> and <span class="underline">Programming
JavaScript Applications</span>
[goes
as far as to say](https://ericelliottjs.com/premium-content/abstraction-and-composition) “abstraction is the process of simplifying code by
finding similarities between different parts of the code and extracting
shared logic into a named component (such as a function, module,
etc...)” --- i.e.: that abstraction is anti-unification. He then
[goes
on to claim](https://medium.com/javascript-scene/the-secret-of-simple-code-a2cacd8004dd%0A) "The secret to being 10x more productive is to gain a
mastery of abstraction." That sounds pretty impressive for a process
which was
[first
automated in 1970](https://homepages.inf.ed.ac.uk/gdp/publications/MI5_note_ind_gen.pdf). ^2


### Boxing {#boxing}

"Boxing" is what happens when you do too much anti-unification: a bunch
of places with syntactically-similar code turns into one big function
with lots of conditionals and too many parameters. "Boxing" is a term of
my own invention, though I can't truly claim credit, as the "stuffing a
mess into a box" metaphor predates me. Preventing this is exactly the
concern expressed in the line
"[duplication
is better than the wrong abstraction](https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction)," as
[clarified](https://www.codewithjason.com/duplication-cheaper-wrong-abstraction/)
by a critic.

There's a surefire sign that boxing has occurred. Sandi Metz describes
it nicely:

> Programmer B feels honor-bound to retain the existing abstraction, but
> since [it] isn't exactly the same for every case, they alter the code to
> take a parameter, and then add logic to conditionally do the right thing
> based on the value of that parameter.

I've
[written](https://www.pathsensitive.com/2018/01/the-design-of-software-is-thing-apart.html)
and
[spoken](https://corecursive.com/036-jimmy-koppel-advanced-software-design/)
against this kind of naive de-duplication before. One of the first
exercises in my course is to give two examples of code that have the
same implementation but a different spec (and should therefore evolve
differently). Having identical code is not a foolproof measure that two
blocks do the same thing, and it's helpful to have different terminology
for merging similar things that do and do not go together.

But, particularly, if we want abstraction to have something to do with
being able to ignore details, we have to stop calling this scenario
"abstraction."


### Indirection {#indirection}

Though not precisely defined, indirection typically means "any time you
need to jump to another file or function to see what's going on." It's
commonly associated with Enterprise Java, thanks to books such as
Fowler's Patterns of Enterprise Application Architecture, and is
exemplified by the Spring framework and parodied by
[FizzBuzz:
Enterprise Edition](https://github.com/EnterpriseQualityCoding/FizzBuzzEnterpriseEdition). This is where you get people complaining about
"layers" of abstraction. It commonly takes the form of long chains of
single-line functions calling each other or class definitions split into
a hierarchy across 7 files.

Fowler's examples include abstracting

```text
contract.calculateRevenueRecognition()
```

into the Service Layer Abstraction™

```text
calculateRevenueRecognition(Contract)
```

If you were to describe the former, you'd probably say "It calculates
the recognized revenue for the contract." If you were to describe the
latter, you'd probably say "It calculates the recognized revenue for the
contract." We've been spared no details.


### Interfaces, Typeclasses, and Parametric Polymorphism {#interfaces-typeclasses-and-parametric-polymorphism}

All three of these are mechanisms for grouping multiple function
implementations so that a single invocation may dispatch to any of them.
Most programmers will be familiar with interfaces, which are a language
feature in Java and TypeScript and a common pattern in Python.
Typeclasses, a.k.a. “traits,” are essentially interfaces not attached to
objects. Parametric polymorphism, a.k.a. “generics,” are a little
different in that they combine functions which differ in nothing but
their type signature.

Parametric polymorphism is essentially just adding an extra parameter to
a function, except that this extra parameter is a type. It's not
abstraction in the same way that anti-unification isn't.

Interfaces and typeclasses do tend to be associated with abstractions in
the sense about to be introduced. But there's a banal reason they do not
satisfy the goal of an abstraction definition: there's nothing mandating
that the many implementations have anything to do with each other. For
example, in my installation of the Julia language, the getindex function
is actually an interface with 188 implementations, dispatched based on
the runtime type of its arguments. Most of these implementations do
lookups into array-like structures, but a few do the exact opposite and
create an array.

Sometimes, when calling a function behind a polymorphic typeclass
interface, the programmer knows only one implementation is relevant, so
the shared name is just to save some typing. Other than that, in order
to make use of any of these, one must be able to explain the operation
of multiple functions in some common language. It is not the language
feature that allows one to program liberated from details, but rather
this common language and its correspondence with each of the
implementations. Which brings us to...


## True Abstraction {#true-abstraction}

In programming language theory and formal methods, there are several
definitions of "abstraction" in different contexts, but they are all
quite similar: abstractions are mappings between a complex concrete
world and a simple idealized one. For concrete data types, an
abstraction maps a complicated data structure to the basic data it
represents. For systems, an abstraction relates the tiny state changes
from every line implementing a TCP stack with the information found in
the actual protocol diagram. These abstractions become useful when one
can define interesting operations purely on the abstract form, thus
achieving the dictum of Dijkstra, that "The purpose of abstraction is
not to be vague, but to create a new semantic level in which one can be
absolutely precise."

You've probably used one such abstraction today: the number 42 can be
represented in many forms, such as with bits, tally marks, and even (as
is actually done in mathematics)
[as
a set](https://en.wikipedia.org/wiki/Set-theoretic_definition_of_natural_numbers). Addition has correspondingly many implementations, yet you need
not think of any of them when using a calculator. And they can be
composed: there is an abstraction to the mathematical integers from
their binary implementation, and another abstraction to binary from the
actual voltages. In good abstractions, you'll never think that it's even
an abstraction.

So, what do abstractions actually look like in code?

They don't.


### Where are the abstractions? {#where-are-the-abstractions}

A running joke in my software design course is that, whenever I show
some code and ask whether it has some design property, the answer is
always "maybe." And so it is whenever you ask "Is Y an abstraction of
X?"

First, a quick digression. In PL theory and formal methods, there are
many definitions of abstraction in different contexts, though they are
all far more similar to each other than to any of the not-abstractions
in previous sections. The one I am about to present is based on the
theory of
[abstract
interpretation](https://en.wikipedia.org/wiki/Abstract_interpretation). Abstract interpretation is usually taught as a (very
popular) approach to static analysis, where it's used to write tools
that can, say, prove a program never has an array-out-of-bounds access.
But it can also be applied to more interesting properties, though
usually in a less automated fashion. I'll be presenting it from the
perspective of understanding programs rather than building tools, and
explaining it without math symbols and Greek letters. I'll be in
particular focusing on abstracting program state. I'll occasionally
gesture at abstracting steps in a program, though the actual definitions
are more complicated. (Google “simulation relation” and “bisimulation”
to learn the technical machinery.)

So:

Abstractions are mappings. An abstraction is a pattern we impose on the
world, not the entities it relates, which are called the abstract domain
and concrete domain. Strictly adhering to this definition, the
well-formed question would be "Is there an abstraction from X to Y?"
followed by “Is that abstraction good?”

Let's return to the example of numbers. There is a great abstraction
from voltages in hardware to strings of 0's and 1's, from strings of 0's
and 1's to mathematical numbers, and also from tally marks to numbers.
These abstractions on numbers induce abstracted versions of each
operation on the base representations, such as the very-simple operation
of adding 1 to a number. Already, we can see that the abstractions live
outside the system; computers function just fine without a device that
reads an exact value for the voltage in each transistor and then prints
out the represented number. Yet in spite of living outside the system,
this mapping is perfectly concrete.


### Evaluating abstractions {#evaluating-abstractions}

The three example abstractions above have two properties that make them
useful. The first is _soundness_. The picture above is what's called a
“commutative diagram” in that any path through the diagram obtains the
same result: given an input set of voltages, it would be equivalent to
either (a) run a circuit for adding one and then convert the resulting
voltages to a number, or (b) convert the voltages to a number and then
add 1 with pen-and-paper. The second is _precision_: Adding 1 to a
number produces exactly one result, even though it corresponds to a
diverse set of output voltages.

Precision is what makes finding good abstractions nontrivial. The
eagle-eyed reader might notice that any function to the integers yields
a sound abstraction. For example, there is an abstraction from your TV
screen to integers: the serial number. However, you'd be hard pressed to
find any operations on TVs that can be sanely expressed on integers.
Turning the TV on or changing the channel leaves it with exactly the
same serial number, while replacing the TV with one slightly larger is
barely distinguishable from randomly scrambling the serial number.
Indeed, one would likely implement the “slightly larger TV” function on
the abstract domain of serial numbers by mapping each serial number to
the set of all other serial numbers. This is sound --- getting a larger
TV and then taking its serial number is certainly contained in the
result of looking at your current TV's serial number then applying this
operation --- but maximally imprecise.

A consequence of this: if we translate every question “is X an
abstraction of Y” to “is there an abstraction which maps X to Y,” the
answer is always “yes.” Instead, we can ask _which operations_ can be
_tracked precisely_ with reference only to the abstract domain. The
abstraction from voltages to numbers is perfectly precise for all
operations on numbers, but not for determining whether a certain
transistor in the adder circuit contains 2.1 or 2.2 volts. The
abstraction from TVs to serial numbers is perfectly imprecise for every
operation except checking whether two TV's are the same (and maybe also
getting their manufacturer and model).

To the property of soundness and the measurement of precision, we add a
third dimension on which to evaluate abstractions: the size (in bits) of
an abstract state. The good abstractions are then the sound abstractions
which are small in bits, yet precise enough to track many useful
operations.

So consider a website for booking tables at restaurants, where the
concrete domain is the actual state of bookings per table
{table1BookedFrom: [(5-6 PM, “Alice”), (7-8 PM, “Bob”)], ...,
table10BookedFrom: [...]}. The abstract domain shall be a list of
timeslots. For each user, it is possible to abstract a concrete state
down to the abstract state listing the booked timeslots for that user,
i.e.: for Bob, [7-8 PM]. What makes this an abstraction, as opposed to
just an operation on the restaurant state, is that we shall then proceed
to describe the effect of every other operation on this value. So
consider the actual booking function, which might have this signature:

```text
void bookTable(User u, TimeInterval t)
```

Below I give 4 specifications for this function. For the example of
booking a table for Carol from 7 to 8 PM, these specifications give:

1.  The actual behavior of this implementation, say, trying to assign
    Carol to the lowest-numbered table.
2.  All allowed behaviors on the concrete states, i.e.: finding any table
    open at the given time and assigning it to Carol, or doing nothing if
    there is none
3.  The allowed outputs on the abstract domain of Carol's bookings,
    namely (assuming Carol does not already have a reservation) either
    [7-8 PM] or [].
4.  The allowed outputs on the abstract domain for Bob or any other user,
    i.e.: the exact same as the input.

From this one example, we can derive quite a few lessons, including:

-   **All of these specifications are useful** in that you might use each of
    them when mentally stepping through the code. Perhaps you'd think
    “This line shouldn't have affected any of Bob's bookings” (using
    specification 4, corresponding to the “Bob's bookings” abstraction) or
    “When I click this button, either table 5, 6, or 7 will be booked”
    (using specification 2).
-   **Abstractions are separate from the code, and even from the abstract
    domain.** It does not make sense to say that the bookTable function or
    anything else in this file “is” the abstraction, because, as we have
    just seen, we can use many different abstractions when describing its
    behavior. More striking, we see that, even for a specific pairing of
    concrete and abstract domains, there can be many abstractions between
    them.
-   **Instead, code is _associated_ with abstractions.** Note the plural.
    We've seen that bookTable can be associated with several abstractions
    of the behavior --- infinitely many in fact, including many useful
    ones not previously discussed, like mapping the restaurant state to
    the list of timeslots with available tables.
-   **No code change is needed to reason using an abstraction.** We could
    extend the mapping from relating abstract/concrete states to relating
    steps between them, and then say the bookTable function “abstracts”
    the set of intermediate steps the program takes for each line in the
    function, but we could do this almost as easily if the bookTable
    implementation was actually a blob in a much larger function.
-   **Different abstractions tend not to be more or less precise than each
    other, just differently precise.** Compare the abstractions from the
    restaurant state to Bob's bookings, Carol's bookings, and the set of
    open timeslots. All of them can be used to answer different questions.

Continuing, we can also evaluate what makes the “Carol's bookings”
abstraction a good one. The corresponding specification, Specification
3, is quite close to deterministic, yielding only two possible output
states. The corresponding abstract states contain much less information
than the concrete ones. And an entity (human or tool) reading the code
tracking only this abstract state will still be able to perfectly
predict the result of several other operations, such as checking whether
Carol has a table. This is the **new semantic layer on which one can be
absolutely precise** that Dijkstra speaks of!

Of course, it is cumbersome to say “there is a sound and precise
abstraction mapping voltages on hardware to mathematical numbers” or
“there is a good abstraction from the specific details of when tables
are booked to just the available times.” It is quite convenient
shorthand to use the more conventional phrasing “numbers abstract the
hardware” or “bookTable abstracts all the details of reservations;” you
can say “abstraction mapping” if you want to clearly refer to
abstractions as defined in this blog post. Yet this shorthand invites
multiple interpretations, and can spiral into an argument about whether
booking tables should actually be the same abstraction as booking hotel
rooms. Feel free to call numbers an abstraction of the hardware, but be
prepared to switch to this precise terminology when there's tension on
the horizon.


## Whence the Confusion {#whence-the-confusion}

Programmers correctly intuit that it is desirable to have some way to
reason about code while ignoring details. In their 1977 paper, Patrick
and Radhia Cousot first taught us the precise definition of abstraction
that makes this possible. The other attempts fail to see the incorporeal
nature of abstractions and instead fixate on something in the code. But
there must be some connection.

Yes, functions are not abstractions. But for every function, there is an
abstraction, not necessarily a good one, collapsing the many
intermediate steps of the function into an atomic operation. There may
also be abstractions which admit a simple description of the relation
between the inputs and outputs.

Anti-unification is not abstraction. Yet two code snippets that could be
fruitfully semantically modeled with similar abstract states will often
be amenable to syntactic anti-unification. As disparate operations are
combined, ever more information must be added into the abstract state to
maintain precision. The result is boxing.

Indirection is hella not abstraction, though similarly-named functions
may suggest slightly-different abstract domains associated with them.
Many changes that make abstractions more explicit come with indirection,
but we've seen it's possible for readers to impose abstractions on code
without any changes at all.

Typeclasses and interfaces are not abstraction, but a good interface
will be associated with at least one good abstract domain precise enough
to make each of the interface's operations nearly deterministic (or at
least simple to specify), and each implementation will come with a sound
abstraction mapping its concrete states into that abstract domain.

Your car's windshield wipers and roof do not abstract away the rain, as
claims Spolsky, but they do mean that, to predict your happiness after
running your brain's DriveToStore() function, you can use an abstract
state that does not include the weather.

Abstractions offer the dream of using simple thoughts to conjure
programs with rich behavior. But fulfilling this promise lies beyond the
power of any language feature, be it functions or interfaces. We must
think more deeply and identify exactly how the messy world is being
transformed into a clean ideal. We must look beyond the binary of
whether something is or is not an abstraction, and discover the new
semantic level on which we can be absolutely precise.


## Appendix: Some Other Views of Abstraction {#appendix-some-other-views-of-abstraction}

Abelson and Sussman's Structure and Interpretation of Computer Programs
is a sure candidate for the title of “Bible of computer programming”
(sometimes [mixed with the
actual Bible](https://kingjamesprogramming.tumblr.com/)), and it's full of instruction on abstraction, beginning
with chapter 1 “Building Abstractions with Procedures.” I expect at
least one reader wants beat me over the head with a copy of the book
saying I'm getting it wrong. I don't really want that (it's 900 pages),
so I walked down 2 flights of stairs from my MIT office to Gerry
Sussman's office and asked him. I'll represent his ideas below.

Sussman explained that he believes abstraction is a “suitcase term”
which means too many different things, though he only sees two main uses
relevant to software. The first definition is: giving names to things
produced by the second definition. That second definition, he explained,
has to do with the
[fundamental
theorem of homomorphisms](https://en.wikipedia.org/wiki/Fundamental_theorem_on_homomorphisms) and its
[generalization](https://en.wikipedia.org/wiki/Isomorphism_theorems#Theorem_A_(universal_algebra)).
And then he pulled an abstract algebra book off the shelf.

I'll try to explain this as best I can with minimal math jargon while
still being precise. I'll explain the definition simultaneously with
Sussman's two examples, multivariate polynomials, and (physical)
resistors in electric circuits.

In this picture, G can be seen as the set of all data in all forms and f
is some operation on G. So G can be the set of all polynomials in all
representations, or the set of all resistors. f then can be the
operation of plotting the polynomial on all values, or computing the
current through a resistor across a range of voltages.

Now, there are many different values in G on which f does the same
thing. G contains both sparse and dense representations of the same
polynomial; these have the same plot. There are different resistors with
the same resistance; assuming they perfectly follow Ohm's Law, they have
the same current at the same voltage. One can write down the list of
lists of which values of G are treated the same by f; that's φ, the
kernel of f. So for polynomials, φ would be the list of distinct
polynomials, each of which contains the list of all representations of
that polynomial.

Now, finally, on can use φ to quotient or “smush” together the like
elements of G. All the different representations of the same polynomial
get mapped to something representing that polynomial independent of
representation. All the different resistors of resistance R get mapped
to the idea of a resistor with resistance R. This is G/K in the picture.

The theorem is then that G/K behaves the same (is isomorphic to) H,
e.g.: that that the set of different representations of polynomials can
be manipulated in the same way as their plot. But I believe Sussman was
gesturing less at this theorem and more at G/K itself, i.e.: at the idea
of merging together different representations that behave the same under
some operations.

I like this idea because it gives a way to unify into a single mapping
the relation between many different implementations and their shared
abstract domain. For the different representations of polynomials, a
typical formulation with abstract interpretation would provide a
different mapping from each kind of implementation into the shared
abstract domain. On the whole though, the operative idea in the
“homomorphism theorem” theory of abstraction seems to be that of merging
together concrete values that can be treated similarly by certain
operations. This idea is already present in abstract interpretation;
indeed, φ can be directly taken to be an abstraction mapping, with G and
G/K the concrete and abstract domains. On the whole, while I find the
connection to abstract algebra cute, I'm not sure that the “homomorphism
theory of abstraction” offers any insight that the theory of abstract
interpretation does not.

So that's the main item in Sussman's suitcase of meanings of abstraction
in software. It looks superficially different from any of the variations
of abstract interpretation, but is actually quite compatible.

Is there anything else in that suitcase? Any other (good) uses of the
word “abstraction” not captured by the previous definitions?

Maybe. I can say that there are is something I'd like to be able to do
with something called “abstraction,” but that I can't do with abstract
interpretation: dealing with inaccuracy.

You see, the orthodox definition of a sound abstraction would rule out a
technique that predicts the concrete output perfectly 99.99% of the time
and is otherwise slightly off, and instead prefers a function that says
“It could be anything” 100% of the time. I know there is work extending
abstract interpretation to some kinds of error, namely for numeric
approximations of physical quantities, but, overall, I just don't know a
good approach to abstraction that allows for reasonable error.

On a related note, sometimes AI researchers also talk about abstraction.
I know that the
[best poker
AIs](https://www.cs.cmu.edu/~noamb/papers/17-IJCAI-Libratus.pdf) “abstract” the state space of the game, say by rounding all bet
sizes to multiple of $5, and that human pros exploit it by using weird
bet sizes and letting the rounding error wipe out its edge. But I am not
aware of a general theory backing this beyond just “make some
approximations and hope the end result is good,” and am not even sure
“abstraction” is a good term for this.

**Acknowledgments**

Thanks to Nate McNamara, Benoît Fleury, Nils Eriksson, Daniel Jackson,
and Gerry Sussman for feedback and discussion on earlier drafts of this
blog post.

---

1.  Daniel Jackson credits Turing Laureate Barbara Liskov with

promulgating this usage. Her influential CLU language uses “abstraction”
to mean any unit of functionality (type, procedure, or iterator).

1.  Technically, it's only first-order anti-unification,

equivalent to extracting named constants, that Gordon Plotkin developed
in 1970. Work on higher-order anti-unification, which corresponds to
extracting (higher-order) functions, began in 1990; Feng and Muggleton's
“Towards Inductive Generalisation in Higher order Logic" (1992) provides
an early discussion. While Elliott is quite explicit that any
anti-unification is abstraction, it is true that there are a vast number
of anti-unifications of a given set of programs, and choosing the best
is very difficult. [DreamCoder](https://arxiv.org/abs/2006.08381) is a
recent notable work based on doing so.


### Liked this post? {#liked-this-post}

<br />

<!--list-separator-->

-  Related Articles

    <span class="org-target" id="org-target--comments"></span>
    <span class="org-target" id="org-target--comments"></span>

<!--list-separator-->

-  7 comments:

    <span class="org-target" id="org-target--comment-holder"></span>

    1.  <span class="org-target" id="org-target--c4782714983878326947"></span>

        {{< figure src="//www.blogger.com/img/blogger_logo_round_35.png" >}}

        [Jason](https://www.blogger.com/profile/14002956273801060588)[March
        29, 2022 at 1:35 PM](https://www.pathsensitive.com/2022/03/abstraction-not-what-you-think-it-is.html?showComment=1648575340644#c4782714983878326947)

        &gt; Indirection is hella not abstraction<br />
        <br />
        The identity abstraction (or any relabeling abstraction) is still
        abstraction. It's just not good.

        Reply[Delete](https://www.blogger.com/delete-comment.g?blogID=8584948780979499548&postID=4782714983878326947)

        <span class="org-target" id="org-target--c4782714983878326947-rt"></span>
        Replies

        <span class="org-target" id="org-target--c4782714983878326947-ce"></span>

    2.  <span class="org-target" id="org-target--c122527442434227251"></span>

        {{< figure src="//www.blogger.com/img/blogger_logo_round_35.png" >}}

        [Viljami](https://www.blogger.com/profile/04647682047426960672)[March
        31, 2022 at 1:14 AM](https://www.pathsensitive.com/2022/03/abstraction-not-what-you-think-it-is.html?showComment=1648703682748#c122527442434227251)

        &gt; On a related note, sometimes AI researchers also talk about
        abstraction. I know that the best poker AIs “abstract” the state
        space of the game, say by rounding all bet sizes to multiple of $5,
        and that human pros exploit it by using weird bet sizes and letting
        the rounding error wipe out its edge. But I am not aware of a general
        theory backing this beyond just “make some approximations and hope
        the end result is good,” and am not even sure “abstraction” is a good
        term for this.<br />
        <br />
        I think those are called abstraction heuristics.

        Reply[Delete](https://www.blogger.com/delete-comment.g?blogID=8584948780979499548&postID=122527442434227251)

        <span class="org-target" id="org-target--c122527442434227251-rt"></span>
        Replies

        1.  <span class="org-target" id="org-target--c4398178886831740087"></span>

            {{< figure src="//www.blogger.com/img/blogger_logo_round_35.png" >}}

            [James
            Koppel](https://www.blogger.com/profile/00605996177342825315)[March
            31, 2022 at 2:26 AM](https://www.pathsensitive.com/2022/03/abstraction-not-what-you-think-it-is.html?showComment=1648708003427#c4398178886831740087)

            Useful keyword; thanks!<br />
            <br />
            One of the first results I found:
            <http://users.cecs.anu.edu.au/~patrik/publik/absh-tutorial-2008.pdf><br />
            <br />
            "An abstraction is a mapping, ϕ, from (states of)<br />
            S to some abstract space AS, which preserves labelled paths<br />
            and goal states."<br />
            <br />
            This looks quite close to the abstract-interpretation definition I
            gave in this post, and identical the definition of a simulation
            relation.<br />
            <br />
            I was about to say that I don't think the "round to $5" mapping
            satisfies this definition. But now I realize that it can, for the
            same reason the floor function is an abstraction (from the reals
            to the integers).

            [Delete](https://www.blogger.com/delete-comment.g?blogID=8584948780979499548&postID=4398178886831740087)

            <span class="org-target" id="org-target--c4398178886831740087-rt"></span>
            Replies

            <span class="org-target" id="org-target--c4398178886831740087-ce"></span>

        <span class="org-target" id="org-target--c122527442434227251-ce"></span>

    3.  <span class="org-target" id="org-target--c8018638081176985264"></span>

        {{< figure src="//resources.blogblog.com/img/blank.gif" >}}

        Anonymous[April
        1, 2022 at 8:32 PM](https://www.pathsensitive.com/2022/03/abstraction-not-what-you-think-it-is.html?showComment=1648859530319#c8018638081176985264)

        I'd think you'll broaden your audience if you start from how the word
        "abstraction" originated in the philosophical context, then got used
        in fields of art ("abstractionism"), literature, and then in turn
        engineering and programming.

        Reply[Delete](https://www.blogger.com/delete-comment.g?blogID=8584948780979499548&postID=8018638081176985264)

        <span class="org-target" id="org-target--c8018638081176985264-rt"></span>
        Replies

        <span class="org-target" id="org-target--c8018638081176985264-ce"></span>

    4.  <span class="org-target" id="org-target--c5956430403847502915"></span>

        {{< figure src="//www.blogger.com/img/blogger_logo_round_35.png" >}}

        [Rasmus
        Källqvist](https://www.blogger.com/profile/04094769764887557424)[April
        3, 2022 at 12:21 PM](https://www.pathsensitive.com/2022/03/abstraction-not-what-you-think-it-is.html?showComment=1649002868768#c5956430403847502915)

        I agree with the anonymous post above. Excellent text about how to
        perhaps better use abstractions, but I found the argument lacking in
        why the common usages of the word are "wrong". Wrong because they're
        not the same as PL people use them? PL people did not invent this
        word, so I would have liked to see this framed more as "this would be
        a more precise and useful definition of abstraction than is often
        used"

        Reply[Delete](https://www.blogger.com/delete-comment.g?blogID=8584948780979499548&postID=5956430403847502915)

        <span class="org-target" id="org-target--c5956430403847502915-rt"></span>
        Replies

        1.  <span class="org-target" id="org-target--c2742654491815920858"></span>

            {{< figure src="//www.blogger.com/img/blogger_logo_round_35.png" >}}

            [James
            Koppel](https://www.blogger.com/profile/00605996177342825315)[April
            3, 2022 at 2:43 PM](https://www.pathsensitive.com/2022/03/abstraction-not-what-you-think-it-is.html?showComment=1649011413784#c2742654491815920858)

            'I would have liked to see this framed more as "this would be a
            more precise and useful definition of abstraction than is often
            used"'<br />
            <br />
            ??<br />
            <br />
            I think that's basically what I say. The first half is dedicated
            to showing how each of the not-abstraction uses break down when
            examined and don't actually comport with the desired property of
            abstraction of allowing one to ignore details.

            [Delete](https://www.blogger.com/delete-comment.g?blogID=8584948780979499548&postID=2742654491815920858)

            <span class="org-target" id="org-target--c2742654491815920858-rt"></span>
            Replies

            <span class="org-target" id="org-target--c2742654491815920858-ce"></span>

        2.  <span class="org-target" id="org-target--c6807590335406116782"></span>

            {{< figure src="//www.blogger.com/img/blogger_logo_round_35.png" >}}

            [Rasmus
            Källqvist](https://www.blogger.com/profile/04094769764887557424)[April
            5, 2022 at 10:10 AM](https://www.pathsensitive.com/2022/03/abstraction-not-what-you-think-it-is.html?showComment=1649167825709#c6807590335406116782)

            This comment has been removed by the author.

            [Delete](https://www.blogger.com/delete-comment.g?blogID=8584948780979499548&postID=6807590335406116782)

            <span class="org-target" id="org-target--c6807590335406116782-rt"></span>
            Replies

            <span class="org-target" id="org-target--c6807590335406116782-ce"></span>

        <span class="org-target" id="org-target--c5956430403847502915-ce"></span>

    <span class="org-target" id="org-target--top-continue"></span>
    Add comment

    <span class="org-target" id="org-target--top-ce"></span>

    Load more...

    <span class="org-target" id="org-target--comment-form"></span>
    [[<https://www.blogger.com/comment/frame/8584948780979499548?po=771403918924813779&hl=en>][]]

    <span class="org-target" id="org-target--backlinks-container"></span>

    <span class="org-target" id="org-target--Blog1-backlinks-container"></span>

    <span class="org-target" id="org-target--blog-pager"></span>
    [Older
    Post →](https://www.pathsensitive.com/2021/03/developer-tools-can-be-magic-instead.html) [Home](https://www.pathsensitive.com/)

    <span class="org-target" id="org-target--sidebar"></span>

    <span class="org-target" id="org-target--Text1"></span>