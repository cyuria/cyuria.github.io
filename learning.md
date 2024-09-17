# Learning a New Language

Someone recently asked me for tips because they wanted to learn python. I
figured my response could probably use a public document, so here it is.

Also, I recently learnt zig, so I will be using that as a bit of a reference.

## Courses, Books, etc

There are many good resources for learning programming languages. Many people
believe in courses. I personally beg to differ. I think courses are useful and
can teach basic syntax, but ultimately they don't teach the full language. If
you want to do a course, that's fine. In fact, I've done a few courses myself
and will freely admit they taught me a fair bit. The biggest problem with
courses is that people take them, add "java expertise" to their resume and never
touch the language again.

What you should do instead is make stuff. Different languages are good for
different aspects. Here are some popular applications of different languages:

### C

*   Simple CLI programs
*   Embedded programming and OSDEV (i.e. writing an OS or parts thereof, such as a
    kernel)

### C++

*   High performance gamedev
*   Interfacing with various protocols and formats (i.e. parsing json, wayland)
*   Native commercial software
*   Android apps

### Python

*   Scripting
*   Gamedev
*   Serving websites (via e.g. django or flask)

### Java

*   Commercial software
*   Minecraft mods

### Rust

*   Efficient, low cost GUI apps and tools
*   Wayland compositors
*   CLI and TUI apps
*   System daemons
*   Other POSIX based apps

### Haskell

I actually have no idea what people write in haskell, but I once used an AUR
helper written in it, so that kind of thing I guess.

### Javascript

*   Server Backends (via e.g. node, express)
*   Frontend web scripting (see DOM and AJAX)

### Fortran

*   Large scale data manipulation (e.g. for libraries such as numpy)

### Ada

*   Safety critical programming (e.g. for missiles for the U.S. military)

### Forth

Be warned that forth is a very different language to the others mentioned here.

*   OSDev
*   Bare metal applications
*   Forth compilers/interpreters

## Methods of Learning

There are a few different ways of learning the basics of a new language.
Ultimately you need to write code and make stuff to get better, but to learn the
basics there are a few different methods.

### Courses

Courses can teach you basic syntax and get you comfortable working with a
language. They don't make you an expert by any means, or even necessarily
proficient, as that comes with time, but they can teach you some basics.

### Books

Books are often really good intermediate learning material, where you can look
up any topic and learn about it, provided you already know some of the basics.
An example of what books can be good at teaching is topics like pointers in C.

### Google

Google is a very useful tool for specific problems. Let's say you want to parse
XML in python. You can type it into google and find more resources to go off of.
In this specific example, you might find the python documentation on the built
in XML parsing library.

This also kind of includes LLMs like chatGPT I guess. One thing to be aware of
is that LLMs don't recommend resources like google does. They are also sometimes
effectively useless or even outright wrong. This isn't saying google doesn't
have these properties sometimes, however with google you can always scroll down
to the next link.

### Watching

You can also learn by watching other people. This often takes the form of
livestreams and livestream recordings, which can commonly be found on platforms
such as youtube and twitch. They can teach you some best practices and build
good habits.

Watching other people is particularly helpful if you are unable to learn in
another way, such as writing code yourself or taking a course.

### Trying

If you know roughly what the syntax of a language should look like, which might
come from taking a course or just reading through an example program, one of my
favourite ways to learn a language is to just try stuff.

This is especially helpful for languages like rust, where the compiler is very
stringent.

## The Whole Process

Ultimately, the best and only way get better at making things in a new
programming language is to make things in said new programming language. There
aren't any shortcuts you can or should take, just write things.

## Copyright

This page is Copyright (C) Cyuria 2024.
