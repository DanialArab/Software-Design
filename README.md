# A Philosophy of Software Design

## Preface

- The most fundamental problem in computer science is problem
decomposition: how to take a complex problem and divide it up into pieces that
can be solved independently. Problem decomposition is the central design task
that programmers face every day, and yet, other than the work described here, I
have not been able to identify a single class in any university where problem
decomposition is a central topic. We teach for loops and object-oriented
programming, but not software design.

- Many people assume that software design skill is an innate talent that cannot be taught.
However, there is quite a bit of scientific evidence that outstanding performance
in many fields is related more to high-quality practice than innate ability (see, for
example, Talent is Overrated by Geoff Colvin).

- Related class taught by the author: CS 190 at Stanford University

- I recommend that you take the suggestions in this book with a grain of salt.
The overall goal is to reduce complexity; this is more important than any
particular principle or idea you read here. If you try an idea from this book and
find that it doesn’t actually reduce complexity, then don’t feel obligated to keep
using it (but, do let me know about your experience; I’d like to get feedback on
what works and what doesn’t).

## CHAPTER 1: Introduction (It’s All About Complexity)

- All programming requires
is a creative mind and the ability to organize your thoughts. If you can visualize a
system, you can probably implement it in a computer program.

- There are two general approaches to fighting complexity, both of which will
be discussed in this book. The first approach is to **eliminate complexity by
making code simpler and more obvious.** For example, complexity can be reduced
by eliminating special cases or using identifiers in a consistent fashion.
The second approach to complexity is to **encapsulate it, so that programmers
can work on a system without being exposed to all of its complexity at once**. This
approach is called **modular design**. In modular design, a **software system is
divided up into modules, such as classes in an object-oriented language**. The
modules are designed to be **relatively independent of each other**, so that a
programmer can work on one module without having to understand the details of
other modules.

- Because software is so malleable (Easily influenced or changed), software design is a continuous process
that spans the entire lifecycle of a software system; this makes software design
different from the design of physical systems such as buildings, ships, or bridges.
However, software design has not always been viewed this way. For much of the
history of programming, design was concentrated at the beginning of a project,
as it is in other engineering disciplines. The extreme of this approach is called
the **waterfall model**, in which a project is divided into discrete phases such as
requirements definition, design, coding, testing, and maintenance. In the
waterfall model, each phase completes before the next phase starts; in many
cases different people are responsible for each phase. The entire system is
designed at once, during the design phase. The design is frozen at the end of this
phase, and the role of the subsequent phases is to flesh out and implement that
design.

- Unfortunately, the waterfall model rarely works well for software. Software
systems are intrinsically more complex than physical systems; it isn’t possible to
visualize the design for a large software system well enough to understand all of
its implications before building anything. As a result, the initial design will have
many problems. The problems do not become apparent until implementation is
well underway. However, the waterfall model is not structured to accommodate
major design changes at this point (for example, the designers may have moved
on to other projects). Thus, developers try to patch around the problems without
changing the overall design. This results in an **explosion of complexity.**

- Because of these issues, most software development projects today use an
**incremental approach such as agile development,** in which the initial design
focuses on a small subset of the overall functionality. This subset is designed,
implemented, and then evaluated. Problems with the original design are
discovered and corrected, then a few more features are designed, implemented
and evaluated. Each iteration exposes problems with the existing design, which
are fixed before the next set of features is designed. By spreading out the design
in this way, problems with the initial design can be fixed while the system is still
small; later features benefit from experience gained during the implementation of
earlier features, so they have fewer problems.

- 
