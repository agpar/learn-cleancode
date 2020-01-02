## Chapter 5 Formatting

*Nice* looking and uniformly formatted code is a sign of professionalism. It's a good sign when one pays attention to detail here.

You or your team should agree on a set of simple rules and follow them. It helps if you have a linter to enforce this.

>Code formatting is important. It is too important to ignore and it is too important to treat religiously. Code formatting is about communication, and
communication is the professional developer’s first order of business.

### Vertical Formatting

**How Long Should Files Be**? Probably quite short, as in not much more than 200-500 lines. Files are a unit of abstraction, if they are too large and complicated you can always split them. 

Try to **Organize Your Files Like A Newspaper Article**. This means a headline (file name) that is clear and descriptive. The first few lines should give the purpose in broad strokes. Detail and minutia should appear farther down (this is related to the "Step-Down" rule in Chapter 03). The newspaper itself contains many small articles. Only a few are large. This again is worth emulating.

**Use Line Breaks To Distinguish Concepts**. Just like in writing. Similarly, group related statements together *sans* line breaks to make their relationship clear.

Indeed **Vertical Distance** is a powerful tool for making code readable. Related lines should appear as closely together as possible.

This means **Variable Declaration Should Occur Close To Usage**. Functions should be short enough that declaring locals at the start of the function does not break this rule. In rare cases, a variable can be declared before a loop or block. But the function is probably getting long at that point.

**Instance Variable Should Appear At The Top Of A Class**. This is the convention. Strictly, it does not matter exactly where you place them, as they can be (and sometimes are) used in every method of a class. So, follow convention.

For **Dependent Functions**, place them close together and if possible put the caller before the callee. In general, functions with a **Strong Conceptual Affinity** - meaning they perform similar tasks or are otherwise related - should be grouped close together vertically.

In general **Call Dependency Should Flow Downwards**. Unfortunately this can be annoying to implement in C. 

>As in newspaper articles, we expect the most important concepts to come first, and we expect them to be expressed with the least amount of polluting detail. We expect the low-level details to come last.

### Horizontal Formatting

**How Long Should A Line Be?** It's not as strict as it used to be, but stick to a consistent upper limit. Something like 80, 100, or 120.

**Horizontal White Space** can be used to accentuate elements of an expression. For instance, putting spaces around binary operators accentuates
the two sides of the operation, while omitting spaces between a function name and it's arguments accentuates their closeness.

**Aligning Multiple Lines** (like in a table) is rarely useful. This is a holdover from the assembly days. 

**Indentation Is Obviously Important**. It usually only causes trouble to "break" the rules for tiny functions or blocks.

While it's fine to have personal preferences, recognize that working on a team means you all have to agree and pull in the same direction on things like this.

