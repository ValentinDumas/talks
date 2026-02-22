## Opening Hook (0:00–0:03)
https://smartbear.com/blog/bug-day-460m-loss/
**"The $300 Million Bug" Story**: Start with the 2012 Knight Capital Group incident, where untested legacy code caused catastrophic financial losses. Use this as a visceral example of why legacy systems demand strategic care.

**Interactive Poll**: Ask attendees, "Raise your hand if you’ve inherited a codebase that felt like a Jenga tower?" Transition into defining legacy code as "code that makes you afraid to make changes" (paraphrasing Michael Feathers).
    - [image] Jenga tower 
- [image] du jeu Mikado, puis [image] de pâtes.

*Mais au fait c'est quoi un code legacy ?*

## Part 1: Understanding Legacy Code
https://gist.github.com/jkone27/2587bdd8d0816b4bf74263f3c1a1287a
https://www.youtube.com/watch?v=mwVRHDD0tEk
- Defining Legacy Code: Characteristics such as lack of tests, outdated tech, and complex entanglements.

    "Legacy code is code without tests"
        - if you have code with lots of tests = ez to change
        - code without tests = u're in serious trouble :)

- Common Challenges: Share vivid anecdotes illustrating maintainability and integration hurdles in legacy systems.


    Key Insight: "Legacy code isn’t about age – it’s about the cost of change."

- Introduction of Live Coding Example (from Part3):
  - https://understandlegacycode.com/blog/5-coding-exercises-to-practice-refactoring-legacy-code/
  - Present a concise, representative legacy code snippet (e.g., a tangled payment validation module or order processing logic) that will be revisited during the session for demonstrations and refactorings.
  - **Live Visual**: Use a dependency analysis tool (e.g., NDepend) to generate a code-mesh diagram of a sample legacy system, showing tangled dependencies.



## Part 2: Refactor vs Rewrite Dilemma - A Battlefield decision (0:10–0:25)

### Possibilités: 7: https://www.gartner.com/smarterwithgartner/7-options-to-modernize-legacy-systems
    - Focus: (4)refacto / (5)rearchitecdt / (6)rewrite.

###### Decision Framework: Introduce the "3 Rs Rule": TODO: IDK !
    1. **Retrofit** (refactor incrementally)
        - (Apply Sprout Method/Wrap Method)
       2. **Replace** (rewrite modules)
           - (Use Strangler Fig Pattern for incremental replacement)
       3. **Rebuild** (full rewrite)
           - (Full rewrite only after proving viability via Tracer Bullet prototyping)
