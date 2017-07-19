Values
======

Clean Code Developers apply to four values described below:

-   Evolvability

-   Correctness

-   Productive Efficiency

-   Continuous Improvement

Evolvability
------------

Let's start this chapter with a provocative thesis:

**Something like software maintenance does not exist!**

Maintenance is a proactive process. In production plans parts are replace on a regular basis before breaking. These are replaced because experience shows that reliability would fall under critical threshold. Hence critical parts are renewed before the whole machinery grounds to a halt. Car owners know that motor oil has to be replaced regularly. Not that oil would be empty or no longer working. It's replace because manufacturer's experience shows a motor will last longer that way.

Nothing of that applies to software. Software is as it is. Most times it contains mistakes. Also these mistakes are as they are. You cannot do anything proactively to improve the software state.

Clearly there are proactive tasks at software operation as ensuring free disk space for log files or double-checking if a database reaches maximum capacity. But software itself cannot be maintained proactively. Any change will have the intention to remove a mistake or implement a new or adopted requirement.

To enable changes software needs structure that embraces changes. This we call Evolvability. Normally software will be operated long periods. During these periods parameters change and features are added. Ideally cost of feature implementation will be independent from the point in time when the feature is introduced.

However in real world the price of a feature raises the later it is introduced. Early features enhancements are reasonably priced and in the end it's no longer possible at all to add features as nobody sees through anymore. That kind of software will be junked and re-developed. Until finally reaching this point costs raise exponentially. There are two evil aspects on exponential growth: 1) initially the moderate increase of costs is almost not sensible. 2) Once you notice cost increase it's too late and taking countermeasures typically fails.

The simpler software can be adopted the higher its evolvability is. Unfortunately evolvability you won't get subsequently. It has to be considered from the start. Software must be constructed like that. An example:

A class should have exactly one responsibility. Being in charge of more than one thing complicates keeping overview. This obstructs change which requires understanding the source code under change. Also class coupling increases. Suddenly everything is connected to everything else. Only clear responsibilities and keeping an eye on coupling can avoid this. Adding new features becomes difficult with a set of highly coupled classes where you have trouble to find single function units. Situation becomes worse if nobody dares to untangle the thicket in time. From a certain point it is hardly possible to add features – ultimate MCA in software development.

Considering evolvability from the start you can steadily enhance and adopt software products over long periods. Cost may increase slightly. But never exponentially.

Correctness
-----------

Software must work correctly. An accounting system has to process bookings properly and a spreadsheet needs to calculate accurately. Also non-functional requirements have to be fulfilled. The application shall save resources (memory, CPU-time, disk space, etc.) and response times shall be within a threshold. Only with all requirements fulfilled a software can be called correct.

Nobody will doubt that correctness is required. But what exactly do we do to grant it? It is not sufficient to pass software though a test department to detect errors. Correctness must be considered during development. Developers have to face up to correctness. And to be able they need to understand the requirements. This is frequently not the case. Developers are asked to implement features without precisely knowing acceptance criteria. This is not seeking culprits outside the development department – the developer's duty is to ask when confronted with unclear requirement rather that peeping into a crystal ball.

Compared to car construction software development is in a bad position regarding correctness. A car consists of many parts. Their correctness can be verified and proved separately. Consider you would have to do error analysis by sitting on the hood of a car with a measuring tool to review what happens within the engine. At 80mph on the highway. Sounds strange? Debuggers are used frequently exactly like this. Probably not a good idea.

Production Efficiency
---------------------

Naturally finally development time and the software's price are important. And that is higher if the production is not done efficiently. This may be everything from manual, non-automatized tasks work steps to high error rates which require repetitive repairs. Ultimately production efficiency means that software can be further developed over years or even decades instead of having to start over again. At the same time high production efficiency reduces the susceptibility to errors.

Furthermore production efficiency as a value is essential to moderately counterbalance the other values. Accordingly spending infinite effort even on correctness is no good idea.

Continuous Improvement
----------------------

Improvement requires reflection. By reflecting you recap if solving a certain task was easy or cumbersome. These insights base on reflection.

It is important for informatics as a young science to consider new insights. This needs reflection on all levels. Starting with reflection on implementation at pair programming or code review, daily team reflection, reflection after each iteration to self-reflection of our line of business.

Principles and Practices
------------------------

The values lead the CCD at his daily business. They are no solutions but instead build a general set-up for solutions. In addition we put together building blocks, each transporting at least one of the values. These building blocks are divided in two categories: Principles and practices.

**Principles**

CCD principles are fundamental software structuring approaches. They are either orthogonal to other parameters or build upon them. Code should be in line with as many principles as possible. Naturally principles are no scientific laws which cannot be ignored. However regarding software development they match their fundamentality. While ignoring a principle doesn't have an immediate negative effect, over time it will lead to pain. This pain may be difficulties to understand code, high effort to introduce changes or ultimately a no longer evolvable software. You will always see in code, if a principle is considered.

**Practices**

Practices are permanently used techniques and methods. They describe what a Clear Code Developers practically do. The practices mantra is "Do it like this. Every day. Always.". They are down-to-earth instructions which sometimes require tool support. You won't necessarily see in code, if a practice was applied.