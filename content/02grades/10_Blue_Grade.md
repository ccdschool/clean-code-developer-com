Grade 5 – Blue
==============

Principles
----------

### Design and Implementation don't overlap

**Why?**

Design papers provide more damage than benefit if they have nothing in common with the implementation. Hence minimize risks for inconsistencies.

-   **Evolvability: \*\***

-   **Correctness: \***

-   **Production Efficiency: \***

-   **Continuous Improvement: \***

-   **Team**

Implementations that do not reflect the previous planning are a problem. Reason is a violation of the DRY principle: Design and implementation are a repetition; a repetition of software structure. As implementation follows design and represents the major part of work both will quickly get out of sync, if structural changes are not included into design during implementation. Otherwise design diagrams will be worthless shortly after implementation start.

Situation improves when design and implementation are compliant to the DRY principle: They shall overlap as little as possible. In that case they are no longer a repetition but describe different things. That means: Design/Architecture doesn't care about implementation and vice versa.

Where is the cutting line? At components (see Practices below). Architects do not care about the internal structure of components. Class structures is not relevant for architecture. On the opposite a programmer merely needs to know the contracts that imported or exported by his component. A general architecture context is irrelevant to him.

Purpose of architecture is to divide software into components, define their dependencies and describe their services in contracts. Purpose of implementation is to materialize the defined components. How they do it is irrelevant for architecture.

### Implementation reflects Design

**Why?**

Implementation deviating from design as you chose leads to no longer maintainable software. Implementation needs a physical frame given by design.

-   **Evolvability: \*\***

-   **Correctness: \***

-   **Production Efficiency: **

-   **Continuous Improvement: **

-   **Single Developer**

Ideally logical structures in architecture manifest as physical as possible:

1.  Architectural structures on various abstraction levels shall be reflected as far as possible in code organization. On the one hand architecture uses physical code units as structural elements. On the other hand these structural element shall be clearly visible in the code respectively in the repository's code organization.

2.  While working on implementation of structural elements and especially within components, design changes "on the fly" shall be impossible. Working in or on a structural element is exclusive to change the surrounding structure. That give the entropy of a software does not grow out of control. That is important because the main purpose of architecture is to minimize entropy and as such the software complexity.

Planning is a must. Implementation must not torpedo planning. Even when learnings from implementation may retroact on planning. Thus planning and implementation must be decoupled. Where that is not possible, the planning should work with funds of implementation and implementation should physically reflect planning.

### You Ain't Gonna Need It (YAGNI)

**Why?**

Stuff which not used by anyone has no value. Do not spend any time on it.

-   **Evolvability: \*\***

-   **Correctness: \***

-   **Production Efficiency: \*\***

-   **Continuous Improvement: \***

-   **Single Developer**

