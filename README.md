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

-  **Change amplification**: The first symptom of complexity is that a seemingly
simple change requires code modifications in many different places. For
example, consider a Web site containing several pages, each of which displays a
banner with a background color. In many early Web sites, the color was specified
explicitly on each page, as shown in Figure 2.1(a). In order to change the
background for such a Web site, a developer might have to modify every existing
page by hand; this would be nearly impossible for a large site with thousands of
pages. Fortunately, modern Web sites use an approach like that in Figure 2.1(b),
where the banner color is specified once in a central place, and all of the
individual pages reference that shared value. With this approach, the banner
color of the entire Web site can be changed with a single modification. One of
the goals of good design is to reduce the amount of code that is affected by each
design decision, so design changes don’t require very many code modifications.

- **Cognitive load**: The second symptom of complexity is cognitive load, which
refers to how much a developer needs to know in order to complete a task. A
higher cognitive load means that developers have to spend more time learning
the required information, and there is a greater risk of bugs because they have
missed something important. For example, suppose a function in C allocates
memory, returns a pointer to that memory, and assumes that the caller will free
the memory. This adds to the cognitive load of developers using the function; if a
developer fails to free the memory, there will be a memory leak. If the system
can be restructured so that the caller doesn’t need to worry about freeing the
memory (the same module that allocates the memory also takes responsibility for
freeing it), it will reduce the cognitive load. Cognitive load arises in many ways,
such as **APIs with many methods, global variables, inconsistencies, and
dependencies between modules.**

- System designers sometimes assume that complexity can be measured by
lines of code. They assume that if one implementation is shorter than another,
then it must be simpler; if it only takes a few lines of code to make a change, then
the change must be easy. However, this view ignores the costs associated with
cognitive load. I have seen frameworks that allowed applications to be written
with only a few lines of code, but it was extremely difficult to figure out what
those lines were. **Sometimes an approach that requires more lines of code is
actually simpler, because it reduces cognitive load.**

- **Unknown unknowns**: The third symptom of complexity is **that it is not
obvious which pieces of code must be modified to complete a task, or what
information a developer must have to carry out the task successfully**. Figure
2.1(c) illustrates this problem. The Web site uses a central variable to determine
the banner background color, so it appears to be easy to change. However, a few
Web pages use a darker shade of the background color for emphasis, and that
darker color is specified explicitly in the individual pages. If the background
color changes, then the the emphasis color must change to match. Unfortunately,
developers are unlikely to realize this, so they may change the central bannerBg
variable without updating the emphasis color. Even if a developer is aware of the
problem, it won’t be obvious which pages use the emphasis color, so the
developer may have to search every page in the Web site.

- Of the three manifestations of complexity, **unknown unknowns are the worst.**
**An unknown unknown means that there is something you need to know, but there
is no way for you to find out what it is, or even whether there is an issue**. You
won’t find out about it until bugs appear after you make a change. Change
amplification is annoying, but as long as it is clear which code needs to be
modified, the system will work once the change has been completed. Similarly, a
high cognitive load will increase the cost of a change, but if it is clear which
information to read, the change is still likely to be correct. With unknown
unknowns, it is unclear what to do or whether a proposed solution will even
work. The only way to be certain is to read every line of code in the system,
which is impossible for systems of any size. Even this may not be sufficient,
because a change may depend on a subtle design decision that was never
documented.

- One of the most important goals of **good design is for a system to be obvious.**
This is the opposite of high cognitive load and unknown unknowns. In an
obvious system, **a developer can quickly understand how the existing code works
and what is required to make a change**. An obvious system is one where a
developer can make a quick guess about what to do, without thinking very hard,
and yet be confident that the guess is correct. Chapter 18 discusses techniques for
making code more obvious.


- **Causes of complexity**: Complexity is
caused by two things: dependencies and obscurity.

- **Dependencies:** For the purposes of this book, a dependency exists when a given piece of
code cannot be understood and modified in **isolation**; the code relates in some
way to other code, and the other code must be considered and/or modified if the
given code is changed. In the Web site example of Figure 2.1(a), the background
color creates dependencies between all of the pages. All of the pages need to
have the same background, so if the background is changed for one page, then it
must be changed for all of them.

- The **signature of a method** creates a dependency between the
implementation of that method and the code that invokes it: if a new parameter is
added to a method, all of the invocations of that method must be modified to
specify that parameter.

- **Dependencies are a fundamental part of software and can’t be completely
eliminated. In fact, we intentionally introduce dependencies as part of the
software design process**. Every time you **write a new class you create
dependencies around the API for that class**. However, one of the goals of
software design is to reduce the number of dependencies and to make the
dependencies that **remain as simple and obvious as possible.**

- Consider the Web site example. In the old Web site with the background
specified separately on each page, all of the Web pages were dependent on each
other. The new Web site fixed this problem by specifying the background color
in a central place and providing an API that individual pages use to retrieve that
color when they are rendered. The new Web site eliminated the dependency
between the pages, but it created a new dependency around the API for retrieving
the background color. Fortunately, the new dependency is more obvious: it is
clear that each individual Web page depends on the bannerBg color, and a
developer can easily find all the places where the variable is used by searching
for its name. Furthermore, compilers help to manage API dependencies: if the
name of the shared variable changes, compilation errors will occur in any code
that still uses the old name. The new Web site replaced a nonobvious and
difficult-to-manage dependency with a simpler and more obvious one.

- **Obscurity**: Obscurity occurs when
**important information is not obvious**. A simple example is a variable name that
is so generic that it doesn’t carry much useful information (e.g., time). Or, the
documentation for a variable might not specify its units, so the only way to find
out is to scan code for places where the variable is used. **Obscurity is often
associated with dependencies, where it is not obvious that a dependency exists.**
For example, if a new error status is added to a system, it may be necessary to
add an entry to a table holding string messages for each status, but the existence
of the message table might not be obvious to a programmer looking at the status
declaration. **Inconsistency is also a major contributor to obscurity**: if the same
variable name is used for two different purposes, it won’t be obvious to developer
which of these purposes a particular variable serves.

- In many cases, **obscurity comes about because of inadequate documentation**;
Chapter 13 deals with this topic. However, **obscurity is also a design issue. If a
system has a clean and obvious design, then it will need less documentation.** The
need for extensive documentation is often a red flag that the design isn’t quite
right. **The best way to reduce obscurity is by simplifying the system design.**

- Together, dependencies and obscurity account for the three manifestations of
complexity described in Section 2.2. **Dependencies lead to change amplification
and a high cognitive load.** And **obscurity creates unknown unknowns, and also
contributes to cognitive load**. If we can find design techniques that minimize
dependencies and obscurity, then we can reduce the complexity of software.

- 
