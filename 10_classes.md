## Chapter 10: Classes

**Classes Should Be Organized** in the following order: public static constant, private statics, private instance, functions. Private "helper" functions should directly follow the public method that uses them (following step-down rule).

**Encapsulation** means, in a very basic sense, making things private unless there's a very good reason for them to be public.

**Classes Should Be Small**. Unlike functions, where *small* refers to line count, for classes we are referring to the *number of responsibilities*. If you're tempted to put words like *manager* or *processor* in the class name, it's likely doing too much. The class name should say exactly what the one responsibility it has is.

**The Single Responsibility Principle (SRP)** states that a class should only have one reason for change. It follows that a class should only have one responsibility. 

SRP is simple to state and understand, but often abused. Why? For one, "getting code to work" and "making code clean" are separate activities, and the second is often left undone. Another reason is developers fear that having many small classes will make it harder to see the big picture - there is a worry that navigating from class to class breaks the flow of understanding. 

The cure for the first reason is simply caring.

The cure for the second is realizing that whether the system has many small classes or few big ones, there is the same amount of logic in it. It's analogous to stuffing all your tools in a small number of shelves or having many small clearly labeled shelves. In fact, the former actually forces readers to wade through more they don't care about on their way to finding what they do care about. 

**Classes Should Be Cohesive**. They should have a small number of instance variables, and all of their methods should read or manipulate one or more of them.

>A class in which each variable is used by each method is maximally cohesive.

Although, this is not a goal to strive for, but the logical limit of the definition. Cohesion should be high, but not necessarily maximal.

While keeping functions small and their argument lists short, you may notice that some of the instance variables are only used by a subset of the methods, and cohesion is dropping. *This is almost always a hint that your class is actually two or more classes!* The same heuristic applies when you have a private helper functions that is only used by a subset of the public functions.

**Maintaining Cohesion Means Many Small Classes**.

There is a "virtuous cycle" of code cleaning that starts with breaking up large functions and ends in discovering new classes:

1. Method is too large, so you decide to split it up.
2. Argument list for new sub-method would be too long, so you promote some of the function variables to class variables.
3. 1 and 2 are repeated a few times...
4. There is now a subset of the instance variables used by only a subset of the methods: a new class is discovered.

**Organizing For Change** means being hyper aware of when classes are taking on multiple responsibilities. Any time a class has n>1 reasons to "open it up" and change it (SRP), you increase the risk of breaking it in proportion to n. This gets especially dire if the testing situation is not good.

For example, a class `SQL` that handles transforming objects into properly formatted string SQL queries is deceptively complicated. It needs to change its functionality if a new statement type is supported and if a previous statement type is modified. It will have helper functions specifically for dealing with Selects and Inserts respectively. Breaking it up into classes for each statement (`SelectSql`, `InsertSql`, etc...) which all inherit from an abstract `SQL` class gives you many "excruciatingly simple" classes which each respect SRP, are easy to test and understand.

**To Isolate From Change, Depend On Interfaces**. Concrete classes are subject to change and outside dependencies. Interfaces are far more static. In addition, it is substantially easier mock an interface dependency than a concrete one for testing.

The **Dependency Inversion Principle** means that classes should rely on abstractions rather than concrete details -- in practice, this means depending on interfaces whenever possible.
