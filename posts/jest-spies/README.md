# Jest: Spies and Mocks

To test code that accepts higher-order functions, create a spy with `jest.fn()`:

```js
const someSpy = jest.fn()
```

This is a function that records information about how or whether it was called, as well as which arguments it was given.

```js
const someSpy = jest.fn()
someFunction(someSpy)
expect(someSpy).toHaveBeenCalled()
```

Note that the assertion is happening on the spy, not on the actual code being tested. This is a common way to test the behavior of higher-order functions and components that accept functions as props.

## Spy Matchers

These are some common matchers called on spies:

| Matcher |
| --- |
| `expect(someSpy).toHaveBeenCalled()` |
| `expect(someSpy).toHaveBeenCalledWith(firstArgument, secondArgument, thirdArgument)` |
| `expect(someSpy).toHaveBeenCalledTimes(invocationCount)` |
| `expect(someSpy).toHaveBeenNthCalledWith(invocationNumber, firstArgument, secondArgument)` |

## Stubs and Mocks

Sometimes code that accepts functions also needs those functions to return a value. You can do this by returning a hard-coded value from a function passed into `jest.fn()`:

```js
const someSpy = jest.fn(() => "Hi")
printMessage(someSpy)
expect(someSpy).toHaveBeenCalled()
```

These functions can also accept arguments and use them in mock implementations:

```js
const someSpy = jest.fn(number => number * 2)

map(someSpy)(["a", "b", "c"])

expect(someSpy).toHaveBeenNthCalledWith(1, "a")
expect(someSpy).toHaveBeenNthCalledWith(2, "b")
expect(someSpy).toHaveBeenNthCalledWith(3, "c")
```

It's very important to keep your mock implementations simple; ignore arguments and return static values when possible. It's easy to start reimplementing functionality that already exists elsewhere. If you start feeling like you need to test your tests, your mocks are too complicated.

## Mocking Modules

If your code uses a third-party library or other module, you may want to mock it to prevent it from actually executing. To do:

1. Import the module into your test file
2. Pass the name of the module as a string into `jest.mock()`
3. Use methods like `mockReturnedValue` and `mockRejectedValue` on any methods that your application code uses

For example:

```js
import axios from "axios"
import someCode from "./some-code"

jest.mock("axios")

test("Some Test", async () => {
  axios.get.mockResolvedValue({ data: "Some Data" })

  expect(someCode()).resolves.toEqual({ data: "Some Data" })
})
```

## Promises

If the function you're spying on is a promise, you can mock its resolved or rejected values:

```js
const someSpy = jest.fn().mockResolvedValue({ result: "success" })
const someSpy = jest.fn().mockRejectedValue({ error: "Uh oh" })
```

## Different Responses For Different Invocations

To help keep logic out of your mock implementations, you can have the same spy return different values based on which time it's invoked by chaining `mockReturnValueOnce` calls:

```js
const someSpy = jest.fn(() => 4) // Default, returned from the fourth call and onward
  .mockReturnValueOnce(1) // Returned from the first call
  .mockReturnValueOnce(2) // Returned from the second call
  .mockReturnValueOnce(3) // Returned from the third call
```

This works the same way with promises:

```js
const someSpy = jest.fn()
  .mockResolvedValue({ result: "4" }) // Default, fourth call and onward
  .mockResolvedValueOnce({ result: "1" }) // First call
  .mockResolvedValueOnce({ result: "2" }) // Second call
  .mockResolvedValueOnce({ result: "3" }) // Third call

const someSpy = jest.fn()
  .mockRejectedValue({ error: "4" }) // Default, fourth call and onward
  .mockRejectedValueOnce({ error: "1" }) // First call
  .mockRejectedValueOnce({ error: "2" }) // Second call
  .mockRejectedValueOnce({ error: "3" }) // Third call
```

## Inspecting Spies and Mocks

Since tests are used to run your code, it may be useful to examine how spies are being called. Each spy has a `.mock` property containing information about how it's been used so far.

* **`someSpy.mock.calls`**: An array of arrays with all arguments the spy has been called with
* **`someSpy.mock.results`**: An array with all return values the spy has been called with

For example:

```js
const additionSpy = jest.fn((numberOne, numberTwo) => numberOne + numberTwo)
additionSpy(1, 2)
additionSpy(3, 4)
additionSpy(5, 6)
console.log(addSpy.mock.calls) // [[1, 2], [3, 4], [5, 6]]
console.log(addSpy.mock.results) // [3, 7, 11]
```

## Watch Out

Don't make assertions on the `.mock.calls` or `.mock.result` of a spy, use the appropriate matcher instead.

## Additional Resources

| Resource | Description |
| --- | --- |
| [Mock Functions](https://jestjs.io/docs/mock-functions) | Official reference for Jest spies. |
| [Jest `expect` API](https://jestjs.io/docs/en/expect) | Official reference for Jest matchers. |
