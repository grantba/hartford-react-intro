# Testing User Actions with Jest

To take actions on an app, use the `userEvent` library:

## Installation

```bash
npm install --save-dev @testing-library/user-event
```

Once installed, each action can be imported from `@testing-library/user-event`:

```js
import {
  click,
  type,
} from "@testing-library/user-event"
```

## Events

### Form Events

| Action | Notes |
| --- | --- |
| `type(inputElement, text)` | The text can also a variety special characters to represent keys that can't be displayed, like enter. Accepts an options object as a third argument that can be used to add time between keystrokes. |
| `upload(inputElement, file)` |  Mock files can be created using the `File` API |
| `clear(inputElement)` | Removes the contents of an `<input />` or `<textarea>` |
| `selectOptions(selectElement, values)` | Given an array of string values, selects each matching option from a `<select>` element |
| `deselectOptions(selectElement, values)` | Given an array of string values, deselects each matching option from a `<select>` element |

### Other Events

| Action | Notes |
| --- | --- |
| `click(element)` | Clicks the element |
| `dblClick(element)` | Double clicks the element |
| `keyboard(text)` | Enters characters without first focusing an element |
| `tab()` | Simulates pressing the tab key without focusing an element first. Take options object as an argument. In the object, `shift` is a boolean for whether the shift key should be held to reverse tab order, `focusTrap` is an element that tabbing should be restricted to. |

## Special Typing Characters

Add these to text strings to simulate pressing the keys:

* `{enter}`
* `{esc}`
* `{backspace}`
* `{del}`
* `{arrowup}`, `{arrowright}``{arrowdown}``{arrowleft}`

You can also use modifiers. These will stay "held down" until explicitly released:

* `{shift}`
* `{control}`
* `{alt}`
* `{meta}`
* `{capslock}`

To release a modifier, but a slash in the first position (eg. `{/shift}, `{/control}`)

```js
const input = screen.getByRole("textinput")
type(input, "{shift}{arrowright}{arrowright}{/shift}{del}")
```

## Watch Out!

* You can't use `{shift}` and `{/shift}` to capitalize characters, just type the actual character case you want to use
* Adding delays to typing makes the action async
* There's a built-in DOM event library in `js-dom` called `fireEvent`. It works like this:

```js
fireEvent.click(someElement, eventDetails)
```

This requires very low-level mocking that gets dangerously close to reimplementing browser functionality. `userEvent` should be preferred for app testing.

## Additional Resources

| Resource | Description |
| --- | --- |
| [User Event](https://testing-library.com/docs/ecosystem-user-event/) | Official User Event docs |
| [Special Characters](https://testing-library.com/docs/ecosystem-user-event/#specialchars) | A list of all of the special characters that can be typed with User Event |
| [MDN: File](https://developer.mozilla.org/en-US/docs/Web/API/File/File) | Documentation on the `File` API |