The YAGNI (*You Ain't Gonna Need It*) principle belongs to the simplest principles in software development. However after the DRY principle it is likely most frequently violated one. That's why YAGNI is not only in [red grade](#grade-1-red) but also here close to end of the track though the [value system](#values).

The YAGNI principle is owed to the special relation between exactness of requirements and the product's materiality. Requirements are habitually imprecise and the product is immaterial. Compared to building machines or houses the material is infinitely flexible and can adopted to basically any requirement with relatively little effort. High volatility and inaccuracy meets high flexibility. That seems to be ideal.

Nevertheless experience shows that the failure of many projects lies in this relation. On short term projects seem to do the right thing by trying the obvious:

-   Software is implemented in a wide and flexible way so that vague or yet unknown requirements are already fulfilled in a kind of early adoption.

-   Permanently changing requirements are quickly introduced in the product.

On long term such an approach however is counterproductive:

-   Early adoption results in width and flexibility which is not really needed. Features are realized which will never be used.

-   Quick restructuring due to changing requirements lead to quality erosion in the code. Though software is immaterial, not every software structure is evolvable and understandable.

Applying YAGNI principle means to implement exclusively what has an immediate benefit without any doubt. Everything can be done later. With that YAGNI goes hand in hand with the [Lean Software Development](http://en.wikipedia.org/wiki/Lean_software_development#Decide_as_late_as_possible) rule "decide as late as possible".

The YAGNI principle is valid on all levels of software development. Whenever you ask yourself if an effort is really worthwhile or something is really needed, it is a case for YAGNI. In doubt decide against the effort.

Customers pay only for direct benefit. If a project attempts to foresee the customers will, it will risk to be disproved by reality the other day. For software development that means:

-   Implement only clear requirements

-   Have the customer prioritize the clear requirements

-   Implement the clear requirements in order of prioritization.

Practices
---------

### Continuous Delivery

**Why?**

Make sure the product becomes installed correctly.

-   **Evolvability: **

-   **Correctness: \***

-   **Production Efficiency: \*\***

-   **Continuous Improvement: \***

-   **Team**

Continuous Integration process from green grade ensures that both build and test errors are detected quickly. Even so we won't reach the goal to have working software installed at the customer, if created software setup itself has errors.

Accordingly setup and deployment need also be automatized to garantee we produce installable software. Automatization ensures that there are no manual steps to do which could be forgotten. So all team members can anytime generate and install the current state of the product.

### Iterative Development

**Why?**

As customer requirements can change software development would be wise to be able to adopt its course.

-   **Evolvability: \*\***

-   **Correctness: \***

-   **Production Efficiency: \***

-   **Continuous Improvement: \***

-   **Team**

Naturally software development goes from planning over implementation to a test by the customer. But it would be utopic to think a project could do with only one of each. Every phase provides input for the preceding phase. At least customer test generates input for planning and implementation.

Projects will only benefit from such input if the proceeding is not linear. If there is no way back from a later phase to an earlier phase, feedback will be useless.

The development process needs to have loops to consider feedback. At least a loop from test to planning. So software development can work iterative in multiple loops over the customers' requirement catalogue. In each iteration the project team learns more about the customers' requirements.

Additionally the team shall also learn about themselves. For that there should be "stops" where the team can reflect their proceeding. The learnings are then considered in the next iteration.

Every iteration has to have an end. To know when you are done, you will have to define what you want to achieve in the iteration (see also [What is done?](http://www.hanselminutes.com/119/what-is-done-a-conversation-with-scrum-co-creator-ken-schwaber)).

### Component Orientation

**Why?**

Software needs black-box-building-blocks which can be developed and tested in parallel.

-   **Evolvability: \*\***

-   **Correctness: \***

-   **Production Efficiency: \***

-   **Continuous Improvement: **

-   **Team**

Up to know the principles of [CCD values](#values) dealt with smaller code sections. Component Orientation is about larger software structures. There are two common definitions of the term "components":

-   Components are binary function units

-   Components service are described in a separate (!) contract.

Components are matter of planning and implementation. To emphasize that, components are developed physically independent, e. g. in separate Visual Studio solutions. This promotes both focus on one task and consequent use of mockups in unit tests. Additionally this code organization improves productivity as components can be development in parallel due to their separate contracts. Finally the physical isolation works against increasing entropy in code. If references between components can be done exclusively via contracts, the coupling will be loosely and controlled.

So Component Orientation does not only include binary code units with separate contracts but also developing contracts before implementation (*Contract-First Design*). Once a contracts for import and export are define, work on a component can be started independently.

### Test First

**Why?**

Customer is king and defines the shape of a service. Service implementations will fit only well, if these are driven by a client.

-   **Evolvability: \*\***

-   **Correctness: \***

-   **Production Efficiency: \***

-   **Continuous Improvement: \***

-   **Single Developer**

Test First bases on the idea that functional units (methods, classes, etc.) are characterized by client-service-relations. These relation are about the interface between client and service. And this interface should be defined by the client. As the service "serves" the client, it shall fit for him.

Hence definitions of code unit interfaces are done outside in. The user, as the ultimate client, is outside at the user interface. He defines the visual / haptic interface of UI code units. These again are clients of the layers below and so on. As such the services and interfaces of the lowest code units can only be defined after the layers above.

This contradicts the frequent bottom-up approach, where a data access layer is defined and implemented first. Though beginning with fundamental functionality seems to make sense, the bottom-up approach is questionable:

-   Business value is provided very late to the customer.

-   You specify without exact requirements of the ultimate client (the user) and you risk awkward or plainly used functionality (a violation of the YAGNI principle).

-   You risk close coupling as lower layers are required to implement layers are above, which makes Inversion of Control and isolated unit-tests with mockups unlikely.

CCD avoid these problems with Contract-first (see [Component Orientation](#component-orientation)) and coding outside in. With automatized tests it become fairly easy to define interfaces in the form of tests.

Test first adds semantic to syntactic contracts (e. g. interfaces). Lacking other formal ways to specify semantic, tests are the only way to formalize requirements. To assign a component to a developer for implementation it would be wise to do well to specify both the API syntax and the expected behavior in form of tests. This as many advantages:

-   The form of an interface is directly driven by a client and as such fully relevant. YAGNI doesn't have any chance.

-   Tests additionally become specification documentation. Both consumers and implementers can study it. Further documentation is largely unnecessary. This complies with the DRY principle.

-   Specifications become executable code rather than passive texts. Once implementation exists, you can check it against the test code. Thus specification and test are no longer time-consuming sequential phases. This increases productivity. This way quality assurance is done before implementation.

Next is [white grade](#grade-6-white).