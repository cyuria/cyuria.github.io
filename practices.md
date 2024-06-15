# My Thoughts on Best Practices in Code

## Foreword

Many people swear by and use just as many different metrics for code. This is
not a critique of those methods, however flawed they may be.

Instead, this is an analysis of the statistics and logic behind the many
metrics people use for evaluating code and what I believe to be the best
metrics for measuring code from a computer engineer's perspective.

## Clean code this clean code that

> Clean code is great and lovely and all, but I think uncle Bob misses the mark
> somewhat
> ~ Me

There's a saying that as soon as a metric becomes a target it ceases to be a
good metric. I believe this applies to clean code as well. In principle, clean
code is a great idea which can improve the codebase. But in practice, I believe
it succumbs to becoming a target.

## Metrics and Targets

Now, you might say, but this applies to every metric ever, not just clean code.
To you I say, you're wrong. There are metrics which can still be good metrics
even when they have become targets. The problem is that most metrics don't
fully align with the intended goal. For example, how would we rate world
happiness? We cannot directly measure happiness. The best we can do is survey
people and ask them how happy they are. The problem is that now we are
measuring people's description of their happiness, not their actual happiness.
This is a problem, as it can incentivise people to provide a false account of
their happiness. Another problem is that people themselves don't have a proper
baseline happiness, meaning that 10/10 happiness for one person may only be
6/10 for another.

Fortunately, capitalism has a very good way of measuring things. Cost.
Developers are paid by the hour and a lot of things happen based on time.
Therefore, the most important metrics for a piece of code is the time cost
taken to develop and maintain it as well as the profits that result from
using the code itself.

This results in three simple metrics for code.
- Profit
- Writability
- Maintainability

Now I would argue that profit is a combination of the performance of the code,
the impact and quantity of the bugs and a number of other factors, such as
marketing and product design, which are outside the typical developer's control
and which are most definitely outside the scope of code quality and therefore
this article.

I would also argue that the maintainability of a piece of code is simply the
combination of the readability and the writability of the code.

Thus, the above three metrics can be transformed into a new set of four metrics
which specifically apply to code quality:
- Performance
- Bugs
- Writablity
- Readability

For the purposes of the following sections, I will reorder these as follows:
- Bugs
- Writability
- Readability
- Performance

## Bugs

The solution for measuring and targeting bugs has already been found and it's
very simple.

Reduce and remove bugs. Failing that, mitigate their impact with workarounds.

Ok, now that we've got that sorted lets move on to writability.

## Writability

You may be wondering what exactly writability means. You probably have a rough
idea, but that's definitely not convertible to a metric which can be used to
measure code quality.

To me, and for the purposes of this article, the writability of code is a way
of measuring how long it takes to write a piece of code. Some pieces of code
can be written very quickly, while others take longer to reason about. The most
important thing about writing writable code is that if you've already written
it, it doesn't matter how writable it is. Code writability is a problem for
project managers and whiteboard engineering.

There are many factors which impact code writability, like the complexity of a
project and how suitable the development environment is, but these don't matter
because writability is not in the scope of code quality.

## Readability

There are too many measures for code readability. For example, clean code, code
complexity, SOLID principles. These don't conflict, and if you know when to
apply each of them, they can be great. This is because they each cover some
similar set of properties which make code readable.

Instead of picking one or multiple of these however, I choose to use another
metric for determining the readability of a piece of code. This metric is born
out of years of trying to prematurely optimise little snippets of code and
attempting to figure out what the best way to write a piece of code is in
advance. My metric of choice is to take a step back from the code, take a look
at the function, and ask myself, "if I were a new contributor, could I
understand this function?".

It's that simple. Is the code legible, yes or no?

If your answer is no, then the code should be fixed.

If your answer is yes, the code is fine and can be left untouched.

There is however one more question you need to ask yourself, and that is "is
this code necessary?". In keeping with [suckless][1] principles, the less code
the better. You should remove any code that is not necessary.

[1]: https://suckless.org/philosophy

## Performance

Performance is fortunately a topic that has been correctly covered by many
other people before me. I'll try not to repeat what others before me have said
and what others in the future may say. Instead, I'll simply cover the
fundamentals of improving performance.

1.  Test
2.  I was going to put some other dot points, but I realise the only thing you
    really need to do is test, everything else just follows naturally.

Consider the potential performance gains versus readability and writability
tradeoffs. I'm not mentioning bugs here, because bugs really shouldn't be
acceptable, however depending on your situation, changing the behaviour of a
program may not be off the table.

### Testing

There are a few different ways to test code and a few benefits to doing so. The
most common two methods of testing code are:
1. Use a profiler
2. Compare two pieces of code

Using a profiler is very language dependent, so I won't touch on it here. There
are also many good performance optimisation guides which go through how to do
this.

Comparing two pieces of code is usually pretty similar. The process is roughly
run each piece of code on the same hardware, under the same conditions and with
the same inputs. Time them and see which is faster. This is also the simplest
way to improve code performance. Optimise something, it doesn't need to be
fully optimised, just enough that you believe it'll make a difference and then
try to measure that difference.

### Two General Optimisation Tips

Although optimisation is very language and project dependent, there are some
general rules of thumb it can be good to follow.

1.  Use language builtins. Depending on your language of choice, these can
    massively speed up your code. This is especially true in interpreted
    languages. For lower level compiled languages such as C and C++, the
    standard library builtins are usually just as good as anything you can
    write yourself, so you might as well use the standard library version as it
    can save you time and improve readability for anyone familiar with the
    stdlib.
2.  Write code for readability. This will often result in simpler code, which
    in turn executes faster. If not, the compiler can usually optimise simpler
    code much more effectively and simple tricks such as shift left to double
    are already built in to the compiler, so you might as well double for
    readability [^1]. In interpreted languages, this last part doesn't apply,
    however usually interpreted languages are slow enough that the difference
    in performance between a multiply instruction and an add instruction is
    completely negligible in the face of interpreter overhead.

[^1]:   Ironically, in x86 architectures, compilers can optimise doubling a
        number into a `lea` instruction, which is sometimes even faster than a
        shift if you need to do something else with the instruction as well
        such as adding a constant or another variable.

## Afterword

Really the whole point of this article was to provide another perspective on
code readability. I approached this from a first principles kind of style,
which means I also happened to touch a little bit on optimisation.

I think the main takeaway from here is that the best way to determine if code
is "good quality" and "readable" is to just try to read it. If you can
understand what it does, it's well written. If not, something's wrong.
