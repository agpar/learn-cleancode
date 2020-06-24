## Chapter 6: Objects and Data Structures

The whole point of private variables is to give yourself the freedom to change internal
representation later. So **Don't Automatically Add A Getter And Setter To Everything!** If you put a
getter and setter on everything, you may as well just make the variables public.

> Hiding implementation is not just a matter of putting a layer of functions between the variables.
> Hiding implementation is about abstractions! A class does not simply push its variables out
> through getters and setters. Rather it exposes abstract interfaces that allow its users to
> manipulate the essence of the data, without having to know its implementation.

The goal of encapsulation is to not expose details of data representation.

Consider the **Data/Object Anti-Symmetry**. Objects hide data behind abstractions and expose methods
to operate on that data. Data structures simply hold data together, exposing everything, with no
meaningful methods. *These two things are near complete opposites.*

When working with a group of related data structures and procedures, adding a new data structure
requires updating all procedures. Conversely, when working with a group of related objects and
methods, adding a new method requires (possibly) updating all objects. What is hard for OO is easy
for procedural, and vice versa. Thus BOTH are useful: if you intend to add *many* new data
    structures, Objects are the way to go, but if you expect to be constantly adding functionality,
    it may be easier to use Data Structures.

**The Law Of Demeter** states that a method `f` of a class `C` should only call methods on :

* the class `C`, 
* objects created in `f`
* objects passed to `f`
* instance objects of `C`

In particular, `f` should *not* invoke method on objects *returned* by any of the above. IMO this is
*slightly* wild, as a strict interpretation would mean you couldn't call `String.replace()` on a
string returned by a call to a String producing function. The *goal* of this law is to reduce the
depth of dependence on foreign code.

A snippet of code like `this.context.getOptions().getTempDir().getPath()` violates this law. This is
called a **Train Wreck**, because it looks like a bunch of tightly coupled train cars. Worse, it
tends to hide how *deep* the chain of dependence is. When this code is expanded, we can see how many
foreign classes the code is depending on.

``` 
Options opts = this.context.getOptions();
File tempDir = opts.getTempDir();
String tempPath = tempDir.getPath();
```

This function, therefore, has to have a high degree of knowledge about multiple classes - that is,
it has to "see through" the abstraction provided by a "nearby" object in order to access a
"stranger" object.

Confusingly, the above would be *OK* if the elements returned were Data Structures rather than
Objects, as Data Structures are not tasked with abstracting their underlying data.

The **Worst Of Both Worlds** occurs when "hybrid" is created: a Data Structure (all its data is
public, or accessible and mutatable publicly) mixed with significant behavior methods. This makes it
hard to add functionality *and* hard to add new data structures. A class should attempt to work
either as an Object (with a usefully abstracted interface) or a Data Structure (with *no* behavior
of its own) -- never both!

>[Hybrids] are indicative of a muddled design whose authors are unsure of—or worse, ignorant
>of—whether they need protection from functions or types.

So how do we respect this law? It is tempting to "explode" the interfaces of classes, adding lots of
methods so that all callers only have to make "one call" to get what they want. This is an
acknowledged difficulty, that is best counteracted with careful thought about what you want to do
and what class should most reasonably take responsibility for doing that thing.

**Data Transfer Objects** are classes with no functionality, they only hold variables. These are
good for talking to databases and sockets. 

It's useful to question whether the common act of making all variables private and only settable
through the constructor actually provides any benefit. It *can* make the object immutable, but is
this always necessary? How bad would the world be if the object just had public variables?

**Active Records** are DTOs, typically, a representation of data stored in a database or elsewhere
(look for the `save` method). Do NOT treat these as objects - this is a very awkward thing to do.
You will quickly end up in the **Worst Of Both Worlds**. It is *simple* to wrap the Active Record in
an Object which provides an abstract interface for manipulating the data.
