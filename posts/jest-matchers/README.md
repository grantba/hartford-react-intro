# Jest: Basic Matchers

Matchers assert things about the values being examined by `expect`. The most simple matcher is `.toEqual`:

```js
expect(4).toEqual(4)
```

Using the other matchers has several benefits:

* They keep logic out of your tests. For example, using the `.resolves` chainer reduces the likelihood of making a mistake manually resolving a promise and asserting the resolved value.
* They make error messages more expressive.
* They serve as better documentation because they read more like sentences and less like code.

Jest comes with a large number of matchers. These are some of the most common and useful:

## Simple Values

| Matcher | Purpose |
| --- | --- |
| `expect(someTestResult).toBe(someValue)` | Basic assertion, used with strings, numbers, and booleans |
| `expect(someTestResult).toBeNull()`, `expect(someValue).toBeUndefined()` | Basic assertion, used with `null` and `undefined`. Note that those values should not be tested using `toBe` or `toEqual`. |
| `expect(someTestResult).toBeTruthy()`, `expect(someValue).toBeFalsy()` | Used to test either the presence or absence of something when its specific value is unimportant. |

## Strings

| Matcher | Purpose |
| --- | --- |
| `expect(someTestResult).toContain(someValue)` | Tests that a string contains another string |
| `expect(someTestResult).toMatch(someValue)` | Tests that a string contains a regex match |

## Arrays

| Matcher | Purpose |
| --- | --- |
| `expect(someTestResult).toEqual(someValue)` | Basic assertion, used with objects and arrays |
| `expect(someTestResult).toHaveLength(someCount)` | Asserts the length of an array or string |
| `expect(someTestResult).toContain(someValue)` | Tests that a string, number, or boolean is in an array |
| `expect(someTestResult).toContainEqual(someValue)` | Tests that an object or array is inside an array |

## Objects 

| Matcher | Purpose |
| --- | --- |
| `expect(someTestResult).toEqual(someValue)` | Basic assertion, used with objects and arrays |
| `expect(someTestResult).toHaveProperty(someKey, someValue)` | Asserts that an object has a property, optionally with a specific value |
| `expect(someTestResult).toMatchObject(someValue)` | Tests that an object is a subset of another object |

## Chainers

These are properties that modify the matchers that come after them.

| Matcher | Purpose |
| --- | --- |
| `expect(someTestResult).not.someMatcher()` | `.not` negates whichever matcher follows it, which allows testing that a value doesn't equal, contain, etc. another value. |
| `expect(someTestResult).resolves.someMatcher())` | Tests that a promise resolves to a value |
| `expect(someTestResult).rejects.someMatcher())` | Tests that a promise rejects to a value |

Note that testing a promise makes the test asynchronous. You'll need to either return the assertion or `await` it.

## Additional Resources

| Resource | Description |
| --- | --- |
| [Jest `expect` API](https://jestjs.io/docs/en/expect) | Official reference for Jest matchers. |
