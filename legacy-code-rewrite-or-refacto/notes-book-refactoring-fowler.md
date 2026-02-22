# Refactoring, Fowler
http://martinfowler.com/books/refactoring.html

*Five or six years ago I was working on an essay about refactoring CSS. I didn't do that, but I did find these notes while working on something new. Hope they're useful!*
*—Dean*

p7
"When you find you have to add a feature to a program, and the program's code is not structured in a convenient way to add the feature, first refactor the program to make it easy to add the feature, then add the feature."

p7
"Whenever I do refactoring, the first step is always the same. I need to build a solid set of tests for that section of code." or, on p8: "Before you start refactoring, check that you have a solid suite of tests. These tests must be self-checking."

p8
"When I look at a long method [like the statement one he's using in his example], I am looking to decompose the method into smaller pieces. Smaller pieces of code tend to make things more manageable. They are easier to work with and move around."

p15
"Code that communicates its purpose is very important. I often refactor just when I'm reading some code. That way as I gain understanding about the program, I embed that understanding into the code for later so I don't forget what I learned."

p20
"The compiler should tell me whether I missed anything. I then test to see if I've broken anything."

p32
"...until I profile I cannot tell how much time is needed for the loop to calculate or whether the loop is called often enough for it to affect the overall performance of the system. Don't worry about this while refactoring. When you optimize you will have to worry about it, but you will then be in a much better position to do something about it, and you will have more options to optimize effectively."

p35
"Why do I prefer to pass the length of rental to the movie rather than the movie type to the rental? It's because the proposed changes are all about adding new types. Type information tends to be more volatile. If I change the movie type, I want the least ripple effect, so I prefer to calculate the charge within the movie."

p38
[Preference of replacing switch methods with polymorphism.]

p50
"All these changes were small steps. It seems slow to write it this way, but not once did I have to open the debugger, so the process actually flowed quite quickly."

p50
"Refactoring (noun): a change made to the internal structure of software to make it easier to understand and cheaper to modify without changing its observable behavior."

p51
"Refactor (verb): to restructure software by applying a series of refactorings without changing its observable behavior."

p51
"Only changes made to make the software easier to understand are refactorings. A good contrast is performance optimization. ...however [with performance optimization], the purpose is different. Performance optimization often makes code harder to understand, but you need to do it to get the performance you need."

p51
"The software still carries out the same function that it did before. Any user, whether an end user or another programmer, cannot tell that things have changed."

p51
"When you add function, you shouldn't be changing existing code; you are just adding new capabilities. You can measure your progress by adding tests and getting the tests to work. When you refactor, you make a point of not adding function; you only restructure the code."

p54
Kent Beck's metaphor of two hats:
"When you use refactoring to develop software, you divide your time between two distinct activities: adding function and refactoring. When you add function, you shouldn't be changing existing code; you are just adding new capabilities. You can measure your progress by adding tests and getting the tests to work. When you refactor, you make a point of not adding function; you only restructure the code."

p55
"Without refactoring, the design of the program will decay. [explanation why] It becomes harder to see the design by reading the code. Refactoring is rather like tidying up the code. Work is done to remove bits tthat aren't really in the right place. Loss of the structure of code has a cumulative effect. The harder it is to see the design of the code, the harder it is to preserve it, and the more rapidly it decays."

p55
"Reducing the amount of code does, however, make a big difference in the modification of the code. ... By eliminating the duplicates [sections of code in unrefactored code], you  ensure that the code says everything once and only once, which is the essence of good design."

p56
"I use refactoring to help me understand unfamiliar code."

p57
"[the way in which refactoring helps one find bugs] reminds me of a statement Kent Beck often makes about himself, 'I'm not a great programmer; I'm just a good programmer with great habits.' Refactoring helps me be much more effective at writing robust code."

p57
"In the end, all the earlier points come down to this: Refactoring helps you develop code more quickly."

p58
"In almost all cases, I'm opposed to setting aside time for refactoring. In my view refactoring is not an activity you set aside time to do. Refactoring is something you do all the time in little bursts. You don't decide to refactor, you refactor because you want to do something else, and refactoring helps you do that other thing."

p58
The Rule of Three:
"Here's a guideline Don Roberts gave me: The first time you do something, you just do it. The second time you do something similar, you wince at the duplication, but you do the duplicate thing anyway. The third time you do something similar, you refactor."

