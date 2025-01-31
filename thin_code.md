# Another Rant on "Clean" Code

The first problem is that a large proportion of developers lack either the
experience or the intelligence to actually understand what clean code looks like.

Clean code is (most commonly) not object oriented. Clean code is something that
is mathematically easy to reason about. That means it has some nice
mathematical (or otherwise) property that make it an elegant solution.

Elegant solutions often means minimising side effects and branching. This *can*
be good for performance but not always. The trap many developers, and I'd call
them beginners but they're usually not, fall into is thinking that *hiding*
side effects is the same as *getting rid of them*. No. Object oriented code
excels at hiding side effects in a different part of the program's scope. This
means to understand any one line, you must rationalise the entire codebase.
Call me a bad programmer, but I can't keep an entire massive codebase
(including all its side effects and quirks) in my head without a lot of time
spent within it. [Rant about the factory pattern below](#the-factory-antipattern).

Actual clean code can be rather difficult to read, as it often makes use of
principles people don't usually think about when reading/writing code. That's
what makes it clean, after all. I'd go as far as to say an example of this is
the infamous quake III fast inverse sqrt algorithm, although it makes some
approximations which I wouldn't necessarily deem clean.

Clean code can have massive performance costs. What is mathematically simple
often doesn't translate to simplicity in performance. See also the previous
point in terms of compiler optimisations and CPU optimisations (i.e.
instruction pipelining and CPU caching).

Code that is easy to reason about while writing, often isn't easy to reason
about when reading. In fact, I'd go as far as to say that the only code that is
easy to reason about when reading is that which is so simple you *don't need to
reason about it when writing*.

## The Factory Antipattern

The factory "pattern" is probably the best example of how OOP is overused.

Firstly, for the creation of one or more objects, you should at most need a
single function. Don't make an entire fucking class. You don't need an entire
fucking class. If you think you need an entire fucking class, think again. If
you still think you need an entire fucking class, stop thinking. If, by some
miracle of god, you still firmly believe you need an entire fucking class to
instantiate a class, you're wrong and [I have a suggestion for your career
choices](https://careers.mcdonalds.com). 

All the logic for the creation of an object should be handled in that object's
constructor. If you somehow need more detailed logic, create helper functions
for the constructor or create a static class method to instantiate a specific
version of the object. It's not difficult and it's much easier to read. If
there's ever a bug, there's also only one location where that bug could
possibly be. Stop creating factories for this shit.

There is one usecase, which the factory pattern was originally designed to
handle, which isn't covered above. This usecase is still a bad fit for the
factory pattern. The usecase is creating multiple of an object. This is where
the name "factory" came from. Use a helper function to do this. Bonus points if
you defer most of the logic to the class's constructor (or similar method as
described above).

## Singletons are Fucking Stupid

Ok, they're not. The problem with singletons is that there's only one of them.
If you can guarantee that there will only ever be one of a class ([and it's not
a fucking factory](#the-factory-antipattern)) then you might as well have it be
a global. This restricts you less. When you design a singleton class, you put
artificial restrictions on yourself, and before you say "oh but what if I want
two instances", just run the goddamned program twice. These artificial
restrictions are created by the fact that you're *designing a class*. If you
can't figure out why that's not what a class is meant to do, consider going
back to programming 101. If that doesn't work, consider never writing object
oriented code again.

People love to hate on globals and say that they're an antipattern or somehow
bad practice. A singleton is a global. They're one and the same. All of the
issues of globals don't magically go away when you wrap everything in a class.
Yes, globals are often misused.

If you think that, in your language, with your way of writing code, singletons
don't restrict you any more than a global, that's fine. Maybe you have found
the perfect use for a singleton. Consider making it a global anyway, if only to
serve as a warning. When someone is reading the code and sees the global,
they're liable to think twice about it. That is never not a good thing.

## The Cleanest Code

The most clean example of code I can think of is a circular doubly linked list.

It has all the hallmarks of clean code. It is structured in such a way as to
have very limited side effects. It doesn't have edge cases (like a regular
linked list). It is a unique and mathematically nice way of thinking. This
translates to being difficult to understand when people first see linked lists.

It even fucks up cache locality to ensure bad performance. It's genuinely some
of the cleanest code to ever have been invented, and *it's not even a piece of
code, it's just a data structure*.

I love circular doubly linked lists. They are, in some ways, a perfect data
structure. When you need them, they are the best fit and nothing else comes
even close to how clean they are.

Some other perfect data structures involve perfect hash tables (not hash maps,
they're riddled with shitfuckery, and regular hash tables aren't the best
either), arrays (just your regular fixed size ones, not dynamic ones) and
probably some spacial tree structure thingy invented by martians.

## The Whole Point

Good code has a balance of clean code and simple, readable code. I wrote about
[brutal code](brutality.md) before but I didn't really hammer on the difference
between "clean code" (robert martin's idea) and actual, elegant, clean code.

The pivotal example for me is having an exit flag (or some other conditional
flag) in a loop. They're not elegant by any means and theoretically have a
decent performance hit. What they are is readable. Flags in loops are some of
the most readable shit I've ever seen. I have a bad habit of avoiding them
wherever possible and attempting to replace them with control flow. It takes up
a fair bit of my time when programming.

I'll also finish this off with a good quote I read recently.

> There are two ways of constructing a software design: One way is to make it
> so simple there are obviously no deficiencies and the other way is to make it
> so complicated that there are no obvious deficiencies.
>
> -- <cite>C.A.R. Hoare, The 1980 ACM Turing Award Lecture</cite>

## Copyright

Copyright (c) 2025 Cyuria. All Rights Reserved.
