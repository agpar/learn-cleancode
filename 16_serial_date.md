## Chapter 16: Refactoring `SerialDate`

First, if the code to be refactored is not fully tested, or if you don't fully understand what the
code is doing, you should write tests to fill in the gaps in the existing tests and in your
understanding.

HTML in javadoc is kind of a waste of time.

Why is this class named `SerialDate`? Because it can be serialized to an int. That's not really a
great reason: it's exposing some of the implementation in the class name. Plus if the class inherits
from `Serializable`, why would this information be necessary? The name should probably just be
`Date`, or `DayDate`.

The class inherits from `MonthConstants`, which is just a trick to make a bunch of int constants
accessible in a classes namespace. Composition is much preferable to inheritance for a case like
this.

Many methods take an `int` to specify a month -- why, when `MonthConstants` exists? Instead
`MonthConstants` should be an enum `Month` and should be used in place of ints representing months.

It's odd that this abstract class contains constants like `MAXIMUM_YEAR`, when this is something a
concrete implementation should be worried about. Even worse, this class actually creates instances
of concrete classes using the `createInstance` method. Why does an abstract class know about it's
implementations? The Abstract Factory pattern can be used to take responsibility for the creating of
concrete classes, allowing the abstract class to no longer be responsible for this.

Lots of things in this class are extraneous and can be deleted.

Many improvements are made by designing additional enums and helper classes, and moving
implementation specific attributes out of the abstract class.
