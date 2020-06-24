## Chapter 14: Successive Refinement Case Study

This chapter is a case study in refining a simple command line argument parser class `Args`. It
starts as a messy parser that could only deal with boolean flags, then was expanded to handle many
data types. After this expansion it looked like a mess, so TDD and cleaning was used to make it
cleaner. It's a bit too verbose to describe here, but it shows how Martin thinks you should be doing
TDD and cleaning: make sure the tests always pass and make the smallest changes possible between
rounds of testing.

*I sort of disagree with keeping the "current arg" as a piece of state on this class simply because
he wanted to avoid functions with two arguments. I would much rather have the "current arg" be
transient value that is passed to methods. The current arg is a state of a process thats running
(looping over the args), not th class itself.*

Most human programmers have to write code in a dirty way at first, then go back and clean it. It's
critical to refine after the first draft.

TDD is important, since when you write a mess you will want to change it to being not a mess while
still being confident that it works.

>Much of good software design is simply about partitioning—creating appropriate places to put
>different kinds of code. This separation of concerns makes the code much simpler to understand and
>maintain.

*Thoughts: I was looking forward to this chapter, but I don't think it works very well in the way
it's presented. It looks like it would work well as an interactive talk, but following all the
changes to the code presented in this way is just not easy. Maybe it would make more sense if I
followed the process with a source file copy of my own?*
