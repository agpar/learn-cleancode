## Chapter 7: Error Handling

Error handling is a necessity. Devices and system calls fail. But code whose *logic is obscured by error handling* is NOT clean.

**Use Exceptions Rather Than Error Codes** (when they are available of course). Exceptions are the primary programming language feature that frees you from mixing business logic with error handling logic.

It can be helpful to **Write Your Try-Catch-Finally Block First** when dealing with exception throwing calls. These statements emulate a transaction. Thus, you need to think about how to leave your program in a consistent state after all possible exit routes. It can also be useful to **Write A Test Expecting An Exception** before implementing handling, that is, thinking about error cases first.

**Use Unchecked Exceptions** when possible. Checked exceptions can be a huge pain, as they either force you to handle exceptions at a low level or make all levels of code between throwing and handling aware of the possible exception. 

**Checked Exceptions** are good for *predictable but unpreventable errors that are reasonable to recover from* (file not found, http request failed). That is, you force the caller to be aware of the error (it's predictable) and to decide how they wish to recover from it (i.e. it's reasonable to expect they can do something about it). **Unchecked Exceptions** should be used in all other cases (the error is not expected or not easy to recover from: the program should STOP). Note, you can always *wrap* a checked exception in an unchecked exception and rethrow it if you consider it unrecoverable-from. There is much debate online over whether all or no Exceptions should be checked.

You should **Pass Informative Messages To Exceptions**. Mention the failed operation and why it failed. This will be good for your logs.

**Define Exceptions In Terms Of Caller Needs**. If your Class is providing an interface at a reasonably high level of abstraction, callers don't need to hear about `IOException`s or `TimeoutException`s. They need errors categorized *based on their needs*. Should the operation be attempted again or not? Should recovery be attempted or not? So, wrap low level API exceptions in custom Exceptions classes. Often entire modules only need one, as all failures are essentially the same to the caller (*most* of the time the logger is called and you quit or ask the user to try again). Only specify new Exception types for a module if there is a a legitimate need for callers to handle them differently.

For example, when interfacing with a payment processor, there's only really a few cases the caller cares about: did the operation fail because the processor couldn't be reached (try call again), or because the CC information was invalid (don't try call again) or because the transaction was not approved (get more money, then try again). The dozens of possible errors can all basically fit into on of these three shapes.

As a side benefit, wrapping dependency Exceptions in custom Exceptions reduces coupling with the dependency.

**Don't Use Exceptions To Cover Special Cases**. When a problem has a special case, it can be tempting to throw an exception and let the caller deal with the case. This is slow and ugly. Exceptions should be reserved for truly exceptional cases.

**Don't Return Null**. Classes that return `null` when they fail in some way are trouble for callers. They need to do constant "error checking" for the nulls. It's often better to either throw an exception (if computation really can't be continued) or return a default (such as an empty collection).

**Don't Pass Null**. Sometimes a library requires you to pass `null` for certain functionality (e.g. strtok) -- this should *not* be emulated in your own APIs. Most languages have no good way to defend against being passed a null when not allowed (and methods to deal with it are clunky). In fact, in most cases, if a `null` is passed where one is not expected, the best thing that can happen is that the program stops immediately (as their is an error in the program logic). Since accidental `null` passing is nasty problem, you should not invite confusion by having certain APIs were passing `null` is valid or expected.