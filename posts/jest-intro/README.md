# Intro to Jest

Jest is a testing tool for JavaScript with 3 parts:

* A syntax for declaring and organizing tests
* A library for asserting things about JavaScript code
* A CLI tool for running tests and reporting the results.

Jest tests look like this:

```js
describe("A group of tests", () => {
  it("is a test", () => {
    expect(1).toBe(1)
  })
  it("is another test", () => {
    const mockFunction = jest.fn(() => {})
    mockFunction()
    expect(mockFunction).toHaveBeenCalledTimes(1)
  })
})
```

## Installing and Configuring

To install Jest on a JavaScript project, run:

```bash
npm install -D jest
```

Jest is setup to run from an `npm` script:

```json
{
  "name": "some-project-name",
  "scripts": {
    "start": "node index.js",
    "test": "jest"
  },
  "devDependencies": {
    "jest": "^27.2.0"
  }
}
```

Jest can now be run with `npm test` on the command line. By default Jest will try to execute any file ending in `.test.js`.

It's often useful to keep Jest running after tests complete so that it can rerun when files change. To do this, add the `--watch` flag to `jest`:

```json
{
  "name": "some-project-name",
  "scripts": {
    "start": "node index.js",
    "test": "jest",
    "test:watch": "jest --watch"
  },
  "devDependencies": {
    "jest": "^27.2.0"
  }
}
```

## Test Files

The simplest test files import a JavaScript function or module, declare a new `test`, and then assert something about the code:

```js
const { add } = require("./math")

test("add sums two positive integers", () => {
  const sum = add(2, 3)
  expect(sum).toEqual(5)
})
```

* `test` is a built-in Jest function that takes a test name as a string and a function containing the test code.
* If anything inside the function throws an error, the test fails. Otherwise, it passes.
* `expect` is a built-in Jest function that accepts any expression. That expression will be compared against a "matcher" method that's chained from `expect()`.
* `.toEqual()` is the simplest matcher method. It asserts that whatever expression was given to `expect` is equal to some value. If it isn't, it throws an error.

When the tests are run, the name of the test will display with a red X or green checkmark indicating whether or not it was able to run the code inside of that test without an error being thrown.

## Watch Out!

* Jest tests are technically Node.js code, even if your project isn't otherwise a Node.js project. That means you may need to use `require` syntax to import modules instead of `import` unless you've configured your project to use `import`/`export` syntax. The code you're testing can export modules with either the standard `export` syntax or Node's `module.export` syntax.
* `test` and `expect` don't need to imported, Jest makes them available when it runs the tests.

## Additional Resources

| Resource | Description |
| --- | --- |
| [Jest](https://jestjs.io/) | Official Jest documentation |
