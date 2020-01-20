## Chapter 12: Emergence

What if there were **four simple properties** you could strive for, and clean code would emerge from applying them?

According to Kent Beck they are:

1. Runs all the tests
2. Contains no duplication
3. Expresses the intent of the programmer
4. Minimizes the number of classes and methods.

Firstly: **Having tests is critical** - they are the only way to verify that a system really works. Fortunately, this forces you into good design decisions: small classes that follow SRP and DIP are easiest to test. 
Secondly: **Having tests is empowering** - it allows you to refactor without fear.

>[When we have tests] we can increase cohesion, decrease coupling, separate concerns, modularize system concerns, shrink our functions and classes, choose better names, and so on. This is also where we apply the final three rules of simple design: Eliminate duplication, ensure expressiveness, and minimize the number of classes and methods.

**Duplication is the enemy of well designed systems**.

Duplication manifests on a line by line level, but also in terms of implementations and responsibilities.

Not all similar looking blocks of code are bad (although it's a strong hint you can reduce duplication), and not all dissimilar looking blocks of code are good (if they duplicate responsibilities or implementations).

Minimizing duplication is useful because duplication is bad, but is also useful because it will help you to notice violations of SRP and places to apply DIP.

The **Template Method Pattern** is a very strong technique for reducing duplication and making smaller classes.

**Expressiveness** is a key quality of good code. The intent of the author should read clearly in the code. This clearly calls for good naming, small methods and classes, using standard procedures and nomenclature, and good clean test. These techniques are all important, but it is also important to put in the effort - it's all too easy to get working code and stop.

**Function and class count should be kept as low as possible**. This means don't create extra excessive numbers of classes and methods. Make the amount appropriate for the amount of concepts and responsibilities.

>High class and method counts are sometimes the result of pointless dogmatism. Consider, for example, a coding standard that insists on creating an interface for each and every class. Or consider developers who insist that fields and behavior must always be separated into data classes and behavior classes. Such dogma should be resisted and a more pragmatic approach adopted.

Note that your classes and methods are still probably too big. It's likely that, while keeping in mind that you can take anything *too* far, the SRP is still worth pursuing with energy.