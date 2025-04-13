# Brutality Over Elegance

## Background

In my exploration and learning about paradigms and what makes code readable,
I've found that consistently, the best code is code that works. People
consistently find metrics to measure code by, when a perfectly good, logical
and simple method already exists. Code readability is one of these.

People love to write beautiful, elegant and "clean" code. In practice, this
means code which solves a problem in a very short and concise way, often using
ideal functional principles.

When people can't write perfect beautiful code, they try to get as close as
possible. This is where the trouble starts. A symptom of beautiful code is that
there are generally no major side effects and there aren't very many lines of
code. People try to emulate this by hiding side effects and code.

### Hiding Side Effects

Hiding side effects involves mutating global or otherwise shared state, often
through object oriented encapsulation. Mutating shared state can also happen by
passing pointers around and mutating the data pointed to. This can be trivially
resolved by `const` correctness, however that doesn't always happen.

### Hiding Code

Hiding code typically means separating lines of code from each other to reduce
the number of consecutive lines of code which do real work. Hidden code also
often takes advantage of hidden control flow to execute more code without
seeming to at a surface level.

### Natural Language

Splitting out information in this way, information being used to refer to
information a programmer would gather by reading code, is common in natural
languages, as when a lot of important ideas are bundled together in one
sentence it often doesn't give a listener time to properly understand what they
are listening to.

Reading natural languages has the same effect. Readers are used to reading
sentences at a specific pace, and that doesn't change easily. That means when
words and ideas are spaced out more, a reader understands more of what they are
reading.

Code is not like this. Programming languages are not natural languages and
there are different ways to indicate heavy logic. The primary culprit for this
is functions. A function can have just about any amount of logic inside it,
meaning the traditional method of parsing natural languages doesn't really
apply.

Code is also not like natural language in that a reader of code is jumping
around a codebase rather frequently. They don't start at the start and end at
the end. They start at, well, somewhere and end, uhh, somewhere else.

If I were to make an analogy to natural languages, I'd say good code is like a
dictionary. It's easy to filter through, everything relevant is grouped
together, and I don't mean in terms of an object, I mean they are physically
next to each other. And most importantly, it works. A generic and elegant
solution would be to teach someone etymology. Then they can derive the meaning
and pronunciation of 95% of words they encounter, the same as a dictionary
would do. The problem here is that etymology is fundamentally a different
field. Not only that, but a programmer is incentivised to continue to make a
truly generic solution. Ninety five percent isn't enough, you want a hundred
percent. Nevermind that you can just make cases for the remaining 5% of words
and anytime it becomes an issue, you just create a new case.

## Beautiful Code is Orthogonal to Good Code

This brings me to my biggest point. Elegant code is not necessarily readable
code. The two concepts are completely orthogonal in my book.

I recently stumbled across a good quote. This particular quote is simply "The
Burden of Generality". I'll even put it in a little quote block for you.

> The burden of generality

This is important because the most readable code solutions are general, but
revert to cases to avoid unnecessary elegance and generality.

