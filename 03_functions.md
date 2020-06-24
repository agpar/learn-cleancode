## Chapter 3: Functions

Functions are the basic building blocks of programs. Using small, clear, well named functions which
only operate at a single level of abstraction is a major key to writing good software.

**Functions Must Be Small**. Smaller than that. If all your functions were under 7 lines you'd be
doing great. Under 5 is even better. Why so small? 

1. For one thing, it helps you to not break all the other rules (mixing abstraction levels, doing
   multiple things, having no side effects). 
2. Second, it's far easier to test and logically verify the correctness of small functions. 
3. Third it forces you to think harder about design and where natural boundaries of responsibility
   and abstraction lie.
4. Fourth, it makes the program more readable, as you can use a descriptive name to say what a
   function is doing. Descriptive function names are often better than comments, as a comment that
   goes stale is easily missed, but a function doing something other than its name implies is
   quickly noticed.

Blocks within loops should also be very short. If you can't express it in 1 or 2 lines, it should
probably be a function call. 

This also means that nested blocks should rarely exist. It should be a function call!

**Functions Should Do Only One Thing**. This has obvious testability and readability benefits. 

How do you count to "one"? It doesn't mean only one statement. "One thing" means doing only
conceptually related operations at a level of abstraction one step below the current one.

> The reason we write functions is to decompose a larger concept (in other words, the name of the
> function) into a set of steps at the next level of abstraction.

Other ways to think about it: if you can extract a function B from A, and the implementation of B is
different (more complex) than its name, then A was doing more than one thing. For example,
extracting a single `if` statement with is usually NOT a meaningful extraction. If your function has
comments for its various "sections" it's likely doing more than one thing.

**Functions Should Operate At A Single Level Of Abstraction**. Low level operations (like appending
values to strings) should not be mixed with high level operations (like making an HTML or DB
request). When they are mixed, it becomes difficult to know what statements are essential and which
are details.

**Follow the Step-Down Rule**. The functions in the program should be organized in descending order
of abstraction. So a function at the top of the class "introduces" the next few functions, which are
at a lower level of abstraction. It should be possible to read the class from top to bottom, only
running into (private) functions whose use has already been seen.

```
java public class Example() { 
    public void A() { B(); C(); }

    private void B() { if (D()) { E(); } return F(); }

    private void D() { ... } private void E() { ... } private void F() { ... }

    private void C() { ...  } } 
```

Another way to think about this is a hierarchy of "TO" paragraphs:

``` 
TO include the setups and teardowns, we include setups, then we include the test page content,
and then we include the teardowns.  
    TO include the setups, we include the suite setup if this is a suite, then we include the
    regular setup.  
        TO include the suite setup, we search the parent hierarchy for the “SuiteSetUp” page and add
        an include statement with the path of that page.  
            TO search the parent. .  
```
    
Following this rule makes it easier to have functions which do "one thing".

**Switch Statements Should Be Avoided**. They are always large, and *almost* always a clue that a
function is doing more than one thing. Switches are also often a clue that an interface or class
hierarchy that *should* exist is being manually implemented (while violating Single Responsibility
and Open Closed Principles).

Switch statements are *fine* in Abstract Factories. Not much anywhere else (so long as you have
polymorphism).

**Functions Should Have Descriptive Names**. A function which is *so hard to name* is often doing
too much. It's OK for a function to have a long name if it's clear and descriptive.

**Function Argument Counts Should Be Minimal**. The fewer arguments a function has, the easier it is
to understand and call.

There is a balance between a functional style, where a function only concerns itself with its
arguments, and a object driven style, where various state features are kept in the instance. I find
it personally difficult to decide when a piece of state should be kept as an instance attribute,
rather than passed around. I guess if a function is private there's no sense being "pure
functional". If a function is not providing a "public service" and has no need to be static, it
could be confusing to market it as so. I'm guessing part of my confusion over this is that I write
classes that do too many things.

**Monadic Functions** are usually either 1) a predicate that answers a question about the single
argument, returning either true or false, or 2) a procedure for transforming a single element
through computation, returning the result of the computation. A third, less common, style is an
"event" function, whose calling is interpreted as an event and may alter some other system state,
typically returning void.

**Boolean Flag Arguments** are a clear indication that the function does at least two things! Simply
avoid them. 

**Dyadic Functions** are twice as bad as monadic ones! Is one of the arguments less important than
the other? Why are things being ignored? 

Dyadic functions are appropriate when the arguments are related and have a natural ordering.
`makePoint(x, y)` is good, `assertEqual(expected, actual)` is less so, as there's no "natural
reason" why expected precedes actual.

Of course, you have to write these some times. However, it's useful to explore opportunities to
avoid them. For instance, `doThing(A, B)` could possibly be replaced with a call to `A.doThing(B)`
(either by extending or wrapping A). Or one of the argument can be made a member of the method's
class.

**Triadic Functions and Longer** are twice as bad again. Try to avoid them. It's rare to have 3 or
more things which have an obvious natural ordering. The function quickly becomes a headache, as even
calling it requires multiple back and forths to get the signature right.

**Verbs And Keywords**: Function name and argument names should compliment each other. For instance,
a verb/noun pair which clearly describes what the function does. Function names can also help with
longer arguments, for example, `assertExpectedEqualsActual(expected, actual)` gives the arguments an
obvious ordering.

Functions should **Have No Side Effects**. If your function does *something* not obvious based on
its name, consider it like lying.

**Output Arguments** (equivalently, mutating arguments) are rarely desirable in object oriented
languages. If you need to change *something* (like appending to a list), make that thing a property
of the class. `report.appendFooter()` is preferable to `appendFooter(StringBuffer report)`.

**Command Query Separation (CQS)** is the idea that a function should *do* something or *answer*
something, but never both. For instance methods, either do something to the instance or answer
something about the instance. A rare exception to this is something like the atomic `boolean
testAndSet`.

**Prefer Exceptions To Error Codes**. Returning an error code is probably a violation of CQS. The
Linux syscall interface is notoriously annoying for this reason. Returning error functions forces
you to be constantly checking for errors, while the Exception mechanism allows them to be handled in
one place.

**Error Handling Is One Thing**. If you need a try-catch block, make it the only top level statement
in function. Have it call another function, which is now "free" from having to consider errors.
Handling errors is "one thing", so don't mix error handling with other concerns.

**Don't Repeat Yourself**. Especially when it comes to algorithms. Extract common functionality. 

The **Single Entry Single Exit** rule for functions (e.g. only 1 return, no breaks or continues) is
*less* useful if your functions are small.

**Write, Then Edit, Edit, Edit**. It's very hard to write a program that respects all these rules on
your first attempt. Don't be discouraged if your first draft of a function/class/module comes out
messy and breaks all these rules. This is normal. In fact, it would be remarkable if you could *see*
all the angles of a problem with such clarity that you could solve it *cleanly* on your first try.
It's difficult to focus on implementing an algorithm *and* making it beautiful all at once. So,
write it once poorly, then don't check it in until you've gotten it up to your standards.

Keep in mind, **your goal with all this** is to tell a story - the story of how the problem is
solved. You are building up a language of functions to tell the story with. If the language is clear
and precise, the story is much easier to understand.
