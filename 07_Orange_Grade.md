Grade 2 – Orange
================

Principles
----------

### Single Level of Abstraction (SLA)

**Why?**

Keeping one level of abstraction fosters readability.

-   Evolvability: \*\*\*

-   Correctness: \*

-   Production Efficiency:

-   Continuous Improvement:

-   Single Developer

Lines of code may have different levels of abstraction. Assigning a value to a variable is on a lower level than let's say a method call. This is because beyond the method call can be far more logic than a variable assignment. Even method calls may be on different levels of abstraction. Calling a framework's method is on a different level than a method call within your codebase.

Within one method you should use only one level of abstraction. Otherwise the reader will find it hard to differentiate essentials from details. So if you need to fiddle with bits, don't combine it with method calls.

A helpful analogy is a newspaper article: First comes is the most important thing – the heading. From this you should roughly know what the article is about. The first sentence of the article describes it on a high level of abstraction. The further you get in the article the more details emerge. We can structure our code in a similar way. Class name is the heading. Next are public methods on a high level of abstraction. These may call lower level methods until we are finally at "fiddle-with-bits" level. With this structure at hand I can easily decide which detail level I want to see when looking at a class. If you are only roughly interested in how a class works, you just need to inspect the public methods which reflect functionality on a high level of abstraction. If you want to know further details, you will drill down to private methods.

### Single Responsibility Principle (SRP)

**Why?**

Focus eases understanding. A class having exactly one task is easier to understand than a convenience store.

-   Evolvability: \*\*\*

-   Correctness: \*

-   Production Efficiency:

-   Continuous Improvement:

-   Single Developer

