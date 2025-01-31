# The Best use cases for Python

## Foreword

Python has many, many uses and is a very versatile language.

This article outlines the best uses I've found for Python to date, and why I
believe them to be the best.

## Scripting

Python is often called a scripting language. What I think most people don't
realise is that Python is the most popular cross-platform scripting language.
This means if you write a script in Python it can (ideally) run on Windows,
GNU/Linux, macOS, Non GNU Linux, BSD and anything else you can think of (with
the important exception of Temple OS). This makes Python an actually decent
alternative to scripting languages such as bash, which don't necessarily have
great support on, for example, windows (I know git bash exists, but it's not as
universal as CPython).

In my mind, Python is the best option for custom cross-platform utility scripts
such as simple test harnesses for less simple testing scenarios or for writing
build scripts or other similar tools. If I had to write a build system for, say
C++, I would write it in Python. In fact, I like to think I would write
something incredibly similar to meson.

The biggest drawback of Python is often touted as its slow speed. The Python
interpreter has proven time and again that it is just not as fast as most other
modern languages for most computational tasks. If you want to write some image
processing code, do it in C or C++. Or maybe Rust or Zig. The point is that
most scripting applications are just a matter of delegating processes and
piping data around. This is stuff for which Python is just as good as anything
else. In fact, many scripting languages like bash are actually quite slow.
People just don't complain about it because no one in their right mind would
ever try to write a performance critical end user application using only bash.
Python is so versatile and beginner-friendly that a lot of people have tried to
use it to write serious performance critical applications. This is where the
stereotype about Python's performance comes from.

Now I fully believe Python could be perhaps better as a dedicated scripting
language, but Python is used elsewhere. It's not just a scripting language, yet
it somehow is still extremely effective at it. The main thing for me is that
Python makes it trivial to write complex behaviour compared to a "real"
scripting language like bash. The amount of libraries and tooling Python has
available through pip and even just the Python standard library is incredible.
Every single CLI utility in Unix and bash is either trivial to implement in
Python or has a good alternative available in the standard library.

Failing to find such an alternative, you could always implement it yourself in
either Python or your C ABI compatible compiled language of choice and compile
the program as a Python C API extension. If you're too lazy to do even that,
just run the shell command from Python, it has support for everything you can
do with bash syntax.

I believe the most important trick to scripting with Python is to explicitly
import all the functions you use, for example:

```py
from json import load
from os import environ, remove
from pathlib import Path
from shutil import which
from subprocess import run
from sys import argv, exit
```

## Gluing

Python has so many incredibly well written and effective libraries available
through pip. My other favourite use for Python is to serve as the glue which
combines interfaces into a cohesive program. You could write the backend code
for a videogame, which combines all the logic for, say, damage and collision,
with a state management system written in Python and taking advantage of types
such as `Dict` and powerful list comprehensions and list slicing features. You
could then use some front end GUI library such as pygame-ce for handling window
management and events as well as another graphics library like modernGL for
rendering the game in 3D. Let's say you want to add multiplayer, you can do
that really easily using one of the many networking libraries available in
Python. Or maybe just plain sockets.

If you were to take the previous example and write the whole thing in, say,
C++, you would end up using a bunch of extra libraries. For the 1 to 1 version
of the example in C++, you'd end up using SDL, GLFW, GLM (probably), STB, some
JSON library, maybe Boost as well and who knows what else. Now you have to deal
with properly linking all of these libraries and making sure they behave
correctly with each other. There's also still a lot of missing functionality,
for example pygame-ce is not just bindings to SDL, it provides a lot of extra
functionality (I should know, I helped write some of it). Meanwhile, you need
at most three external libraries in Python, all of which are one `pip install`
away from just working. Of course, you could definitely use fewer libraries in
C++, for example, you don't necessarily need GLM or Boost, and maybe you don't
need STB or the JSON library either. That gets you down to two libraries as
well. The problem is that the more functionality you add the more you'll wish
you had these libraries. You'll also need to deal with a lot more
cross-platform compatibility issues.

Personally if I were to start making a videogame as of the time of writing
this, using the same principles, I would write the graphics in either C or C++
using Vulkan. Then I'd maybe create some simple bindings which can easily
be accessed from Python. The important thing here is that I can control exactly
what code ends up on the Python side and what ends up on the C/C++ side. Then
I'd take advantage of Python's superb support for image loading and
window/event handling and write the videogame backend logic in another,
separate C or C++ module. Then I could fairly trivially add networking on the
Python side.

## Distributing Python

One more thing about Python is its availability. Python is available on the
machines of pretty much anyone who does dev work and you can reasonably expect
it to be so. Don't expect Python to be on an end user machine though. An end
user should be able to just install a program and it'll work without any
magical extra dependencies. Everything should just come bundled. You absolutely
need a C++ standard library? Bundle it. Or statically link, it's not like I
care that much. If that's still somehow too much to ask, then bundle the
standard library with the installer. That's what Windows programs that use
Microsoft's Visual C++ redistributables do. Also remember that all Python is
open source. This is a further reason to only use it as a wrapper for all your
other mission-critical code. Something breaks for a user? It's entirely
possible you can fix it by just modifying the wrapping Python script. Someone
wants to copy or take your code? Well don't worry, all the logic is compiled
into an extension. Now the only thing left to solve is the electron problem.

## The Takeaway

Python is an excellent language if you can restrict yourself to two simple
principles.
1.  Use it where there is some other performance bottleneck, e.g. networking or
    heavy IO.
2.  Don't use everything Python has to offer. It has many, many features, but
    you should never be using all of them. Python is a general purpose
    programming language. That means it serves a lot of purposes and your
    use case is just one. Most features in Python are only appropriate for
    specific use cases and odds are, yours isn't one of them.

Sticking to these two principles makes Python an excellent language for pretty
much any purpose you can think of.

Python is a tool just like any other. It is in fact an excellent tool. As such
there are occasions where it should be used and occasions where it shouldn't.

## Copyright

Copyright (c) 2024-2025 Cyuria. All Rights Reserved.
