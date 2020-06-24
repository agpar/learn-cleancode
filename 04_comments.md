## Chapter 4: Comments

Comments are not "all good". They are *compensation* for lacks of language expressiveness and skill.

>The proper use of comments is to compensate for our failure to express
ourself in code. Note that I used the word failure. I meant it. Comments are always failures. We
must have them because we cannot always figure out how to express ourselves without them, but their
use is not a cause for celebration.

Comments are *worse* than code simply because they go out of date. Once they do, they are lies.
There is very little warning when this happens, or incentive to fix them. It takes energy to keep
them up to date, energy that's better spent on the actual code. 

Inaccurate comments are worse than no comments.

**Comments Do Not Make Up For Bad Code**. If code is confusing, has strange assumptions, and is hard
to use, it's better the *clean* it than to document it.

You can and should **Explain Yourself With Code**. Is a condition check a little cryptic? Extract
the predicate to a well named function.

Here is a list of cases where comments can be **good**.

* **Legal Comments**: Sometimes a license is required.
* **Informative Comments**: For example, providing an example of the kind of a string a compiled
  regex is looking for.
* **Explanation of Intent**: When you're forced to do something you predict will raise eyebrows, it
  can be good to leave a comment.
* **Clarification**: If you're returning or passing obscure arguments, clarifying comments can be
  helpful. You should try making it clearer, but often (when interfacing with a library) this is not
  always easy. Be warned that these can be a trap if they are incorrect.
* **Warning of Consequences**: At key points, it can be helpful to explain why a certain feature is
  disabled or that a library class makes some assumption (e.g. is not thread-safe)
* **TODOs**: Sometimes you just don't have the time to do something perfectly.
* **Amplification**: When a step appears banal but is actually critical, a comment indicating this
  can be helpful.
* **Docs**: If the API will be public, you ought to document it.


Here is a list of ways comments can be **bad**. Most comments are.

* **Mumbling Comments**: A hastily written, unclear comment. Asks more questions than it answers. If
  you need to go hunting for answers after reading the comment, it's a mumble.
* **Redundant Comments**: If it simply restates the code (with a necessary degradation of
  precision), what is it doing but adding clutter? If the code is so complex it needs to be
  explained, simplify it until a comment would be redundant.
* **Misleading Comments**: Worse than no comments.
* **Mandated Comments**: It's just not true that *every* function needs a header comment. Be
  judicious.
* **Journal Comments**: Sometimes people keep a "journal" comment at the top of a module. It's just
  bad git.
* **Noise Comments**: Simply stating useless or obvious information is a waste of space. Angry with
  the code? A comment expressing this is pointless noise.
* **Comments In Place of Well Named Functions and Variables**. If a few lines of code seem cryptic,
  maybe it's because you're lacking well named functions and variables to express it. Don't use
  comments as a crutch in this case.
* **Position/Section Markers**. Rarely useful. Often a sign that a new class or file is needed.
* **Closing Brace Comments**. In deeply nested code, it can be tempting to mark what structure a `}`
  corresponds to. Stop writing deeply nested code.
* **Attributions**: Git keeps track of this.
* **Commented Out Code**: Commented out code is hard to delete once you forget about it. Source
  control should already have it. Or put it in it's own function. Or, best, just delete it.
* **HTML In Comments**: Don't do it. Hard to read. Your tool should handle it.
* **Nonlocal Information**: Don't write about things which are out of the control of the scope of
  the comment. They will change and the comment will be wrong.
* **Too Much Information**: You don't need a history lesson in every doc string. It's very rare that
  people actually read these.
* **Inobvious Connections**: It should be clear how a comment relates to the code it's placed next
  too. If it's not clear, what's the point of it?
* **Function Headers and Doc Strings**: If a function is small, and especially if it is not part of
  a public API, it is worth seriously questioning whether or not it needs a doc string. The same
  applies to javadocs.
