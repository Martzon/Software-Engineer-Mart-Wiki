Unit testing is a software testing method by which individual units of source code are tested to determine whether they are fit for use. A unit is the smallest possible testable software component. Usually, it performs a single cohesive function. A unit is small, so it is easier to design, execute, record, and analyze test results for than larger chunks of code are. Defects revealed by a unit test are easy to locate and relatively easy to repair.

## Why’s
- Maintainability
- Sustainability
- Readability
- Quality
- Prevents coupling
- Documentation

## How’s

The “**Arrange, Act, Assert**” pattern is a widely known way to structure the code in a unit test. It consists of breaking up the code inside a unit test into three clearly divided groups, each one representing a phase in the test:

- **Arrange**. In this phase, you do whatever preparation you need in order to run your test. Instantiation of the system under test will usually happen in this phase.
- **Act**. The name pretty much says it all. In this phase, you generally do whatever action you want to test.
- **Assert**. Finally, it’s time to verify if we’ve got the desired results.


Write your tests in such a way that the phases are clearly recognizable and then respect each part. Don’t do assertions on the Act phase, don’t arrange in the Assert phase, and so on. Also, only do **one** Assert per TestMethod.
