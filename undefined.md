# Causes of Undefined and Unexpected Behaviour

The Root of All Bugs is Unexpected (which includes undefined) Behaviour

Yeah. No shit.

Let me explain how I got there though, because the journey is much more
interesting and could lead to some actually helpful insights instead of "if you
don't want bugs, don't write code with bugs".

## My Theory of Conditional Control Flow

This realisation first started with a thought process I couldn't quite explain.
My idea was simply that conditional control flow causes bugs. The less control
flow you have, the fewer number of bugs.

From one perspective this is super obvious. Conditional control flow leads to
complex programs, which are known to generally have more bugs. There's a pretty
well known Tony Hoare quote which explains this quite well.

> There are two ways of constructing a software design: One way is to make it
> so simple that there are obviously no deficiencies, and the other way is to
> make it so complicated that there are no obvious deficiencies.

But what I mean is a little more nuanced than that. What I mean is that complex
programs lead to more bugs *because of* having more conditional control flow,
not the other way around.

More importantly, that conditional control flow is the main or only factor that
impacts how many bugs a piece of code has.

## Holes in my Theory

Thinking further on this idea, I couldn't shake the feeling that I was right. I
felt it in my bones sort of thing.

But I could come up with a few counter examples which didn't quite fit my idea.

Pretty much all of those are memory safety vulnerabilities. Initially I
attempted to explain them by saying that `malloc()` is at fault, and that
forcing someone to manually `free()` heap stuff instead of it happening
automatically based on scope (like what rust does) was the issue.

This didn't sit right though, and it wasn't until I watched a youtube video on a
bug caused by invalid UTF-8 that I realised exactly why it was that conditional
control flow causes bugs.

## From Conditional Control Flow to Undefined Behaviour

Firstly, I posit that all bugs are caused by undefined behaviour. The trick is
to expand your definition of undefined behaviour to behaviour which is
undefined by anyone, including the developers themselves.

Next I posit that conditional control flow encourages writing code with
undefined behaviour. Specifically people use conditional control flow to impose
conditions on program state.

These conditions could be as simple as an array index being valid to some
complicated condition such as a series of dependencies being satisfied in one
of many ways.

The conditional control flow and conditions themselves are not the issue, it is
the code that comes after that is problematic. This code is written with
certain assumptions in mind. These assumptions stem from the control flow
above. Sometimes these assumptions stem from control flow which is *supposed*
to be present, but isn't. This has led to many, many buffer overflow
vulnerabilities.

The problem with writing code that makes assumptions (even if they're backed
up) is that it introduces a set of state which a portion of the code may
execute that has behaviour that isn't accounted for by the developers.

If we start to think of program state like any other data, we might notice that
the best data is that which is structured in such a way as to not allow invalid
cases. This might be something like using a tagged union instead of a struct
with a bunch of fields which aren't all supposed to be used at once.

Now ultimately, everything is just made of bits, and unless every possible case
can fit exactly into a power of 2, it's not possible to eliminate invalid
state. Also usually cramming every possible program state into the one set of
bytes isn't really a great for performance or code readability.

But what we can do is structure our code in such a way as to create stronger
guarantees that our invalid cases can never be reached. The best way to do this
is to ensure invalid cases can never be initialised. This is a very repetitive
process. What do we do when we see a repetitive process? We get a computer to
do it. In our case this means the compiler.

Moral of the story? Use a language that has a compiler which checks everything
for you.

Ok no, rust is an incredible language, but you don't need to use it for
everything, and you can still get bugs even if you write all your code in rust.

## The Real Moral of the Story

So what should you be doing?

Writing code in a way that reduces invalid states. This *can* mean reducing
conditional control flow in order to make yourself write code that has less
invalid state.

## Copyright

This page is Copyright (C) Cyuria 2025.
