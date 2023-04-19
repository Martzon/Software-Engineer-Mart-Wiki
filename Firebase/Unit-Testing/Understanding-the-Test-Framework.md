The unit testing principles applied in other tech stack such as in `.NET Core` are still applied for writing unit tests in `Firebase`

You should:
1. Practice `Dependency Injection`; all dependencies of a class should be injected through the constructor
2. Know how stubbing and/or mocking work
3. Know the AAA and Single Assertion standard
4. Know the `Test Initialize / Setup` and/or `Test Cleanup / Teardown` blocks

# Test Classes
Will be written in `TypeScript` together with the other `JavaScript` test frameworks below. Our standard from .NET still carries over here, here are some:
1. One test class/file per class
2. AAA
3. Single Assertion per `[TestMethod]` or `it` in `Mocha`
4. Instead of a separate `**.Tests` project, we will just have a `/tests` folder in our `Firebase` app e.g. `functions/tests`


# Mocha
Is the test runner; runs the test classes written in `TypeScript` with the help of `ts-node`, because this is originally intended to run pure `JS` tests.

Some concepts, functions, keywords, snippets you will encounter that comes from `Mocha`:
1. `describe` - "describes" a block of test methods. Use this to "describe" or group your test methods on what they test e.g. happy path, sad path, errors, constructor, and etc.
   - The test class should have an outer `describe('ClassToBeTested', ...)`
   - Each method of the class being tested shall be grouped in another `describe('methodName', ...)`
   - Different scenarios/outcomes for each method should be further described: `describe('An error is thrown', ...)`
2. `beforeEach` - for every "describe" grouping, you can put a `beforeEach` block that runs the code block "before each" test method is ran in that "describe" grouping.
   - Use  this to arrange stubs. Time to create fake data and setup your stubs to return it.

# Chai
Is the assertion library. We used `Chai` because it works very well with our stubbing library `Sinon`. It also provides a handful of utility methods to assert `Promises` which is very common to our project.

Some concepts, functions, keywords, snippets you will encounter that comes from `Chai`:
1. `expect` - is the way to assert or evaluate tests. It's a fluent way (chainable) to make assertions in your test method.
   - For example, to assert if two values are equal using `expect`, you can `expect(actual).to.equal(expected)`
   - When these expectations fail, the test method will also fail (obviously)
2. `expect` is more than just comparing two values; it can also check if your `sinon.spy` is called, it can also check if your test throws an exception/error, and it can even check if your method that returns a `Promise` resolved or rejected.
   - Some of the calls to validate spy calls will look like `expect(loggerStub.log).to.have.been.calledWith(...)`. This checks if the logger gets called with the provided parameters.

# Sinon
Is the stubbing/mocking/spying library. This will allow is to stub out and create a fake implementation of the dependencies that our class have, to trigger certain conditions/scenarios.

Some concepts, functions, keywords, snippets you will encounter that comes from `Sinon`:
1. `sinon.stub()` -> creates a "stub" or an object that you can easily alter the behavior/result using `someStub.returns`
2. `sendgridStub.sendEmail.returns(...)` -> if you have created a `sendgridStub` using `let sendgridStub = sinon.stub()`, and you want to "fake" the return of it's method `sendEmail`, then this is the way to go.
   - If `sendEmail` returns a `Promise` and you want to simulate a successful call, you can set it up by `sendgridStub.sendEmail.returns(Promise.resolve({...})` so that the outer code will proceed/not catch an error
   - You may pass in necessary arguments in the resolve to simulate certain behaviors in the client code/class that is under test


# NYC
Is the test coverage tool/viewer


