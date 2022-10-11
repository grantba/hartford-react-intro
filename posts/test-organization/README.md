# Test Organization with Jest

## Levels of Organization In Tests

Test organization happens on 3 levels: The file system, within a test file, and within a test.

## Organizing Test Files

Files are the primary unit of test organization. In Jest, every test file must end in `.test.js`, `.spec.js`, or their `.ts` equivalents to be recognized by the test runner, but aside from that the test files can be placed anywhere. Here are some suggestions:

* Keep test files in the same directory as the code they test. This makes them easy to find, which means they'll be more likely to be read and maintained. This is especially useful for unit and component tests, where it's easy to maintain a 1-to-1 correspondence between code files and test files.
* Keep all test files in a separate folder from the source code. This keeps both folder hierarchies less noisy and makes it easier to jump between different test files. This is especially useful for E2E and integration tests that aren't associated with any particular part of the source code.
* Split tests into separate folder hierarchies for unit, integration, and E2E tests files.
* Organize test files by putting them in directories named after the features they're primarily used in.

You can also mix and match these into your own strategy. All of these are equally valid approaches, just make sure they make sense for the kind of code you're testing and you apply your file organization strategy consistently so other developers can find the files.

## Organizing Within Test Files

The only level of organization test files are required to have is calling `test()` or `it()` to declare test cases. There are even [strong arguments](https://kentcdodds.com/blog/avoid-nesting-when-youre-testing) for why intentionally keeping the organizational complexity low improves test readability. That said, there are some structures built into Jest that may improve your test code.

### Grouping Tests with `describe()` and `context()`

To group tests, wrap them in a `describe` or `context` function:

```js
describe("Bank ledger", () => {
  context("Starting with a positive balance", () => {
    it("allows withdrawals up to the balance", () => {
      // Test code
    })
    it("doesn't allow withdrawals over the balance", () => {
      // Test code
    })
  })
  context("Starting with a zero balance", () => {
    it("doesn't allow withdrawals", () => {
      // Test code
    })
  })
  context("Starting with a negative balance", () => {
    it("doesn't allow withdrawals", () => {
      // Test code
    })
  })
}
```

Creating a hierarchy like this allows for tests to easily reuse setup with `before` and `beforeEach` calls and is common in BDD-style testing. It can make it easier to see what is and isn't being tested from a high level, but it's also harder to see what any one test case is doing since it requires so much additional context.

### Setting Up Tests With `beforeEach()` and `beforeAll()`

Jest ships with two functions that allow you to run setup code before each of your tests. `beforeAll()` runs once before any of your tests, `beforeEach()` runs before every one of your tests. These can either run for the entire file or for a particular `describe` or `context` block.

```js
describe("Bank ledger", () => {
  beforeAll(() => createBankAccount())
  beforeEach(() => {
    resetBankAccount()
  })

  context("Starting with a positive balance", () => {
    beforeEach(() => {
      setBalance(10000)
    })
    it("allows withdrawals up to the balance", () => (/* Test code */))
    it("doesn't allow withdrawals over the balance", () => (/* Test code */))
  })
  context("Starting with a zero balance", () => {
    beforeEach(() => {
      setBalance(0)
    })
    it("doesn't allow withdrawals", () => (/* Test code */))
  })
  context("Starting with a negative balance", () => {
    beforeEach(() => {
      setBalance(-10000)
    })
    it("doesn't allow withdrawals", () => (/* Test code */))
  })
}
```

Extracting this kind of test setup into `before` hooks is common in BDD, but hurts test readability. Application code generally strives to be DRY and abstract out all shared code. In contrast, since tests need to function as documentation it's desirable to repeat yourself often so that everything needed to understand the test is in one place. For example, compare these two approaches:

```js
describe("Bank ledger", () => {
  beforeAll(() => createBankAccount())
  beforeEach(() => {
    resetBankAccount()
  })

  context("Starting with a positive balance", () => {
    beforeEach(() => {
      setBalance(10000)
    })
    it("allows withdrawals up to the balance", () => (/* Test code */))
    it("doesn't allow withdrawals over the balance", () => (/* Test code */))
  })
}
```

vs.

```js
beforeAll(() => createBankAccount())

test("Bank ledgers with positive balances allow withdrawals up to the balance", () => {
  resetBankAccount()
  setBalance(10000)
  // Test code
})

test("Bankledgers with positive balances don't allow withdrawals over the balance", () => {
  resetBankAccount()
  setBalance(10000)
  // Test code
})
```

Both test suites are the same, but the second one is much easier to follow. Don't be afraid of repeating yourself and avoid hasty abstractions.

## Within Tests

Within a test, keep the arrangement of conditions, action execution, and assertion separate. This helps tests from doing too many things at once. Another way to think of these is Given/When/Then:

* Given the system being tested is in a particular state
* When a certain action is taken
* Then a particular thing happens

For example:

```js
test("Bank ledgers with positive balances allow withdrawals up to the balance", () => {
  // Given I have a correctly setup bank account with a positive balance
  resetBankAccount()
  setBalance(10000)

  // When I withdraw up to my balance
  const cash = withdraw(10000)

  // Then I have that money as cash
  expect(cash).toBe(10000)
})
```

Sometimes `expect` assertions put the action directly in the call:

```js
expect(withdraw(10000)).toBe(10000)
```

There are no hard rules on this. Consider whether having an extra variable makes the test easier or harder to follow. In the above case, it probably hurts readability. In this case it probably helps:

```js
expect(withdraw(10001)).toThrow()
```

Use whichever style has the least noise and the most clarity for that particular test.

### Watch Out!

* Keep test files small, prefer them as a unit of organization over lots of describes and nesting.
* `describe()` and `context()` are the same, as are `it()` and `test()`. `describe` and `it` come from RSpec and a testing philosophy called BDD. `context` and `test` are more agnostic. Use whichever one makes your tests easier to read.
* `describe()` and `context()` functions can be nested within each other to create subgroups of tests. `test()` and `it()` functions always represent individual tests and cannot be nested.
* Any one test can have as many assertions as you like, but be careful about asserting too many things in one test. Each test should represent one reason why the system could fail. If you use multiple assertions in a test, they should all fail for the same reason.
* There are `afterEach` and `afterAll` hooks, but they should be avoided as there is no guarantee they will run. Initial conditions for each test should be ensured either in the test itself or in `beforeEach` and `beforeAll` hooks.
* Tests should be able to run in any order. That means one test shouldn't rely on the state from another test. Use `beforeEach` or manually reset state at the beginning of each to make them order-independent.

## Additional Resources

| Resource | Description |
| --- | --- |
| [Avoid Nesting When You're Testing](https://kentcdodds.com/blog/avoid-nesting-when-youre-testing) | Thoughtful blog post on the benefits of not using abstractions in testing |
