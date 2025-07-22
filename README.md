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

## Chapter 1: Introduction (It’s All About Complexity)

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

- Incremental development means that software design is never done. Design
happens continuously over the life of a system: developers should always be
thinking about design issues. Incremental development also means continuous
redesign. The initial design for a system or component is almost never the best
one; experience inevitably shows better ways to do things. As a software
developer, you should always be on the lookout for opportunities to improve the
design of the system you are working on, and you should plan on spending some
fraction of your time on design improvements.

- If software developers should always be thinking about design issues, and
reducing complexity is the most important element of software design, then
software developers should always be thinking about complexity. This book is
about how to use complexity to guide the design of software throughout its
lifetime.

- This book has two overall goals. The first is to describe the nature of
software complexity: what does “complexity” mean, why does it matter, and how
can you recognize when a program has unnecessary complexity? The book’s
second, and more challenging, goal is to present techniques you can use during
the software development process to minimize complexity

- The best way to use this book is in conjunction with code reviews. When you
read other people’s code, think about whether it conforms to the concepts
discussed here and how that relates to the complexity of the code. It’s easier to
see design problems in someone else’s code than your own. You can use the red
flags described here to identify problems and suggest improvements. Reviewing
code will also expose you to new design approaches and programming
techniques.

- One of the best ways to improve your design skills is to **learn to recognize red
flags:** signs that a piece of code is probably more complicated than it needs to be.

- Almost all of the examples in this book are in Java or C++, and much of the
discussion is in terms of **designing classes in an object-oriented language.**
However, the ideas apply in other domains as well. Almost all of the ideas related
to methods can also be applied to functions in a language without object-oriented
features, such as C. The design ideas also apply to modules other than classes,
such as subsystems or network services.

## Chapter 2 The Nature of Complexity

- This book is about how to design software systems to minimize their complexity.
The first step is to understand the enemy. Exactly what is “complexity”? How
can you tell if a system is unnecessarily complex? What causes systems to
become complex?

- The ability to recognize complexity is a crucial design skill. It allows you to
identify problems before you invest a lot of effort in them, and it allows you to
make good choices among alternatives. It is easier to tell whether a design is
simple than it is to create a simple design, but once you can recognize that a
system is too complicated, you can use that ability to guide your design
philosophy towards simplicity. If a design appears complicated, try a different
approach and see if that is simpler. Over time, you will notice that certain
techniques tend to result in simpler designs, while others correlate with
complexity. This will allow you to produce simpler designs more quickly.

- Complexity is anything related to the structure of a software system that
makes it hard to understand and modify the system. Complexity can take
many forms. For example, it might be hard to understand how a piece of code
works; it might take a lot of effort to implement a small improvement, or it might
not be clear which parts of the system must be modified to make the
improvement; it might be difficult to fix one bug without introducing another. If
a software system is hard to understand and modify, then it is complicated; if it is
easy to understand and modify, then it is simple.

- You can also think of complexity in terms of cost and benefit. In a complex
system, it takes a lot of work to implement even small improvements. In a simple
system, larger improvements can be implemented with less effort.

- Complexity is more apparent to readers than writers. If you write a piece of
code and it seems simple to you, but other people think it is complex, then it is
complex. When you find yourself in situations like this, it’s worth probing the
other developers to find out why the code seems complex to them; there are
probably some interesting lessons to learn from the disconnect between your
opinion and theirs. Your job as a developer is not just to create code that you can
work with easily, but to create code that others can also work with easily.

- **Symptoms of complexity**

  Complexity manifests itself in three general ways, which are described in the
paragraphs below. Each of these manifestations makes it harder to carry out
development tasks.

- Change amplification:
- Cognitive load
- Unknown unknowns

-  Change amplification 