p59
Refactoring in Code Reviews:
"My experience suggests having one reviewer and the original author work on the code together. The reviewer suggests changes, and they both decide whether the changes can be easily factored in."

p60
Note by Kent Beck:
"What is it that makes programs hard to work with? Four things I can think of as I am typing this are as follows:
- Programs that are hard to read are hard to modify.
- Programs that have duplicated logic are hard to modify.
- Programs that require additional behavior that requires you to change running code are hard to modify.
- Programs with complex conditional logic are hard to modify.
Refactoring is the process of taking a running program and adding to its value, not by changing its behavior but by giving it more of these qualities that enable us to continue developing at speed."

p61
"The fastest way is to refactor; therefore I refactor."

p62
Beck, on indirection:
"Speculative design is an attempt to put all the good qualities into the system before any code is written. Then the code can be just hung on the sturdy skeleton. The problem with this process is that it is too easy to guess wrong. With refactoring, you are never in danger of being completely wrong. The program always behaves at the end as it did at the beginning. In addition, you have the opportunity to add valuable qualities to the code."

p65
"Using published interfaces is useful, but it comes with a cost. So don't publish interfaces unless you really need to. This may mean modifying your code ownership rules to allow people to change other people's code in order to support an interface change. Often it is a good idea to do this with pair programming."

p66
On rewriting vs refactoring:
"Remember, code has to work mostly correctly before you refactor. A compromise route is to refactor a large piece of software into components with strong encapsulation. Then you can make a refactor-versus-rebuild decision for one component at a time. ... With a key legacy system, this would certainly be an appealing direction to take."

p66
On refactoring close to a deadline:
"Ward Cunningham describes unfinished refactoring as going into debt. Most companies need some debt in order to function efficiently. ... You can bear some interest payments, but if the payments become too great, you will be overwhelmed. It is important to manage your debt, paying parts of it off by means of refactoring."

p66
"Not having enough time usually is a sign that you need to do some refactoring."

p67
"With refactoring the emphasis changes. You still do upfront design, but now you don't try to find the solution. Instead all you want is a reasonable solution. You know that as you build the solution, as you understand more about the problem, you realize that the best solution is different from the one you originally came up with. With refactoring, this is not a problem, for it n o longer is expensive to make the changes."

p68
"With refactoring you approach the risks of change differently, You still think about potential changes, you still consider flexible solutions. But instead of implementing these flexible solutions, you ask yourself, 'How difficult is it going to be to refactor a simple solution into the flexible solution?' If, as happens most of the time, the answer is 'pretty easy,' then you just implement the simple solution."

p69
On refactoring and performance:
"Refactoring certainly will make software go more slowly, but it also makes the software more amenable to performance tuning. The secret to fast software, in all but hard real-time contexts, is to write tunable software first and then to tune it for sufficient speed."

p70
"The interesting thing about performance is that if you analyze most programs, you find that they waste most of their time in a small fraction of code. If you optimize all the code equally, you end up with 90 percent of the optimizations wasted, because you are optimizing code that isn't run much. The time spent making the program fast, the time lost because of lack of clarity, is all wasted time."

--

smells

Duplicated Code — 76

Long Method — 76
"A heuristic we follow is that whenever we feel the need to comment something, we write a method instead. Such a method contains the code that was commented but is named after the intention of the code rather than how it does it."

Large Class — 78
"If your large class is a GUI class, you may need to move data and behavior to a separate domain object. This may require keeping some duplicate data in both places and keeping the data in sync."

Long Parameter List — 78
[use objects that know about the values you need, if you can]

Divergent Change — 79
"Any change to handle a variation should change a single class, and all the typing in the new class should express the variation."

Shotgun Surgery — 80
"Divergent change is one class that suffers many kinds of changes, and shotgun surgery is one change that alters many classes. Either way you want to arrange things so that, ideally, there is a one-to-one link between common changes and classes."

Feature Envy — 80
"The whole point of objects is that they are a technique to package data with the processes used on that data. A classic smell [this one] is a method that seems more interested in a class other than the one it actually is in."
— 80
"Of course there are several sophisticated patterns that break this rule. From the Gang of Four Strategy and Visitor immediately leap to mind... You can use these to combat the divergent change smell. The fundamental rule is to put things together that change together."

