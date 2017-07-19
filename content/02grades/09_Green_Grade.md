Grade 4 – Green
===============

Principles
----------

### Open Closed Principle

**Why?**

Keep the risk as low as possible to destabilize a system by adding new features.

-   Evolvability: \*\*

-   Correctness: \*

-   Production Efficiency: \*

-   Continuous Improvement:

-   Single Developer

*Open Closed Principle* ([OCP](http://www.objectmentor.com/resources/articles/ocp.pdf)) claims to keep a class open for enhancements but closed against modifications. It is another of the [SOLID](#solid) principles. A code sample shall highlight the problem:
```
public double Price() {
	const decimal regularDiscount = 0.95m;
	switch(customerType) {
	case CustomerType.FirstTime:
		return quantity * pricePerUnit;
	case CustomerType.Regular:
		return quantity * pricePerUnit * regularDiscount;
	default:
		throw new ArgumentOutOfRangeException();
	}
}
```
If another price calculation is introduced, you will have to modify that class. Risk is that the modification can introduce mistakes which break the already existing functionality. The risk to introduce new bugs exists even with automatized unit tests and integration tests in place because 100% test coverage is rare. So it needs a technique which allows to enhance the class without modifying it. One option to achieve this is the *Strategy Pattern*:
```
private IPriceCalculator PriceCalculator;
public double Price() {
	return PriceCalculator.Price(quantity, pricePerUnit);
}

public interface IPriceCalculator {
	double Price(int quantity, double pricePerUnit);
}
public class FirstTime : IPriceCalculator {
	public double Price(int quantity, double pricePerUnit) {
		return quantity \* pricePerUnit;
	}
}
public class Regular : IPriceCalculator {
	const decimal regularDiscount = 0.95m;
	public double Price(int quantity, double pricePerUnit) {
		return quantity \* pricePerUnit \* regularDiscount;
	}
}
```
Concrete price calculation is extracted to separate classes which implement a common interface. Thereby is feasible to add a new implementations of that interface any time. Thus the class will be open for enhancements but at the same time closed against modifications. You may apply the [Replace Conditional with Strategy](http://www.industriallogic.com/xp/refactoring/conditionalWithStrategy.html) refactoring to make existing code compliant to Open Closed Principle.

**Source**

ObjectMentor; author: Robert C. Martin; Article regarding Open Closed Principle; published 1996 in *The C++ Report*, Engineering Notebook

### Tell, Don't Ask

**Why?**

High cohesion and loose coupling are virtues. Public state details in a class contradict those.

-   Evolvability: \*\*

-   Correctness:

-   Production Efficiency:

-   Continuous Improvement:

-   Single Developer

Speaking radically a class should not have property getters. These mislead clients to do decisions based on values provided by an object. So rather than telling the object what to do, it is asked for a value to guess from outside on the inner state of the object.

A core principle of Object Oriented Programming is Information Hiding (see also in [yellow grade](#grade-3-yellow)). No class shall publish details which give indication on how the class is implemented internally. If a class requires an internal state, the value will be typically stored in a private field. This value being visible to the outside will mislead clients to adduce the mainly internal object state for own decisions. With that a class is quickly reduced for data storage only. Telling an object what to do is preferable in any case. Thereby the clients does not need to know how the class accomplishes the task internally.

Compliance to the [Tell don't ask](http://www.pragprog.com/articles/tell-dont-ask) principle results in objects with behavior instead of "stupid" data storage objects. Object interaction becomes loosely coupled as the object don't need to do assumptions on their collaborating objects. Even more! If objects don't publish their states, the will keep the power of decision. Cohesion of the code in question grows because it is consolidated into one place.

### Law of Demeter

**Why?**

Object dependencies over multiple service chain elements lead to unpleasantly close coupling.

-   Evolvability: \*\*

-   Correctness: \*

-   Production Efficiency:

-   Continuous Improvement:

-   Single Developer

The [Law of Demeter](https://en.wikipedia.org/wiki/Law_of_Demeter) is about limiting the interplay of objects to a healthy extent. Simplified it means "Don't talk to strangers". Following the Law of Demeter a method exclusively uses other methods

-   within the class

-   of parameters

-   of associated classes

-   of self-instantiated objects

Though: From time to time pure data storage objects do make sense and the Law of Demeter does not need to be applied. E. g. configuration data may nicely be distributed hierarchically over multiple classes so that a value access would finally be as follows:

int margin = config.Pages.Margins.Left;

Applying the Law of Demeter would only allow access to config.Pages.

Practices
---------

### Continuous Integration

**Why?**

Automatization of centralization of software production increase productivity and reduce risk

-   Evolvability: \*

-   Correctness: \*

-   Production Efficiency: \*\*

-   Continuous Improvement: \*

-   Team

Often integration of software components is postponed and done costly and error prone by hand. Actually software should be fully loadable at any time. Continuous Integration means a process that takes care to compile and test the code after transmission of changes.

This is especially important for teams as the whole code base is used, not merely the part one developer currently worked on. Automatized tests should be executed by every developer before transmitting changes to version control. This is not affected by Continuous Integration. To ensure the tests were executed indeed and mistakes get detected early, tests run on the Continuous Integration Server in any case. It doesn't release the developer from running tests before the Commit. Finally faulty code in version control obstructs the whole team, maybe even further teams. So the Continuous Integration Process ensures across teams that errors are detected as soon as possible.

Multiple [tools](#_Tools) are available for the Continuous Integration process. Besides build and test also long running processes like database tests can be automatized. These may be only executed at night for an instance. [Green grade](#grade-4-green) regards only both build and test process. Continuous setup and deployment follows later in [blue grade](#grade-5-blue).

Martin Fowler wrote an excellent [article](http://www.martinfowler.com/articles/continuousIntegration.html) on this topic.

### Static Code Analysis (Metrics)

**Why?**

Trust, but verify.

-   Evolvability: \*

-   Correctness: \*

-   Production Efficiency: \*

-   Continuous Improvement: \*

-   Single Developer

How is the quality definition for code unit like a class or a component? Is it sufficient to fulfil the customers' functional requirements? Is it sufficient to be fast enough and scalable? Automatized tests and finally customer tests will tell. Without compliance to requirements naturally software has no relevant quality. If it is not use for the customer, you can spare further questions.

However, contrary to wide-spread belief it is not sufficient to be just compliant to requirements. High quality does not merely result from functionality and let's say performance. Besides functional and non-functional requirements there is another usually unspoken requirement: Customers always want software fulfil their requirements today, but also tomorrow and the day after. Customers want investment protection through evolvability.

For customers this requirement pertains implicitly. They think it come naturally that an immaterial product like software can be eternally adopted to new requirements by pressing a button. Also managers often believe in this. And even software developers themselves.

The misunderstanding could hardly be bigger. Evolvability neither is self-evident in the sense the target that a software developer strives for, nor comes it naturally out of thin air. Evolvability on the contrary is hard work and steadily needs balancing against other values.

Other compliances can be determined by (automatized) tests – so what about evolvability? Can code quality be measured in an automatized way regarding vitality and survivability? Partially yes. Not all aspects can be verified by a machine. For instance it won't recognize if software is being kept open for enhancements via an add-in concept.

Nevertheless there are measurable [metrics](http://en.wikipedia.org/wiki/Software_metric) for software. There is support by [tool](#_Tools)s which should be used in any software project.

-   Fore legacy code, tools can retrieve the status quo and define a baseline to compare the future code development.

-   For new code, developed considering evolvability, static code analysis will show if planned goal was achieved

Clean Code Developer are not satisfied with having code tested automatically. They always will keep an eye on its evolvability because they know that customers expect it – indifferent if they explicitly said it or not.

### Inversion of Control Container

**Why?**

It is easier to configure things which are not hard-wired.

-   Evolvability: \*

-   Correctness:

-   Production Efficiency: \*\*

-   Continuous Improvement:

-   Single Developer

In [yellow grade](#grade-3-yellow) the CCD got to know Dependency Inversion Principle. While there the dependencies were resolved "by hand", the next step will now be to automatize that. Two techniques are available for this:

-   Locator

-   Container

Both use a so-called *Inversion of Control Container* (IoC Container). Initially the classed used need to be deposited in the container. Then the container can provide instances of the deposited classes. With a *Locator* this happens explicitly. Advantage is that dependencies do not need to be listed in the class' constructor. With crosscutting aspects like *Logging* this is the usual approach. Though normally the dependencies will be provided as constructor parameters. Advantage is that all dependencies are visible. The container can implicitly resolve the dependencies by recursively instancing all required objects via the container.

IoC container become important when the number of classes is growing. If you consider *Separation of Concerns*, many small classes with reasonable sizes with be created. Combining instances of these classes will be more effort accordingly. This is where an IoC Container comes into play – it helps with instantiating and combining multiple small objects.

Further benefit of IoC containers is that they can define the *lifecycle* of an object via configuration. If there shall be only one unique instance of an object (*Singleton*), you will simply advice the container to always return the same object. Also other lifecycles like *one instance per session* are supported.

To avoid dependency on a specific IoC container you may use *Microsoft Common Service Locator* (see [Tools](#_Tools)). It provides a unified interface to common IoC containers.

It is helpful to implement the functionality of an IoC container yourself to understand mechanics beyond. Don't build a fully-fledged container but just the basic functions.

### Share Experience

**Why?**

Sharing your experience helps others and yourself.

-   **Evolvability: **

-   **Correctness: **

-   **Production Efficiency: **

-   **Continuous Improvement: \*\***

-   **Single Developer**

Professional work requires up-to-date knowledge. It doesn't mean that anyone would know everything about software development even only on the .NET platform. Up-to-date knowledge concerns you specialist fields – whichever those might be. Thus other grades contain practices for gathering information over various channels regularly.

However collecting information is only the first of two steps. The second step is providing information; knowledge transfer. Professionalism includes research and teaching. Only with teaching a subject it will be fully conceived.

This becomes clear when you try to explain an (assumedly) learned topic to someone else. Quickly questions occur which you never asked yourself. Other people will often have a totally different perspective.

So you should expose yourself to teaching, passing on information, knowledge transfer. Presenting your learning in your own words in front of an audience will tell you how deep your knowledge really is. Question marks over your "pupils" heads may indicate that something is still wrong.

A real audience is optimal. This can be a meeting with colleagues or a user group event. You will get direct feedback there. Alternatively or additionally written knowledge transfer are suitable, too. A blog is drafted in 5 minutes and professional magazine are permanently looking for new authors. Feedback is not that direct but still putting your stuff into textual form is a good exercise.

### Error Measurement

**Why?**

You will only be able to reduce the error rate, if you first-hand know how many errors occur and adopt your approach accordingly.

-   **Evolvability: \***

-   **Correctness: \***

-   **Production Efficiency: \***

-   **Continuous Improvement: \*\***

-   **Team**

Mistakes happen. In all phases of software development: Misunderstood or unclear requirements same as buggy implementations. Finally everything is a mistake which results in a software that does not fulfills the customers' requirements. An iterative approach and reflection are two building blocks which help to improve the process. For knowing if improvement happens, you will have to have a measured variable to compare.

Error measurement can be counting or taking time. Precision is not in the fore as long as the measuring method returns comparable data. A trend of multiple iterations shall become apparent. In the end it doesn't matter who caused the error as long as the team learns and improves its process.

Do not measure errors occurring during development. These are unavoidable and hopefully result in an errorless product at the end of an iteration. It is about errors reported after an iteration from the customer, product owner or support. Those errors interfere implementation of new requirements.

Next is [blue grade](#grade-5-blue).