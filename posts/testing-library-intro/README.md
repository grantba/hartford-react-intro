## Intro to Testing Library

Jest comes with everything needed to run and make assertions about JavaScript code. However, it doesn't have any tools for making assertions about the DOM. Testing Library is a tool for easily getting elements out of the DOM and making assertions about them.

Testing Library is intended to be a generic base that can be extended for different applications. For example, there are versions of testing library for plain DOM, React, Vue, React Native, Angular, Svelte, and more. All of them use the same concepts and a similar syntax, which makes it easier for developers to move between frameworks.

## Installing

To install the most basic version of Testing Library (vanilla DOM app with the Jest test framework):

```bash
npm install --save-dev @testing-library/jest-dom
```

To use it in your Jest tests, make sure this line is included once per app in the test setup:

```js
import '@testing-library/jest-dom'
```

Additionally, the following ESLint plug-ins will add Testing Library-specific rules to ESLint:

* `eslint-plugin-jest-dom`
* `eslint-plugin-testing-library`

## Getting elements

The most important terms to understand in Testing Library are `get`, `find`, and `query`.

**`get`**: Find an element that's already in the DOM
**`find`**: Find an element that will soon be in the DOM (must be `await`ed!)
**`query`**: Look for an element that shouldn't be in the DOM

All the of them can be modified to find multiple matches by adding `All` to them: `getAll`, `findAll`, `queryAll`.

To get elements from the page, add a query to the end of the query type:

**Form Inputs**:

| Priority | Query | Description |
| --- | --- | --- |
| 1 | `ByLabelText(labelText)` | Matches form inputs by looking at the text of their attached `<label>`s or elements with the `aria-label` attribute |
| 2 | `ByPlaceholderText(placeholderText)` | Matches form inputs by their placeholder text, only use if the input is unlabeled |
| 3 | `ByDisplayValue(currentValue)` | Matches form inputs that currently have the provided value, good for update forms |

**Other Elements**:

| Priority | Query | Description |
| --- | --- | --- |
| 1 | `ByRole(ariaRole)` | Matches elements with the provided ARIA role, can be furthered narrowed by passing the `aria-label` name: `getByRole("header", { name: "primary header" })` |
| 2 | `ByText(text)` | Matches elements containing the provided text. Accepts strings or regex. |
| 3 | `ByAltText(altText)` | Matches images by their alt text |
| 4 | `ByTitle(title)` | Matches elements by their title attribute |
| 5 | `ByTestId(testId)` | Matches elements by their `data-testid` attribute, only use if no other query is appropriate |

For example:

* `getByRole("header")` will return the first element with an ARIA role of `header` and throw an error if it isn't already in the DOM.
* `await findByRole("header")` will do the same thing as `getByRole("header")`, but it will wait up to a few seconds for the element to appear in the DOM. This is useful if something needs to resolve or finish rendering.
* `getAllByText("Hello, world!")` will return every element containing the text "Hello, world!"
* `getByLabelText(/username/i)` will return the first form input with an attached label of "username" (case-insensitive)
* `queryByAltText("happy pig")` will return any images containing the alt text "happy pig", but will not error if it doesn't find any
* `await findAllByTestId("product")` will return every element with an HTML attribute of `data-testid="product"`

## Async DOM Assertions

If you need to wait for an element to show up in the DOM, use a `findBy` query. If you need to assert something asynchronous, use `waitFor` and `waitForElementToBeRemoved`. This retries the assertion for 1 second by default:

```js
const someAsyncSpy = jest.fn()
makeAnAsyncRequest(someAsyncSpy)

await waitFor(() => {
  expect(someAsyncSpy).toHaveBeenCalledTimes(1)
})
```

This waits up to 1 second by default for the queried element to not be in the DOM:

```js
showToastMessage()
await waitForElementToBeRemoved(queryByText("Registered!"))
```

## Jest DOM Matchers

The built-in Jest matchers work with any of JavaScripts native values, but none of them are designed to work specifically with DOM elements. By importing the `@testing-library/jest-dom` package at the beginning of a test file, new Jest matchers are added to `expect` for DOM elements.

### Black Box Assertions

These are common assertions made from a user's perspective:

| Matcher | Purpose |
| --- | --- |
| `expect(someElement).toBeVisible()` | Asserts that something is on the page and not obstructed. |
| `expect(someElement).toBeInTheDocument()` | Commonly combined with `.not` to assert that something isn't on the page. |
| `expect(someElement).toHaveTextContent(someRegexOrString)` | Asserts that an element contains a string or matches a regex. Use `/^text goes here$/` to do a precise match. |

### White Box Assertions

These are a little more dangerous and should be used less often because they look at the page's implementation, not its actual content.

| Matcher | Purpose |
| --- | --- |
| `expect(someElement).toHaveAttribute(attributeName, attributeValue)` | Asserts that an element has an attribute with a particulary value |
| `expect(someElement).toHaveClass(className)` | Asserts that a class is present on an element |
| `expect(someElement).toHaveStyle(someCSSPropertyValuePairs)` | Asserts that an element has any number of CSS styles applied to it |

### Form Assertions

| Matcher | Purpose |
| --- | --- |
| `expect(someFormInput).toHaveValue(someValue)` | Asserts that a form input has a particular value |
| `expect(someFormInput).toHaveFocus()` | Asserts that the form input is currently active |
| `expect(someForm).toHaveFormValues(someNameValuePairs)` | Asserts that the entire form has particular values. The keys of the object will use the `name` attribute of the elements, the values of each of them are the associated values. |
| `expect(someFormInput).toBeChecked()` | Asserts that a checkbox or radio button is selected |

## Watch Out!

* If you're waiting for an element to appear in the DOM, use `find` queries rather than using `waitFor` to wait for the element to show up.
* `query` and `queryAll` queries should only be used to get elements if you're going to assert that something _isn't_ in the DOM.
* `ByRole` should be your default query because it uses the accessibility API to find elements. Always try to use semantic elements rather than putting ARIA roles on non-semantic elements.
* `get` and `find` queries can act like implicit assertions since they throw errors that fail the test if the element isn't present. Additionally using an explicit matcher like `.toBeVisible()` or `.toBeInTheDocument()` helps document the desired behavior better.
* It's possible to extract query functions from the `render` method that are already scoped to the rendered DOM, but you should still prefer querying with the `screen` object to simulate what the user is actually presented with.
* When doing async assertions, use `waitFor` and `waitForElementToBeRemoved` on the assertion, not the behavior that triggers the async behavior.

## Additional Resources

| Resource | Description |
| --- | --- |
| [Guiding Principles](https://testing-library.com/docs/guiding-principles/) | Official principles of Testing Library |
| [Which query should I use?](https://testing-library.com/docs/queries/about/#priority) | Official Testing Library guide to choosing a query |
| [ARIA Roles](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles) | MDN's reference on different ARIA roles |
| [Guide to Disappearance](https://testing-library.com/docs/guide-disappearance) | Official testing library guide to working with elements that aren't in the DOM |
