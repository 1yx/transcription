# Learn to Debug

Debugging is the cornerstone(基石) of being a programmer. The first meaning of
verb "debug" is to remove errors, but the meaning that really matters is to see
into the execution(执行) of a program by examining it. A programmer that cannot
debug effectively is blind.

Idealists(理想主义者), those who think design, analysis, complexity(复杂) theory,
and the like are more fundamental(基本) than debugging, are not working
programmers. The working programmer does not live in an ideal world. Even if you
are prefect, you are surrounded(包围) by and must interact with code written by
major software companies, organizations like GNU, and your colleagues. Most of
this code is imperfect(不完善) and imperfectly documented. Without the ability to
gain visibility into the execution of this code, the slightest(丝毫) bump(碰撞)
will throw you permanently(永久). Often this visibility can by gained only by
experimentation: that is, debugging.

Debugging is about the running of programs, not programs themselves. If you buy
something from a major software company, you usually don't get to see the
program. But there will still arise places where the code does not conform(符合)
to the documentation (crashing your entire machine is a common and
spectacular(壮观) example), or where the documentation is mute. More commonly,
you create an error, examine(检查) the code you wrote, and have no clue how the
error can be occurring. Inevitably(必将), this means some assumption(假设) you are
making is not quite correct or some condition arises that you did not
anticipate(预料). Sometimes, the magic trick of staring into the source code
works. When it doesn't, you must debug.

To get visibility into the execution of a program you must be able to execute
the code and observe something about it. Sometimes this is visible, like what is
being displayed on a screen, or the delay between to events. In many other
cases, it involves things that are not meant to be visible, like the state of
some variables inside the code, which lines of code are actually being executed,
or whether certain assertions(断言) hold across a complicated data structure.
These hidden things must be revealed(透露).

The common ways of looking into the 'innards(内脏)' of an executing program can be
categorized as:

- Using a debugging tool,
- Print lining - Make a temporary modification to the program, typically adding
lines that print information out.
- Logging - Creating a permanent window into the programs execution in the form
of a log.

Debugging tools are wonderful when they are stable and available, but the print
lining and logging are even more important. Debugging tools often lag behind
language development, so at any point in time they may not be available. In
addition, because the debugging tool may subtly(巧妙) change the way the program
executes it may not always be practical(实用). Finally, there are some kinds of
debugging, such as checking an assertion against a large data structure, that
require writing code and changing the execution of the program. It is good to
know how to use debugging tools when they are stable, but it is critical to be
able to employ the other two methods.

Some beginners fear debugging when it requires modifying code. The is
understandable - it is a little like exploratory(探索) surgery. But you have to
learn to poke(戳) at the code and make it jump; you have to learn to experiment
on it and understand that nothing that you temporarily do to it will make it
worse. If you feel this fear, seek out mentor - we lose a lot of good
programmers at the delicate(精巧) onset of their learning to this fear.

# How to Debug by Splitting the Problem Space

Debugging is fun, because it begins with a mystery. You think it should do
something, but instead it does something else. It is not always quite so simple
--any examples I can give will be contrived(做作) compared to what sometimes
happens in practice. Debugging requires creativity and ingenuity(创造力). If there
is a single key to debugging it is to use the divide(划分) and conquer(征服)
technique on mystery.

Suppose, for example, you created a program that should do then things in a
sequence. When you run it , it crashes. Sine you didn't program it to crash, you
now have a mystery. When you look at the output, you see that the first seven
things in the sequence were run successfully. The last three are not visible
from the output, so now your mystery is smaller: 'It crashed on thing #8, #9,
or # 10.'

Can you design an experiment to see which thing it crashed on? sure. You can use
a debugger or we can add print line statements (or the equivalent(当量) in what
ever language you are working in) after #8 and #9. When we run it again, our
mystery will be smaller, such as 'It crashed on thing #9.' I find that
bearing(举止) in mind exactly what the mystery is at any point in time helps keep
one focused. When several people are working together under pressure on a
problem it is easy to forget what the most important mystery is.

To a true beginner, the space of all possible errors looks like every line in
the source code. You don't have the vision you will later develop to see the
other dimensions of the program, such as the space of executed lines, the data
structure, the memory management, the interaction wight foreign code, the code
that is risky, and the code that is simple. For the experienced programmer,
these other dimensions from an imperfect but very useful mental model of all the
things that can go wrong. Having that mental model is that helps one find the
middle of the mystery effectively.

Once you have evenly subdivided(细分) the space of all that can go wrong, you must
try to decide in which space the error lies. In the simple case where the
mystery is: 'Which single unknown line makes my program crash?', you can ask
yourself: 'Is the unknown line executed before or after this line that I judge
to be executed in the  middle of the running program?' Usually you will not be
so lucky as to know that the error exists in a single line, or even a single
block. Often the mystery will be more like: 'Either there is a pointer in that
graph that points to the wrong node, or my algorithm that adds up the variables
in that graph doesn't work.' In that case you may have to write a small program
to check that the pointers in the graph are all correct in order to decide which
part of the subdivided mystery can be eliminated(淘汰).