Data Clumps — 81
"Bunches of data that hang around together really ought to be made into their own object."
— 81
"Don't worry about data clumps that use only some of the fields of the new object. As long as you are replacing two or more fields with the new object, you'll come out ahead."
— 81
"A good test is to consider deleting one of the data values: if you did this, would the others make any sense? If they don't, it's a sure sign that you have an object that's dying to be born."

Primitive Obsession — 81

Switch Statements — 82
"The problem with switch statements is that of duplication. Often you find the same switch statement scattered about a program in different places. ... The object-oriented notion of polymorphism gives you an elegant way to deal with this problem."
— 82
"Most times you see a switch statement you should consider polymorphism. The issue is where the polymorphism should occur."

Speculative Generality — 83
"Speculative generality can be spotted when the only users of a method or class are test cases"

Temporary Field — 84
[why and how one might deal with a field which is only used in a specific codepath]

Message Chains — 84



Comments — 87
"...comments aren't a bad smell; indeed they are a sweet smell. The reason we mention comments here is that comments often are used as a deodorant."
— 88
"When you feel the need to write a comment, first try to refactor the code so that any comment becomes superfluous."
— 88
"A good time to use a comment is when you don't know what to do."


--

toward a catalog of refactorings

p103
"The summary includes a short statement of the problem that the refactoring helps you with, a short description of what you do, and a sketch that shows you a simple before and after example."

p106
"The refactorings in this book are my notes about the refactorings I use."

p106-7
"Another aspect to remember about these refactorings is that they are described with single-process software in mind. In time, I hope to see refactorings described for use with concurrent and distributed programming. Such refactorings will be different. For example, in single-process software you never need to worry how often you call a method; method calls are cheap. With distributed software, however, round trips have to be minimized. There are different refactorings for those flavors of programming..."

p107
"As the essential Gang of Four book says, 'Design Patterns... provide targets for your refacotrings.' There is a natural relation between patterns and refactorings. Patterns are where you want to be; refactorings are ways to get there from somewhere else."

--

composing methods

p109
"The key refactoring is Extract Method, which takes a clump of code and turns it into its own method."

Extract Method — 110-1
"To me length [functions] is not the issue. The key is the semantic distance between the method name and the method body. If extracting improves clarity, do it, even if the name is longer than the code you have extracted."

Inline Method — 117
"Another time to use Inline Method is when you have a group of methods that seem badly factored. You can inline them all into one big method and then reextract the methods."

Replace Temp with Query — 120
"...temps tend to encourage longer methods, because that's the only way you can reach the temp. By replacing the temp with a query method, any method in the class can get at the information."
— 121
[When refactoring out temp values, consider making that variable final, or a constant, or some other kind of invariant. This way you can make sure that it only gets one assignment.]
— 121
"You may be concerned about performance in this case. As with other performance issues, let it slide for the moment. Nine times out of ten, it won't matter. When it does matter, you will fix the problem during optimization."


-- 

Organizing Data

Replace Data Value with Object — 175

Change Value to Reference — 179
"The decision between reference objects and value objects is not always clear. Sometimes you start with a simple value with a small amount of immutable data. Then you want to give it some changeable data and ensure that the changes ripple to everyone referring to the object. At this point you need to turn it into a reference object."



--

Simplifying Conditional Expressions

Introduce Null Object — 260
[when you have repeated checks for a null value; replace the null value with a null object]
— 260
"The essence of polymorphism is that instead of asking an object what type it is and then invoking some behavior based on the answer, you just invoke the behavior. The object, depending on its type, does the right thing."
—261 (from quote by Ron Jeffries)
"An interesting characteristic of using null objects is that things almost never blow up. Because the null object responds to all the same messages as a real one, the system generally behaves normally. This can sometimes make it difficult to detect or find a problem, because nothing ever breaks."
— 261
"Create a subclass of the source class to act as a null version of the class. Create an isNull operation on the source class [returns false] and the null class  [returns true]."
— 263
"If you like, you can signal the use of null object by means of an interface."
— 263
"I like to add a factory method to create null customers. That way clients don't have to know about the null class."
— 265
"...this movement of behavior [from testing for null to polymorphic delegation] makes sense only when most clients want the same response. ... Any clients who want a different response to the standard one can still test using isNull."
— 266
"When carrying out this refactoring, you can have several kinds of null. ... If that is the case, you can build separate classes for the different null cases."
— 266
"Sometimes null objects actually can carry data, such as usage records for the unknown customer, so that we can bill the customers when we find out who they are."

