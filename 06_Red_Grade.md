Grade 1 – Red
=============

Principles
----------

### Don't Repeat Yourself (DRY)

**Why?**

Every duplication of both code and manual tasks fosters inconsistencies and mistakes.

-   Evolvability: \*\*

-   Correctness: \*\*

-   Production Efficiency: \*

-   Continuous Improvement: \*

-   Single Developer

DRY "*Don't Repeat Yourself*" is valid since the very begin of software development – otherwise there wouldn't be subroutines or data normalization. Even though it is the most frequently disregarded principle. It is too simple to repeat code using copy & paste. Especially when it is meant to go quick this happens far too often.

Clean code developer practice in the red grade to regard this principle. They become aware when they repeat code or other artifacts. They recognize repetitions created by themselves or others. They clean-up repetitions by refactoring – as long as no other principles or limitations contradict.

### Keep It Simple, Stupid (KISS)

**Why?**

Doing more than the obvious keeps customers waiting and complicates solutions unnecessarily.

-   Evolvability: \*\*

-   Correctness: \*\*

-   Production Efficiency: \*

-   Continuous Improvement:

-   Single Developer

To quote Albert Einstein: "Everything should be done as simple as possible, but not simpler". Prerequisite for evolvability of code is that code is comprehensible. Always prefer a simple, clear and easy to understand solution. It should ring an alarm if you won't understand you own code after a short period of time. Even more important is that other developers can understand the code quickly. Pair Programming and regular reviews support this. These provide also control if the simplest solution was indeed used.

Technical details drive temptation to head for a complex solution. If the well-known and obvious appears too boring, a complex solution might sneak in. Provided the simple solution works, it shall be favored. Same so for data structures. If IEnumerable will be sufficient, ICollection or even IList shall not be used.

### Beware of Optimizations!

**Why?**

Optimizations cost effort. Being aware of that often saves precious capacity for stuff the customer really benefits from.

-   Evolvability: \*\*

-   Correctness:

-   Production Efficiency: \*

-   Continuous Improvement:

-   Single Developer

**M.A. Jackson**

Rules of Optimization:

-   Rule 1: Don't do it.

-   Rule 2 (for experts only). Don't do it yet.

W.A. Wulf:

More computing sins are committed in the name of efficiency (without necessarily achieving it) than for any other single reason – including blind stupidity.