An example of this I recently came across was looking at a codebase in which
someone was writing a simple DSL parser in rust. They mentioned having a large
number of `match` statements (rust's equivalent of a switch) instead of a
generic solution.

I told them there was nothing wrong with the "ugly" list of options in a bunch
of big long matches. I went as far as to say I believe their solution was
significantly more readable than a generic, "elegant" solution would be.

They brought up a common counterpoint. What if they wanted to extend the code?
A generic solution would allow them to create, say, a new instance of a class
or interface or *something* where all of the new code would be in one place.

Code being in one place is very good for avoiding bugs. The thing about rust is
that rust has exhaustive matching. That means if you don't cover every possible
case in a `match` statement, the compiler will throw an error. Clang and GCC
both do a similar thing in C/C++, however they throw warnings instead. This is
why you always resolve compiler warnings. Ultimately, exhaustive matching means
you can't miss a spot you need to change in code when adding a feature because
the code won't compile if you do. This is the kind of guarantee which a system
using features like inheritance to do branching doesn't have. Instead,
inheritance will simply implicitly do what the parent does if you forget
something. The code all being in the same place won't help you there.

Now let's switch perspective. The zen of zig says to favour reading code over
writing it. We've just been discussing how to write code. That is after all
what you do when you implement a new feature. Keeping the rust DSL parser
example going, when someone wants to read the function that interprets a token,
they can see all the possible options at a glance instead of having to jump
through every different location (which will be hidden because "elegance") in
which some simple abstract logic is defined. There will end up being more
abstract code to handle the split nature of the "elegant" solution than there
will be actual logic.

It is this style of writing "ugly" code which enumerates every possibility
directly in, most commonly, a `switch` or `match` statement. I like to describe
this kind of code as "brutal" because it puts everything you need immediately
in front of you. It brutally slams all the information you might need in your
face instead of politely only saying the minimum amount and requiring a
programmer to "ask" for more information about any one topic.

## Writing Good Beautiful Code

Brutal code is not necessarily easy to write well. What it does do is give a
programmer clear feedback on whether code is written well or not. A programmer
will favour a more beautiful solution where possible. When the code is brutal
there is nowhere to hide, making it clear just how beautiful a piece of code
is.

Not all code needs to be beautiful. But if code is beautiful, it cannot be
brutal.

In order to write beautiful code, you need to create space for the code to be
beautiful. That means making meaningful, large jumps between abstractions and
interfaces. Making thick layers of code allows functions to have depth, which
make functions actually do work. It is only once a function does enough work
that you can refactor that work into a beautiful function.

The trick to writing beautiful code is to understand that not all code can be
beautiful. A beautiful piece of code is often inflexible in its implementation.
This means you often need to structure your other code around the beautiful
bits. That's where the brutal code comes in. You write pieces of brutal code
that simply say "do this". That gives you the freedom to structure the brutal
code in a way that cleanly interoperates with the beautiful code. Note my usage
of "cleanly" here simply means "without issue", as opposed to the typical
tenets of "clean" code, which favour emulating beautiful code as much as
possible over all else. When every piece of code tries to be beautiful, none of
it can truly be such.

## Writing Brutal Code

Most importantly, brutal code is procedural. Brutal is characterised by clear
use of explicit control flow to exhaustively enumerate and control
possibilities. The `else` or `default` statements that are available in a
number of programming languages to automatically enumerate any remaining switch
or match cases can often be a code smell. In fact, I'd recommend putting these
options first in any switch block. If it doesn't make sense that way, it's
almost definitely a code smell.

On the topic of not using `else`, I'd say it's generally a code smell. There
are exactly three good uses of `else` that I've ever found.

Python's `for ... else` and `while ... else` [^1]. These constructs allow better
control flow. I firmly believe all known control flow is good control flow.
This basically means if you can write an LSP "jump to definition" function for
a piece of control flow (that is, when hovering over a jump of any kind, you
can trivially jump to the location the code will jump to), then it's good
control flow. I admit `goto` is maybe an exception here. To this end, I add one
more clause required for good control flow. That being having a known purpose.
Good control flow should answer the questions "where" and "why".

Zig's `inline else` inside a switch statement to inline expand enumerations of
all possible cases. This is usually only really a good idea if it is the only
prong in the switch statement, although it is possible to use correctly when
writing a hybrid of brutal and beautiful code.

When returning data from a function, if there are two pretty much equal options
to return from, an `else` is sometimes the best way to indicate that the two
prongs hold equal weight. Honestly, a switch over a boolean value would do just
fine here too.

Any other uses of `else` can and should typically be substituted with some
other control flow, such as guard clauses. This is because `else` typically
doesn't intrinsically answer "why" it's used.

Because of the heavy use of switches, brutal code often takes the form of very
tabular looking code. That is, the code often looks like it contains a series
of big tables.

Favour enumerating possibilities over reducing lines of code. Reducing lines of
code is supposed to reduce complexity. Using an `else` statement instead of
exhaustively enumerating possibilities does not reduce complexity. Enumerating
possibilities reveals hidden complexity and creates compile errors instead of
runtime bugs.

Favour pure functions where possible. Pure functions avoid side effects. This
makes it easier to enumerate possibilities.

Favour global state over singleton objects. Global state is bad. Singletons are
the exact same thing. There's absolutely no reason they should be any more
acceptable than global state. In making the singleton global, you've now
removed this bias.

[^1]:   I believe zig has support for this syntax as well. While I don't know
        of any other languages that also do, I'm sure they exist.

## The Single Responsibility Principle and OOP

The single responsibility principle is rather shortsighted. Using OOP to model
the world around us relies on our own understanding of said world. When using
OOP, programmers erect hard barriers between concepts which truly only have
soft barriers. Consider a class for a chair. What actually defines a chair?
What about stools? Ok, let's say you group chairs and stools together. They
have a common parent or something. When your application changes, so does that
grouping, yet it is not reflected in code. Chairs and stools are both great for
sitting on. But what if you wanted to smash a window with them? A person would
generally hold a stool by a leg if they wanted to smash a window with a stool,
but a chair would be held by it's back for window smashing.

Ok, so we make sitting the responsibility of the `person` class. Great, what if
a dog wants to sit on a chair? All of this instantly violates the single
responsibility principle, despite being a natural consequence of the "elegant"
object oriented approach.

What do we do instead? Separate the `Person`, `Dog`, `Chair` and `Stool`
classes from the actions of `sitting()` and `windowSmashing()`. Now they can be
free functions which enumerate every possible combination of "sitter" and
"sittee". This is starting to sound a lot like the brutal programming approach.

Another great quote I heard recently is "Data doesn't do anything". Like
before, let's put it in a nice quote block so it looks important.

> Data doesn't do anything

The idea here is that in separating the data from the methods, you can more
accurately represent real relationships.

## Beauty and Brutality

Stop writing "elegant" and "clean" code. Clean code is a misnomer. Real clean
code is code which does nothing. Start writing "beautiful" and "brutal" code,
because "beautiful" and "brutal" code both define clear boundaries and
possibilities.

Code that is "clean" and "elegant" tends to defer responsibility and meaningful
choices to the caller, and you have to run the code somewhere. Ultimately you
either end up with "brutal" calling code that is also unreadable to anyone
unfamiliar with the codebase, or you drown the important choices in so many
layers of abstraction that there is no meaningful code to write.

## Copyright

Copyright (c) 2024-2025 Cyuria. All Rights Reserved.
