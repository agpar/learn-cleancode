## Chapter 15: Junit Internals

Like chapter 14, a walk-through example of refactoring a class.

This chapter works a lot better though, as the class is a little bit smaller, and I agree more with
(most of) the changes made. Also, it starts from a class that is already "pretty good" and makes it
"really good" instead of showing you all the changes a class goes through from start to end. 

Some of my thoughts:

* Combining `findCommonPrefix()` and `findCommonSuffix()` into a single method to make clear their
  temporal dependence works pretty well. In order to ensure that the temporal dependence is obvious
  here, there is no longer a `findCommonSuffix()` method - only a `findCommonPrefix` and a
  `findCommonPrefixAndSuffix` method. I find this a little awkward, and probably would have stuck
  with `findCommonSuffix(String prefix)` to make the dependence clear. However, my preferred
  approach does not force the caller to pass the correct argument, so it's a mixed bag. To me, the
  "pipeline" of temporally dependent methods is obvious and has nice analogies to UNIX text
  processing.
* Having a `shouldBeCompacted()` and `shouldNotBeCompacted` method just seems strange to me. I think
  in cases like this it suffices to implement the positive case and allow callers to flip it if
  necessary. If the boolean logic is simpler to express the negative case, simply doing `!(<logic>)`
  in the method for the positive case gives you the best of both worlds. Also, I prefer to only
  implement the positive case as negation and double negation is confusing. 
* The renaming changes, especially carefully distinguishing indexes from lengths and how it allowed
  him to remove pointless branches, is all positive changes.
