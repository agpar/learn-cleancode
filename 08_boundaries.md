## Chapter 8: Boundaries

It's very common to need to interface with third party code. Creating good boundaries makes this easier.

A **Tension Exists Between Interface Creators And Consumers**. The creator wants the interface to have broad applicability, while the consumer wants specific and sometimes restricted functionality. The third party code will rarely be *exactly* what you need.

Therefore, you should **Avoid Deep Dependencies On Third Party Code**. Even something like a `HashMap` can provide too much functionality or too little to be safely returned to a caller. This means third party object should not be 'passed around' different modules of the system. It is fine to pass around a `HashMap` inside a single class or related group of classes, but it is somewhat dangerous to accept or return one in a public API, as the "boundary" between the third party code and your own becomes poorly defined.

When learning how to use a new third party dependency, **Consider Writing Learning Tests**. That is, rather than trying to integrate the code with your production code, write a set of unit tests that demonstrate how to set up and use the dependency. This allows you to do precise experiments in a controlled environment. You can also keep the learning tests around, in order to verify that new versions of the dependency do not break functionality you depend on. A set of **Boundary Tests** is a useful thing to have when new upgrades come in.

You can **Use Code That Does Not Yet Exist** by defining a boundary and implementing the API you "hope" to see as a class. When the module is finally written, you can simply write an adapted to map calls from the class you "wish" you had to the one that is actually implemented.

>Code at the boundaries needs clear separation and tests that define expectations. We should avoid letting too much of our code know about the third-party particulars. It’s better to depend on something you control than on something you don’t control, lest it end up
controlling you.
We manage third-party boundaries by having very few places in the code that refer to them. We may wrap them as we did with Map , or we may use an ADAPTER to convert from our perfect interface to the provided interface.