Single Responsibility Principle (SRP) is one of the [SOLID](#solid) principles stating that a calls shall have only **one** responsibility.

Beyond the Single Responsibility Principle stands the idea that changing or enhancing functionality should affect only a few classes. The more classes need to be changed the higher is the risk that problems arise in areas which basically have nothing to do with the enhancement. A SRP violation leads to coupling and increased complexity. It becomes harder to understand the code.

### Separation of Concerns (SoC)

**Why?**

If a code unit does not have a clear purpose, it will be difficult to understand, difficult to use, difficult to enhance and difficult to correct.

-   Evolvability: \*\*\*

-   Correctness: \*

-   Production Efficiency:

-   Continuous Improvement:

-   Single Developer

You should not combine multiple concerns in one class. What is a concern? Concerns a "completely different" purposes. Concern are considered to be orthogonal to each other and especially orthogonal to the main functionality of a functional unit. Samples for typical concerns are: Tracing, logging, transaction handling, caching. If you follow SoC principle, you will extract these concerns into specialized functional units.

The Separation of Concerns principle is closely connected to the Single Responsibility principle. Concerns are a superset of responsibilities. A responsibility ideally consists of exactly one concern which is its core functionality. Nevertheless more often multiple concerns are mingled in one responsibility. This usually cannot be totally avoided. So the principle doesn't say that a responsibility must consist of one concern but just that the concerns need to be separated. For instance within a method multiple concerns shall be clearly visible, so that concerns don't spread willfully over the whole method but are grouped in a way that makes clear what belongs to a certain concern.

Domain Driven Design attempts to strictly separate business domain from infrastructure. So a business domain class must not contain infrastructure like database access but can only represent business logic. Persistence is a "Concern" which has nothing to do with business logic. Separation of Concerns leads to lose coupling and high cohesion. Each component focusses on a single task – its concern - and thereby is easy to understand. All parts of that component would be oriented on that task so that the part a closely connected (high cohesion). Separation of Concerns further leads to well testable components because a focused purpose of a code unit needs less wide tests. Regarding the code unit under test less parameter combinations have to be checked. To live SoC consequently Aspect Oriented Programming (AOP) needs to enhance Object Orientation. That way aspects like transaction handling, tracing or caching can be fully extracted from a method.

### Source Code Conventions

**Why?**

Code is more frequently read than written. Accordingly conventions are important to support reading and conceive code quickly.

-   Evolvability: \*

-   Correctness: \*

-   Production Efficiency:

-   Continuous Improvement:

-   Team

Following aspects are important:

-   Naming conventions

-   Proper comments

Not that other conventions would be irrelevant. Though these two are essential. As with all code conventions sticking to it is more important than how they exactly look like. And it is about the awareness that conventions are necessary.

**Naming Conventions**

**Why?**

Without naming conventions you have to accustom to styles of individual developers again and again.

Naming conventions support understanding while reading coding. For instance it is helpful to make out fields from local variables. Hence this can be supported by a naming convention. Using `this.xyz`, `_xyz` or something else is a matter of taste. Important is only to consequently stick to the chosen convention. Also the need for a naming convention depends on the context. For a class of 400 lines a naming convention to highlight fields from variables appears significant while in compact class the convention will fade into the background. Doing root cause analysis a clean code developer verifies the need for a coding convention.

**Proper Comments**

**Why?**

Unnecessary or wrong comments hamper reading. Code itself shall be clear so that in gets along without comments as far as possible.

Rather than
```
int length; // in mm
```
write
```
int lengthInMM;
```
Rather than
```
public double price() {

// calculates the gross price }
```
write
```
public Money PriceGross() { … }
```
Comments if any shall explain why you are doing something, not what.

Practices
---------

### Issue Tracking

**Why?**

Only written issues are not forgotten and can be efficiently followed-up or delegated.

-   Evolvability: \*

-   Correctness: \*

-   Production Efficiency: \*\*

-   Continuous Improvement: \*

-   Team

Structured issue management is essential to avoid something is lost in first place. Overview over all open topics allows to prioritize and order these topics. No sophisticated tools are necessarily required for that. A board with paper cards can do the trick. Rather than the tool the activity shall be to the fore.

### Automatized Integration Tests

**Why?**

Integration tests ensure the code does what it shall do. It would be a waste of time to do this repetitive activity manually.

-   Evolvability: \*\*

-   Correctness: \*\*

-   Production Efficiency: \*\*

-   Continuous Improvement:

-   Single Developer

When we do code changes we shall be sure not to break anything. This security can be only achieved by testing if the application still behaves same as before. Testing manually after every change is not viable – we need to automatize. The worry to overlook some detail while changing code and break existing code is a big evil in software development. Indifferently if changes are needed to implement new requirements or to improve existing code (refactoring). As long as we are not perfectly sure that everything works same as before that worry persists. And in doubt we keep the code as it is – just because it works. Indispensable refactorings are omitted out of fear to do mistakes.

Automatized integration tests can build a safety net. Either these are attached onto the user interface and test the application through all layers or they are plugged in at a lower level. In any case they test the interaction of multiple functional units.

Accordingly we create integration tests for affected code areas before we apply changes or enhancements. Tools and techniques like WatiN, UI automation and others may be used. Also it would be helpful to have unit test which test single functional units. However the prerequisites for unit tests are probably not yet there: Code has to fulfil the [Single Responsibility Principle](#single-responsibility-principle-srp). Otherwise dependencies will prevent isolated testing. The long-term objective is to have unit tests created before implementation (*test first*). But in first place it requires integration tests to get there. They ensure that after a refactoring the application behaves same as before.

### Read, Read, Read

**Why?**

Reading educates!

-   Evolvability:

-   Correctness:

-   Production Efficiency:

-   Continuous Improvement: \*

-   Single Developer

Software technology evolves permanently. There are big evolutionary steps like procedural, object oriented, functional or aspect oriented programming. Further there are smaller developments or trends a professional developer has to deal with. E. g. techniques like Dependency Injection or Object Relational Mappers. Even within these techniques are evolutions as Domain Specific Languages (DSLs) for configuration vs. XML based configuration. Besides technical aspects of software development also the process continuously evolves. So various agile processes where introduced after the insight established that the waterfall model does not work. A clean code developer has to have an eye on all of this.

Proposal is to read at least 6 specialist books a year and regularly read periodicals like professional journals or blogs.

Find some recommendations here.

### Reviews

**Why?**

Four eyes will see more than two eyes. Explaining own code to a fellow developer frequently reveals details which were not considered yet.

-   Evolvability: \*\*

-   Correctness: \*\*

-   Production Efficiency:

-   Continuous Improvement: \*\*

-   Team

Usually two kinds of reviews exist: A continuous process during pair programming or a separate code review process step. In both cases the target is to have the code examined by a second developer. This prevents organizational blindness. Already the fact that a developer presents and describes his code leads to aha moments.

Nine times out of ten only a discussion with other developers reveals strengths and weaknesses of case. Exactly the process of continuous improvement involves dealing with other developers views.

Naturally reviews can be done for other things, too. They are suitable to double-check any kind of development activity as long as it results into something readable. There are informal reviews with just a second person having a look or formal reviews with dedicated roles. Common review types are Walkthrough, Technical Review, Peer Review and Inspection.

Reviews supplement automatized unit-tests and integration tests. Other than these reviews can also find mistakes in requirements. Also the can be done early in the development process and thus find mistakes early. The earlier you find a mistake the cheaper it can be resolved.

Next is [yellow grade](#grade-3-yellow).