# Object Oriented Wire Protocols

I've recently been looking into writing my own wire protocol implementations for
a couple of protocols, most notably the wayland and dbus protocols.

Something I've found tricky is that these protocols are object oriented, meaning
you create objects and call methods on those objects. My plan however, is to
write my implementations in zig, which emphasises data oriented design.

## The Issues

There are a few issues, but the big one is that zig is not object oriented. That
doesn't mean you cannot write OOP-like code in zig, but I want to try and avoid
doing so, as that somewhat defeats a large aspect of the language.

## The C Approach

Most of the time when this kind of thing is a problem in C, people just
enumerate the possibilities and write a bunch of functions for each of them.
And that works. Kind of. Not for me.

The problem is that you are trying to interface with language features that
don't exist, so you wind up with the same code just without the encapsulation,
and that's find except for the part where you no longer have any encapsulation
and side effects can run rampant.

This can induce bugs, which of course a proper specification can help avoid, but
I'd rather just not face the issue in the first place.

## Brute Force

I've tried to simply bulldoze over the problem. What I ended up with was one
large encapsulating "object" which does everything. Once again, UNIX philosophy
was right and this was not the way to go. The problem is that I'm trying to move
all of the OOP into one big object, which is not the way OOP is supposed to
work.

OOP works much more effectively when you could reasonably take advantage of
inheritance (even if you don't). That means small, bite-sized objects.

Smaller objects also helps reduce the scope of possible side effects, making
individual components much more manageable. The biggest reason why OOP might be
considered detrimental is that it encapsulates logic within side effects. You
are basically using global variables, without calling them global variables, and
that's what procedural programming gets right.

Basically, I've wound up using OOP in all the wrong places.

## Competing Protocols

My current best approach is to pretty much just write my own representation of
the problem. The idea is that now, instead of writing some kind of OOP
interface, we are writing our own interface which gives us much more freedom,
and a translation layer between the two interfaces.

## Copyright

Copyright (c) 2024-2025 Cyuria. All Rights Reserved.
