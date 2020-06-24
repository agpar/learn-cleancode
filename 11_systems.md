## Chapter 11: Systems

How would you build a city? Could you manage all the complexity. Surely not. Cities work because
they have teams working in different sectors and levels of abstraction. Clean code should work like
this.

**Separate Constructing a System From Using It**. Different procedures and employees are used for
building and running a hotel. Software should be the same. The **Startup Process Is A Single
Concern**. 

Lazy initialization of dependencies has some merits, but it should not be used to mix setup logic
with business logic, like below, where Service now is 1) substituting a concrete default that may
not always be appropriate and 2) responsible for knowing how to instantiate a `MyServiceImpl`. This
is a bad break down of modularity and will cause havoc for testing and flexibility.

```
java public Service getService() { 
    if (service == null) { 
        // Good enough default for most cases?
        service = new MyServiceImpl(...); 
    } 
    return service; 
} 
```

How, instead, should we go about setting up graphs of objects that depend on each other?

One option is to **Put All Initialization Code In `main()`**. Then only one class is responsible for
knowing how to wire together dependencies. This is a simple approach, where only `main()` (and
modules called by it) need to know how to build things. All dependency flows *out* of main. The rest
of the code can simply expect that everything has been wired together properly.

When the timing of object instantiation is important (e.g. creating `LineItem`s to fill an `Order`),
**The Abstract Factory Pattern Can Separate Business Logic From Setup Logic**. In this case,
`main()` can instantiate a `LineItemFactory` and make it available to modules that need `LineItem`s,
giving them control of when to make new `LineItem`s but not *how* to.

**Dependency Injection** is a complete solution to this problem, where a special service or
framework is responsible for initializing all objects. The Spring framework for Java is a popular DI
solution.

Note, that **Software Grows Like A Town Into A City**. You would not use a full featured dependency
injection framework for a small project, just as you would not put a 6-lane highway through a small
town. You have to embrace the pace of growth. **If Concerns Are Properly Separated, Software Can
Grow Incrementally**.

**Don't Use Active Records For Anything Other Than Data Transfer**. If you have a `PersonRecord
extends ActiveRecord` class (i.e. it represents a row in a database), you should not combine your
business concerns regarding `Person`s in this class. Have `Person` have an instance of
`PersonRecord` instead. Putting all your business logic in `PersonRecord` is combining concerns, and
makes it basically impossible to unit test. This logic applies to any class you are making to
conform to a framework interface - make conforming to that interface it's only responsibility.

Some concerns, like your strategy for persistence, are cross cutting. They apply to a large number
of classes. **Aspect Oriented Programming** is a technique for dealing with cross cutting concerns
in a consistent and non-invasive way.

>In principle, you can reason about your persistence strategy in a modular, encapsulated way. Yet,
>in practice, you have to spread essentially the same code that implements the persistence strategy
>across many objects. We use the term cross-cutting concerns for concerns like these.

> In AOP, modular constructs called aspects specify which points in the system should have their
> behavior modified in some consistent way to support a particular concern.

Most implementations of AOP for persistence involve defining "Plan Old" objects, then using tools
(e.g.: code, declarative documents, annotations) to define how a proxy for that object should be
built that handles the persistence concerns. Useful tools for this are NHibernate and AspectJ.

Using these tools is highly encouraged. Persistence is one of the most common "cross-cutting"
concerns in an application, and managing that concern carefully and consistently and *isolated* from
other concerns is important.

When your application's business logic is implemented in "Plain Old" objects that are decoupled from
architecture concerns, you gain a large amount of flexibility and testability.

**Optimal system design consists of modularized "Plain Old" objects, where cross cutting concerns
are handled by minimally invasive Aspects**. This architecture can be easily tested and iterated
upon.

With properly architected systems, it's possible to delay decision making until the latest moment,
maximizing opportunities for knowledge and feedback gathering.

However, be aware that while standards and frameworks like NHibernate are useful for many reasons,
they should not become and end on their own. Times and needs change.

**In Conclusion:** Systems need to be clean too. System architecture (e.g. set up, logging strategy,
persistence) should not overwhelm or interfere with business logic. The best way to design systems
is to implement business logic in "Plain Old" objects and use Aspect Oriented Programming to handle
cross cutting architectural concerns noninvasively. When designing your system, use the simplest
tool that works, avoid Building It All Up Front and letting your tools become the master.
