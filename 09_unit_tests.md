## Chapter 9: Unit Tests

TDD is mainstream now, and it's a key to reliable software. However, in the rush to adopt automated
testing, some subtle points have been lost.

**The Three Laws Of TDD** are as follows:

1. You may not write production code until you write a failing unit test.
2. You may not write more of a unit test than is sufficient to fail, and not compiling is failing.
3. You may not write more production code than is sufficient to pass the current failing test.

These three laws lock you into a loop about 30 seconds long. The tests and code are written
together. It also has the nice effect of forcing you to think about your interface/specification
every 30 seconds.

If you really follow these laws, you will write hundreds of tests, such that even managing them all
can be a problem.

**Tests Need To Be Kept Clean**. Having dirty tests is maybe *worse* than having no tests. Tests and
production code need to evolve together. If test code is allowed to be dirty, it is hard to change,
and tests will begin to seem like a liability. **Test Code Is Just As Important As Production
Code**.

If tests are not kept clean, they will become an every increasing headache. They will get thrown
away. **Without Unit Tests Production Code Is Inflexible**. With tests, you can be reasonably sure
that a change does not break core functionality. Without tests, every change is potentially a bug.
Unit tests are the key to maintainability, flexibility an reusability. 

**Readability Is The Key To Clean Tests**. Tests that are hard to read are hard to change. Just like
clean production code, each function should be operating at a distinct level of abstraction, with
the test method itself as the highest. One readability key is to follow the "Build Operate Check"
pattern for tests. 

**Develop A Testing API**. Don't feel constrained to use the exact same APIs that source code uses
to interact with classes. Build an API on top of these that simplify and clarify functions
(specialized setups and teardown functions, specialized assertion functions, etc).

While standards of code clarity should be equivalent for test and production code, **Their Exists A
Dual standard For Efficiency**. Namely, test code is allowed to be less efficient than the
production code, simply because the testing environment is *not* the production environment.

It's true that **The Number Of Asserts In A Test Should Be Minimized**, but it's not necessarily the
case that "one and only one" assert should exist per test. Sometimes there really are a couple
things you need to check that all have the same pre conditions. You can use Template Method pattern
or the @Before attributes to reduce code duplication if you really desire to have one and only one
assert per method.

A better rule of thumb may be **One Concept Per Test**. Test functions should really only test one
"thing". If the reason for multiple assertions is that you are testing multiple things, then those
really *should* be split up.


Tests should follow the F.I.R.S.T. acronym.

* **F**ast: if tests take forever to run, you won't run them. So you won't catch mistakes quickly.
  Their value is diminished.
* **I**ndependent: All tests should be able to run in any order and have no reliance on each other. 
* **R**epeatable: Tests should be able to run in any environment. This means having no dependence on
  outside variables (the network, the database, etc.). If you can't run the test in every
  environment, you won't always run them. Similarly, test results should be deterministic.
* **S**elf-Validating: Tests should either pass or fail. No ambiguity. You should not have to
  manually inspect output to determine if it worked.
* **T**imely: Tests should be written in a timely fashion. Tests should be written just before
  production code. If you wait until after, you'll probably find the production code hard to test.

The importance of clean, maintainable and flexible unit tests can not be overstated. It's what gives
you flexibility.
