Grade 3 – Yellow
================

Principles
----------

### Interface Segregation Principle (ISP)

**Why?**

A service description that is independent from concrete implementation generates liberties.

-   Evolvability: \*\*

-   Correctness: \*

-   Production Efficiency:

-   Continuous Improvement:

-   Single Developer

Interface Segregation Principle ([ISP](https://en.wikipedia.org/wiki/Interface_segregation_principle)) is another of the [SOLID](#solid) principles. It states that a client shall not depend on service details which the client does not use. The leaner the service interface is the smaller is the coupling of both components.

Imagine to design a plug that connects a monitor to a computer. You decide to provide simply each and every signal available on a computer via that plug. That plug will then have some hundred pins but be maximal flexible. Unfortunately coupling will also be maximal.

With the plug sample it is obvious that a monitor connection needs to receive only signals required for displaying an image on the monitor. Same so with software interfaces. Similarly they shall be as lean as possible to avoid unnecessary coupling. Exactly as a monitor plug an interface should have high cohesion: It shall only things that belong closely together.

You may use [Extract Interface](http://refactoring.com/catalog/extractInterface.html) and [Extract Superclass](http://refactoring.com/catalog/extractSuperclass.html) refactoring to apply the Interface Segregation Principle.

**Source**

ObjectMentor; author: Robert C. Martin; Article regarding Interface Segregation Principle; published 1996 in *The C++ Report*, Engineering Notebook

### Dependency Inversion Principle (DIP)

**Why?**

Class isolation is a prerequisite for testing to the point. Isolation is when classes receive no more implementation dependencies – neither at compile time nor at runtime. Concrete dependencies shall be decided on as late as possible. Ideally at runtime.

-   Evolvability: \*\*

-   Correctness: \*\*

-   Production Efficiency: \*

-   Continuous Improvement:

-   Single Developer

Also Dependency Inversion Principle is a [SOLID](#solid) principle. It says:

-   High-level classes must not depend on low-level classes but both from interfaces.

-   Interfaces must not depend on details but details on interfaces.

If a high-level class uses a low-level class directly, there will be a strong coupling between both of them. You will hit problems latest when trying to do an isolated test of the high-level class. Therefore the high-level class shall depend on an interface which again is implemented by the low-level class. That way the low-level class can be mocked in a unit test.

Basically there are three options to resolve an inverted, abstract dependency at runtime:

-   Constructor parameter

-   Inversion of Control Container (IoC Container), e. g. Castle Windsor

-   Dependency Lookup

In yellow grade dependencies are injected using constructor parameters. That is a simple solutions which works nicely with a small set of classes. Later on in [green grade](#grade-4-green) an IoC Container and Dependency Lookup will be used.

**Source**

ObjectMentor; author: Robert C. Martin; Article regarding Dependency Inversion Principle; published 1996 in *The C++ Report*, Engineering Notebook

### Liskov Substitution Principle

**Why?**

Avoid surprises with the heirs if you are familiar with the testator.

-   Evolvability: \*

-   Correctness: \*

-   Production Efficiency:

-   Continuous Improvement:

-   Single Developer

Also the Liskov Substitution Principle ([LSP](https://en.wikipedia.org/wiki/Liskov_substitution_principle)) is a [SOLID](#solid) principle. It claims that subtypes have to behave like their base type. Sounds trivial. Looking at exceptions highlights the problems occurring when violating LSP: If a base type method doesn't throw an exception the subtypes have to stick to that rule. If a subtype method raises an exception nonetheless, clients using the base type will get into trouble because they won't be prepared for it. If the base type doesn't raise an exception clients will not expect they have to handle one.

Generally speaking the principle states that a subtype may only extend base type functionality but must not reduce it. A subtype can keep or extend a value range defined in a base type but never limit it.

The Liskov Substitution Principle implies the recommendation to think thoroughly about inheritance. In most cases composition is to be preferred over inheritance ([Favor Composition over Inheritance](#favor-composition-over-inheritance-fcoi)). Do consider behavior with inheritance, not only structure. Accept inheritance as a *behaves-as* relation that considers behavior rather than a *is-a* relation that reflects only the (data-)structure.

**Source**

ObjectMentor; author: Robert C. Martin; Article regarding Liskov Substitution Principle; published 1996 in *The C++ Report*, Engineering Notebook

### Principle of Least Astonishment

**Why?**

If a component behaves surprisingly different than expected, your application will become unnecessarily complex and error prone.

-   Evolvability: \*\*

-   Correctness: \*

-   Production Efficiency: 

-   Continuous Improvement:

-   Single Developer

To a high degree software development is a creative process. In that process it is important to be in the flow. In that state code easily splutters. Any flow disturbance is an interruption that results in less code being produced in the available time and code quality dropping. After each interruption the developer needs gathering speed to get into the flow again. Surprises are disturbances. They result in interruptions and mistakes. Sample: If keyboard shortcuts in the development environment the common short Ctrl-C has completely different meaning, this will disturb the developer. Using the "wrong" shortcut will annoy him or her again and again. This prevents creative work.

Software implementation should avoid surprises. If a method named `GetValue()` does not only return a value but also changes the systems state, a developer ideally would disregard that method to avoid naughty surprises. In worst case he won't be aware of that suspicious behavior. (Query methods which change the state defy the *Command Query Separation* principle). Test-driven development fosters least astonishing interfaces as interfaces are designed and implemented from the clients view.

### Information Hiding Principle

**Why?**

Hiding details in an interface reduces dependencies.

-   Evolvability: \*\*

-   Correctness: \*

-   Production Efficiency:

-   Continuous Improvement:

-   Single Developer

Interface design should consider which details need to be visible to the outside world. "Interface" not only in its object oriented meaning but also implicit interfaces. Every class necessarily has an implicit interface – it contains all externally visible details. The more details are visible externally the higher is the coupling between class and its clients. Once used by a client it will be harder to adopt that detail of a class. This obstructs evolvability of software.

Practices
---------

### Automatized Unit Tests

**Why?**

Only automatized tests are really executed in a consequent manner. The more accurate unit test verify code the better.

-   Evolvability: \*\*

-   Correctness: \*\*

-   Production Efficiency: \*\*

-   Continuous Improvement:

-   Single Developer

[Orange grade](#grade-2-orange) introduced integration tests. Now it is about unit tests. Other than an integration test a unit test verifies an isolated functional unit (particularly classes but also methods or components). This requires to unchain the function unit from its dependencies. If unit tests are written for existing code in the aftermath, refactorings will be necessary pretty often. Integration tests ensure that no errors are introduced with that.

Automatized tests generate two benefits:

-   They save time.

-   They take fear.

The more a code is under change the larger is the time saving benefit. When code is changed you will need to test new and old functionality (regression tests) again and again. Automatization simply saves time with that. And the more complex code is the larger is the benefit of taking fear. If complex code is enhanced, optimized or plainly fixed, there will be a high risk to introduce mistakes unnoticed. Automatized tests in small steps will reveal that, so that fear of disimprovement gets superfluous.

### Mockups

**Why?**

Mockups make controllable tests possible.

-   Evolvability: \*

-   Correctness:

-   Production Efficiency: \*\*

-   Continuous Improvement:

-   Single Developer

Normally components use other components. If you want an isolated component test, these dependencies have to be removed as you are only interested in that one component (*System Under Test or SUT*) and how the component interacts with others.

To isolate we use mockups. These are used in place of real components. So the System Under Test interacts with well controlled mockups instead of real components.

Literature mentions further terms like *Stub*, *Dummy* or *Fake* which sometimes used as a synonym but actually stand for [different functionalities](http://martinfowler.com/articles/mocksArentStubs.html). Implement a mockup manually before you use a mock framework like [Rhino Mocks](https://hibernatingrhinos.com/oss/rhino-mocks). This helps to understand the mechanics.

### Code Coverage Analysis

**Why?**

Only believe in tests you know they really cover the test area.

-   Evolvability:

-   Correctness: \*

-   Production Efficiency: \*

-   Continuous Improvement: \*

-   Single Developer

Unit tests ideally cover all paths through our code. Only then we gain confidence that the code works correct. *Code Coverage Analysis* is used to learn which code areas are not yet covered by tests. It reveals code that is not yet executed by automatized tests.

Having 100% code coverage does not mean by default that enough tests exist. But less than 100% indicate that there a niches you cannot say anything about correctness. 100% code coverage should always be aimed for.

In real live 100% code coverage not always can be achieved with reasonable effort. As in other parts of life the final 2, 3 or 4 percent cause disproportional trouble. Hence also less than 100% can be acceptable after a thorough analysis of the coverage situation.

Coverage below 90% though is too full of holes to be considered professional. Thus starting with automatized tests shall be accompanied by Code Coverage Analysis. Otherwise you cannot rate test quality.

For measuring code coverage there are two simple metrics called C0 and C:

C0 = Number of tested methods / Number of methods

C1 = Number of tested decisions or branches / Number of decisions or branches

C1 is the stronger metric because 100% branch coverage implies 100% method coverage. That does not hold true the other way round.

### Attend professional events

**Why?**

Best way to learn is from others and in company.

-   Evolvability:

-   Correctness:

-   Production Efficiency:

-   Continuous Improvement: \*

-   Single Developer

Discussing regularly to other software developers and exchanging experiences prevents stewing in one's own juice. To get new views that exchange should happen with developers outside of the team, apart from daily routine, e. g. in user groups.

In regional user groups exchange or experiences is in the fore. That is important. The longer you are in a group the better you get to know your discussion partners and the more opinions equalize also in a user group. Hence it is important to think out of the box every now and then. National developer conferences provide new brain feed and allow discussions with completely different developers.

A CCD should keep an eye on three levels for exchange and inspiration: The own developer team, a regional user group and national or international conferences. Every level has its own rhythm: daily, monthly, yearly.

### Complex Refactorings

**Why?**

It is not possible to write code in an ultimate form.

-   Evolvability: \*\*

-   Correctness:

-   Production Efficiency:

-   Continuous Improvement: \*

-   Single Developer

Simple refactorings were introduced in [red grade](#grade-1-red). However *Rename* and *Extract Method* may not be enough to improve code – many times bigger interventions are necessary. Dividing simple from complex refactorings make sense because complex refactorings will only be efficient and riskless with automatized tests at hand. Without tests you wouldn't know if the code is still correct.

Next is [green grade](#grade-4-green).