Understandability of code hast always priority. Optimized code pretty often is all but well readable. By reducing the absolutely required into the shortest possible form it may fulfill the customer's functional and non-functional requirements. But it mostly won't reflect them in an understandable way. This is counterproductive regarding software durability which is usually expected. Donald Knuth wrote in 1974: „*We should forget about small efficiencies, say about 97% of the time: premature optimization is the root of all evil.*“ (Knuth, Donald. [Structured Programming with go to Statements](http://web.archive.org/web/20130803163743/http:/pplab.snu.ac.kr/courses/adv_pl05/papers/p261-knuth.pdf), ACM Journal Computing Surveys, Vol 6, No. 4, Dec. 1974. p.268.)

Pathfinder rule does not mean to strive for code optimizations. It actually intends the opposite: Understandability and evolvability.

So a clean code developer should think at least twice before he starts to screw out another trickle of performance. For one thing he will decrease understandability, for another thing the optimization might be unnecessary for various reasons. If the performance leak is general issue, the next larger refactoring will probably take care of it as then is a global structural issue. Or the upcoming hardware generation smooths away the problem. Or the customer doesn't mind at all. Anyway the customer must have asked for optimization. No code change without a benefit expected by the customer – only for that he is willing to pay.

There is an even more fundamental rule beyond the decision against optimizations in cases of doubt: YAGNI – *You ain't gonna need it*. To its full extend that is part only of the blue grade.

If against any warnings and doubts a performance optimization was unavoidable, this should be started exclusively based on a detailed profiler analysis. Only if you identified the bottlenecks that way, you will be able to see if you resolved them during and after the optimization.

### Favor Composition over Inheritance (FCoI)

**Why?**

Composition promotes loose coupling and more flexible testability of a system.

-   Evolvability: \*\*

-   Correctness:

-   Production Efficiency:

-   Continuous Improvement:

-   Single Developer

There are two well-known candidates for functional reuse in object oriented programming (OOP): Inheritance (whitebox reuse) and composition (blackbox reuse). Reusing functionality by deriving from a class will make the subclass dependent from the parent class. In many cases a system becomes unnecessary complex, poorer to test and makes it difficult to switch functionality at runtime. In clean code development we consider the Liskov Substituion Principle (LSP) for correct inheritance.

With composition on class uses a different class. Doing that via a neatly defined interface promotes decoupling. Favor Composition over Inheritance asks you to prefer composition before dealing with LSP.

### Integration Operation Segregation Principle (IOSP)

**Why?**

A broad symptom of code which is hard to change are deep hierarchies of functional dependencies. The decrease understandability and hamper both automatized tests and refactoring.

-   Evolvability: \*\*\*

-   Correctness: \*\*

-   Production Efficiency:

-   Continuous Improvement:

-   Single Developer

If a method contains both logic and calls to other methods, the total behavior will be no longer clear. The instructions are blurred over a possibly very deep hierarchy. Furthermore this kind of method has a tendency to grow unlimited.

IOSP calls for a clear separation:

-   Either a method contains exclusively logic, meaning transformations, control structures or API invocations. Then it's called an *Operation*.

-   Or a method does not contain any logic but exclusively calls other methods within its code basis. Then it's called *Integration*.

That explicit separation has many positive effects:

1.  Methods tend to stay short. More than 10, 20 or 30 lines of pure logic or exclusively method calls "feel strange". As mixing is not allowed small methods will be extracted.

2.  Short logic methods are easy to test as they don't have dependencies.

3.  Short logic methods are relatively easy to understand. The methods name can drive the meaning.

4.  Short integration methods are very well understandable and reveal what happens at first glance.

5.  Correctness of integrations can be reviewed easily. Basically just the process order needs to be double-checked. Compiler and unit-tests of operations do the rest.

6.  Integrations can be nicely expanded by inserting additional method calls. Understandability stays.

Any developer willing can apply IOSP off-hand. Also IOSP compliance is trivial to verify as integration and operation differ notably in form.

Read more to IOSP in free booklet "[Messaging as a Programming Model](https://leanpub.com/messaging_as_a_programming_model)“.

Practices
---------

### Pathfinder Rule

**Why?**

A broad symptom of code which is hard to change are deep hierarchies of functional dependencies. The decrease understandability and hamper both automatized tests and refactoring.

-   Evolvability: \*\*\*

-   Correctness:

-   Production Efficiency:

-   Continuous Improvement:

-   Single Developer

Establishing the CCD values needs time. Also it is difficult to apply the principles to the whole code base as a CCD rarely starts alone on a green field project. Therefore it is more realistic and more motivating to aim for tiny but continuous progress.

Accordingly the pathfinder rule belongs to the clean code development fundamentals. It says:\
*Leave the campground cleaner than you found it.*

Concerning software development that means: Clean code developers leave code in a better state than they found it. So after work accomplished code shall apply more to CCD values than before.

What exactly to be done is specific to situation and code – and of course to the grade currently worked on. A CCD in read grade would for an instance move code into version control, if it wasn't yet in there. And he would focus on eliminating any kind of redundancies which are violations of the DRY principle.

So a CCD will steadily try to heal weaknesses in the sense of CCD values wherever he finds it. In small steps. And naturally he will try hard to avoid weaknesses upfront. As said: Always at the level of his personal development.

This maxim is essential in the evolution of a CCD bearing [broken windows theory](https://en.wikipedia.org/wiki/Broken_windows_theory) in mind. According to that decay of quality in general starts with trifles which are ignored long enough.

Following the pathfinder rule no "broken windows" will be produced – and existing ones are repaired one by one. The pathfinder rule systematically eliminates fissures and bumps based on the CCD values, so that no further deposits are formed. This practice works proactively against code erosion which is so fundamental that it is included in red grade.

### Root Cause Analysis

**Why?**

While eliminating symptoms brings quick relief, it costs more effort in the long run. You will be more efficient, if you have a look under the surface of problems.

-   Evolvability: \*

-   Correctness:

-   Production Efficiency:

-   Continuous Improvement: \*

-   Single Developer

A rule from the very first day as a CCD should be to always search for the root cause of an issue. Clean code developer do not consider themselves satisfied with healing symptoms. Example:\
Sorting data in memory is too slow. A symptom cure would strive for speed up single instructions or instruction blocks. Maybe unsafe code or parallelization becomes an option. A thorough root cause analysis would have shown that the chosen sort algorithm is the real culprit. Hard to understand low level optimizations hence can be avoided by choosing a better algorithm.

Root cause analysis serves understandability and effort reduction. This is because with knowing the root cause, clean-up tends to be less effert than curing symptoms. A CCD hitting a problem will pause to get himself a chance looking beyond the symptoms.

Root Cause Analysis is also known as "Five Why's". This term origins from the Toyota Production System (TPS) stating the basic idea to ask "Why?" five times.

### Version Control 

**Why?**

Being afraid of damaging a running system paralyzes software development. Using version control that fear is obsolete and development can progress quickly and bravely.

-   Evolvability:

-   Correctness:

-   Production Efficiency: \*\*

-   Continuous Improvement: \*

-   Team

It's a must for every CCD to protect his code using version control. If it is GIT, TFS, Subversion, Mercurial, VSS or Vault does not matter. Don't work on code without putting it under version control. Reason is simple: Version control removes fear. And absence of fear is prerequisite to bravely apply principles and practices of CCD values.

Version control eliminates fear to do something wrong and break the system. With code under version control a CCD can apply changes as desired without any fear to destroy the current state. Nothing will be lost. Version control is a time machine for code.

Hence version control is the very best basis for learning. Since learning means doing mistakes. You can do any mistakes with version control as safety net. So first requirement to step into clean code development is permanent use of version control.

If that is not possible in a project, the fundament for clean code development will not be there. Also there is no meaningful reason why use of version control should not be possible. It can go without costs and training efforts for the basic functions are minimal.

### Simple Refactoring Patterns

**Why?**

Improving code is easier if you know typical improvement patterns. Their usage scenarios sensitize for weaknesses in self-written code. As accepted patterns they encourage to be applied.

-   Evolvability: \*\*

-   Correctness:

-   Production Efficiency:

-   Continuous Improvement: \*

-   Single Developer

It requires smaller or larger interventions to leave code better than you found it. A CCD can do these without fear due to version control. But how can he do in the possibly easiest way?

Key is "Refactoring". [Martin Fowler](http://martinfowler.com/) describes [Refactoring](http://www.amazon.de/Refactoring-Studentenausgabe-vorhandener-verbessern-Programmers/dp/3827322782) as fundamental technique to increase code quality in his equally named book. In there he defines a bunch of code change patterns to eliminate "Code Smells" which is a metaphor for both suboptimal structures and general disregard of principles.

[Extract Method](http://martinfowler.com/refactoring/catalog/extractMethod.html) refactoring is the centrally relevant on in red grade to satisfy the DRY principle. Clean code developer apply this refactoring to extract redundant code into a method.

Second refactoring to be applied when appropriate is [Rename](http://martinfowler.com/refactoring/catalog/renameMethod.html). It fits the pathfinder rule as a frequent filthiness are cryptic names in code.

Refactoring can be done manually or with tool support. Modern IDEs provide some built-in refactoring patterns. Further tool are listed in our Tools list.

"Refactoring" and "Clean Code" are required reading for clean code developers in the red grade.

### Daily Reflection

**Why?**

There is no improvement, no progress, no learning without Reflection. But only if reflection is on the schedule, it will happen under daily business pressure.

-   Evolvability:

-   Correctness:

-   Production Efficiency:

-   Continuous Improvement: \*\*

-   Single Developer

Personal development is a central topic in clean code development. So it's about change: Every day the CCD values shall be integrated a tiny bit more in daily project business of the clean code developer. That is the CCD pathfinder rule applied to itself.

Walking such a way of change isn't easy, especially alone. So how shall you stay on track? How measure your progress?

Without establishing a control system it requires two things:

1.  Plan in small steps

2.  Reflection after each step

Independent from project management input a CCD shall plan his work in a way that the tasks can be finished in one day. That way you can make a balance every evening. This again is important to avoid taking work after quitting time. This is required for recreation.

To consequently evolve a clean code developer shall reflect daily if he considered the CCD values of his current grade. For red grade this would be questions as: Are all code fragments under version control? Did I apply the DRY-Principle consequently? Did I in general leave code in a better state as I found it?

Don't mind if you hesitate to answer with yes or even have to say no. How hard you may have tried - sometimes it simply won't have worked.

Still then the following is to be done:

-   Either start to amend until no violation of principles is left for the working day.

-   Or take the recognized violations on your next day's task list.

The CCD bracelet can help with reflection – of course only if you don't mind wearing a colorful silicon bracelet. Switch the bracelet to your other arm if you can't or don't want to eliminate a principle violation. So you deliberately indicate a difference between the grades requirements and your achievement. Don't misunderstand this as defeat or even penance. Intention is a haptic support of the learning process.

After not switching the bracelet arm for 21 days the CCD may move on to the next grade – the [orange grade](#grade-2-orange).