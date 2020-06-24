## Chapter 2: Meaningful Names

Everything in your program requires a name. Choosing good names takes time, but it's worth it.

Use **Intention Revealing Names**. This means the name should tell you what it is, why it exists,
and what it does. 

```java 
// This is NOT a useful variable name.  
int d; // Elapsed time in days

// One of these would be much better!  
int elapsedTimeInDays; 
int daysSinceCreation; 
int daysSinceModification; 
int fileAgeInDays; 
```

You need to **Avoid Disinformation**. For instance, using the word "List" in a name is a bad idea if
the thing is technically an Array. Similarly, using abbreviations that have multiple meanings can
cause confusion.

Giving similar classes similar names is good, while failing to do this is a kind of disinformation.
If things are similar, it helps (especially in IDEs and docs) if they sort close to each other
alphabetically.

It's important to **Make Meaningful Distinctions**. If two things are indeed different, their names
should reflect this. Avoid numbering identifiers. 

It's also not meaningful to add "noise words" like "data" or "info" to class names, or "variable" or
"object" in a variable. Similarly, it's usually not helpful to include the name of the class in a
variable name, especially not in statically typed languages.

**Use Pronounceable Names**. This is obvious. If a name *looks* like gibberish in your natural
language, it's easy to ignore it, confuse it with other names, and it's difficult to talk about.
Name should also **Be Searchable**. This means avoiding single character names - the only case these
really make sense is as loop indexes (by tradition and tiny scope).

**Avoid Name Encodings**. Special systems for naming which reveal details of the underlying type or
access rights of a variable are useless in modern environments and languages and are typically
ignored. Similarly, encoding a concrete type name into a variable name just makes refactoring
harder.

**Avoid Mental Mapping**. Needing to "map" variable names onto concepts in your head is a bad sign!
Even loop variable names like `i` should be replaced with something more clear if you find this
happening.

**Class Names** should be nouns or noun-phrases. Not a verb. Avoid useless fluff words like
"Manager", "Processor", "Data" and "Info".

**Method Names** should be verbs or verb-phrases. Use the standard `get`, `set`, and `is` prefixes
to name getters, setters and predicates. When you have multiple constructors, it is often preferable
to use static factory methods, e.g. `Complex.FromRealNumber(32.0)` is preferable to `new
Complex(32.0)`.

**Pick One Word Per Concept**. For instance, don't use `get` and `fetch` as prefixes to getters.
Choose one (and choose `get`). If a `fetch` prefixed method appears, it should be doing something
conceptually different than simply reading a private variable (such as making a HTTP call).
Similarly, it is something tempting to use generic terms like "controller" and "manager"
interchangeably. Try not to do this - have them each mean something distinct. 

**Don't Pun**. In contrast to the last point, you should not use the same name to refer to
conceptually different tasks. For instance, don't use `add` to both do addition and list appending.

**Use Solution Domain and Problem Domain Names When Appropriate**. Sometimes there are obvious
solution domain names for concepts, such as `Queue`, `Stack`, or `Visitor`. You should use these
when they are accurate. Other times, it's best to use a term from the problem domain, such as
`Reconciliation`. It's important to think about which domain you are pulling from and which is
appropriate. 

**Add Meaningful Context**. If multiple variables are related, why not make a class to group them
together? `Customer.state` is way more ambiguous than `Customer.Address.state`. In general, be very
liberal in grouping related concepts together into a class.

Naming is hard. It requires thought and effort and a shared cultural background. You should not
worry too much about other developers objecting to name changes - in most cases the IDE removes all
friction from looking up a name, and people generally appreciate improved names.