- Decision Factors:
  - Discuss code quality (code smells, ..). How ?
    - Divergent Change (multiple modifications for one feature)
    - Shotgun Surgery (one change requires many edits)
    - Feature Envy (methods excessively access another class' data)
    - Use these smells to quantify technical debt during evaluation.
  - Discuss business constraints, risk, and resource availability influencing refactor or rewrite choices.

#### Case Study / Fight 1 – The Perils of rewriting / Rewriting Trap:
- A fintech startup spent 18 months rewriting a core banking system only to discover undocumented edge cases during migration.
- TODO: fetch story details + logo.
- Live Demo: Use git blame on a sample codebase to show how "ancient" code often contains hidden business rules.
- BUT, "it is possible.. How ?"
    - Tracer Bullet Prototyping
  - TODO: greenfield vs brownfield dev.
    - TODO: ... + need to reaerchitect ??
    - Preservation techniques:
      - Parallel Change: Run old/new systems concurrently during rewrite
      - Feature Flags: Gradually enable refactored components
    - key takeaways: pros/cons ?

[Transition] si on estime que les [refacto]pros>>[refacto]cons, on refacto.

#### Case Study / Fight 2 – The Refactor Victory:
- An e-commerce platform incrementally extracted a monolith into microservices, achieving 40% faster deployment cycles.
- Live Demo: Perform a sprout method refactoring – add new features alongside legacy code without touching it.

[Takeaway] Compare in which cases we refacto or rewrite
[Takeaway] Rewrite: techniques;
[Takeaway] Refacto: techniques;



## Part 3: Live Demo, refactoring in Action
- Testing and refactoring legacy code https://www.youtube.com/watch?v=LSqbXorkyfQ
- https://www.youtube.com/watch?v=9HmVrfkzm9I
- "To test, we need to KNOW what it DOES (Learn more about the system) --> characterization tests"

TODO: check if the video has test in examples.
If not at all, then we can apply bullet points below to both "test/no test" sections.

### Live Demo Flow
- Setup: Present the legacy code snippet introduced earlier, highlighting its issues (tangled logic).
  - https://understandlegacycode.com/blog/5-coding-exercises-to-practice-refactoring-legacy-code/
    - use Trivia ? https://github.com/jbrains/trivia/tree/master/java 
- 2 cas de figure:
  - Quand y'a quelques tests ?
  - Quand y'a ZERO tests et que c'est ultra complikeyy ?!
- Refactoring Process:
  - Introduce [before refactoring] characterization tests using the Golden Master technique to capture existing behavior safely.
      - [if needed] Use ApprovalTests to capture current behavior of a legacy payment validator.
      - [if needed] Mutate the code to show test failures proving their value.
  - [if enough time] Apply the Mikado Method to break down refactoring into small, deployable steps, avoiding tunnel vision.
  - Incrementally improve code structure, decouple dependencies, and add unit tests, demonstrating techniques from Working Effectively with Legacy Code by Michael Feathers.
  - TDD in Legacy Terrain: add a new currency validation rule using TDD, showcasing how to grow tests around legacy components.
  - BDD Collaboration: - invite an audience member to write a Gherkin scenario for a new feature, then implement it.
  - Outcome: Show improved readability, testability, and maintainability of the refactored code.
- Reusable Example: Mention this example will be referenced later when discussing testing strategies and metrics.

**Final Rallying Cry**: End with a split-screen comparison:
- Left: A legacy codebase’s file (5000 LOC, no tests)
- Right: The same system after 6 months of disciplined refactoring

[Takeaway / Techniques]
- [?] Wrapper Generation (demo generating an API facade around legacy SOAP services)
- ...

[Takeaway] Mikado method / Characterization tests

[Teakeway] Testing as Your Forcefield
### The Testing Pyramid Reborn:
    [New Code]          
    ↗ TDD ↖            
    [Legacy Code] → Characterization Tests  
    ↘ BDD ↙            
    [Business]



### DORA Metrics Impact Analysis (0:40 – 0:45)
- Introduction to DORA Metrics: Briefly explain the four key metrics:
    - Deployment Frequency 
    - Lead Time for Changes 
    - Change Failure Rate 
    - Mean Time to Restore (MTTR)

- Impact on Legacy Code Management:
  - How refactoring legacy systems and improving test coverage can increase deployment frequency and reduce lead time by enabling smaller, safer changes.
  - How reducing change failure rate and MTTR ties directly to better testing and incremental refactoring strategies.
  - Real-world examples linking refactoring efforts to measurable improvements in DORA metrics (e.g., faster recovery from defects, more frequent releases). Call to Action: Encourage attendees to measure these metrics as part of their legacy code improvement initiatives to track progress and justify investments.

- **Culture / Call to Action**:
  - Encourage attendees to measure these metrics as part of their legacy code improvement initiatives to track progress and justify investments.
  - Share the "20% Legacy Tax" practice – dedicating 1 day/week to debt reduction.



### Conclusion
- Key Takeaways:
    - Legacy code challenges require strategic evaluation between refactoring and rewriting.
    - Testing (especially characterization tests) is essential to safe refactoring.
    - DORA metrics provide a powerful lens to measure and improve software delivery performance through legacy code management.
- Final Thoughts: Advocate for continuous improvement, adaptability, and data-driven decision-making when working with legacy systems.

---

Post-Session Resource Sharing
- Michael Feathers’ Working Effectively with Legacy Code
- Martin Fowler’s Refactoring
- Live coding katas for legacy code practice (e.g., Gilded Rose kata)
- Tools and techniques: Golden Master, Mikado Method, DORA metrics dashboards.

**Q&A Catalyst**: Pose, "What’s the one legacy system you wish you could eliminate – and what’s stopping you?"

---

## Dependency-breaking patterns:
Fowler's Catalog Techniques :

    Scenario	Technique	Example
    Complex conditionals	Decompose Conditional	Split 10-line if into isEligible() method
    Data clusters	Introduce Parameter Object	Replace (lat, lng) with GeoCoordinate class
    Tight coupling	Hide Delegate	Encapsulate third-party API calls behind facade

## ...others?

TDOO: fetch AI impact on coding practices / refacto practices.
https://michaelfeathers.silvrback.com/possible-ai-impacts-on-development-practice



