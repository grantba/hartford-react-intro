# Intro to Testing

Tests verify that something does what you think it does. Some examples of tests:

* Opening an app, clicking a button, checking that the right screen loads
* Console logging that a function is getting called
* Checking that a function runs without changing another value
* Code that automates any of the above

Most developers test their code, they just do it manually and infrequently and don't keep the tests when they're done. Using dedicated testing tools helps developers write more accurate and expressive tests and gives them real-time feedback about their code.

Tests can be written at any point in the development process, but there are some distinct advantages to using tests as a design tool. This is admittedly counter-intuitive. Writing tests before you write code forces you to define the interface for the code you want to test, which naturally leads to decoupled and modular designs.

## Why Write Tests?

* **Tests create confidence**. Tests allow you to fearlessly change your code. You can delete files, rework implementations, and try alternatives and get instant feedback from your tests about what is no longer working. Without this feedback, developers become afraid to change or remove things, and even start creating duplicate implementations out a fear of breaking something.
* **Test are documentation**. Tests are executable examples of how your code works. Since it's not possible for your tests and your actual code to get out of sync, tests end up more reliable than prose documentation.
* **Tests run your code.** One of the most time-consuming parts of developing software is manually testing code as you're writing it. Tests do this automatically.

## Why Don't Developers Write Tests?

If automated tests are so valuable, why do developers resist using them?

* **Developers lack fluency with their testing tools.** A `console.log` is always going to be right there. If installing and configuring testing tools is awkward, if the developer has to look up all the syntax, if they're constantly fighting against the testing tools, they won't get used.
* **Most books, blog posts, and general advice relies too heavily on unit tests.** Unit tests are a valuable part of any testing strategy, but they're often so close to the parts of the code that change the most. This often means throwing away tests nearly as quickly as they're written, which is disheartening.
* **It's hard to know what's actually valuable to test.** The tests that are easiest to write often are the least useful. TDD in particular relies on being able to predict what you'll eventually need, which takes experience.
* **There's always more features to write.** It's easy to fall into the trap of thinking that testing slows down development. It often does... at first. As soon as the app gets too big for developers to hold in their heads at the same time, tests are the only thing that will enable speed.
* **Adding tests to legacy code is difficult**. One of the advantages of writing tests first is that it encourages writing modular, testable code. It follows that without tests, it's easy to write highly coupled code that can't be isolated for tests.
* **Developers think testing is for testers.** There's a pervasive belief that testing is a skill that requires a particular mindset that only some possess. This is untrue, any developer can learn to write great tests. Additionally, many developers feel that testing is beneath them and should be farmed out to dedicated testing teams. Remember, tests don't only verify behavior; they also run and document the code and provide real-time feedback to the developer.

## What Gets Tested?

While definitions and divisions vary between testers, these are most commonly used levels of test:

* **End-to-End (E2E)**: Sometimes called feature or UI tests, these simulate how a user uses an application. For web apps, this means opening a browser, going to a URL, clicking and typing, and asserting that things are visible on the string.
* **Integration**: These test significant pieces of your app, like features. These are generally combinations of smaller pieces of code (like units), and are tested by isolating that part of the code and asserting that they behave as expected.
* **Unit**: Unit tests are for the smallest parts of your code like functions and methods. They assert that correct values are returned or correct state changes occur under particular circumstances.
* **Static**: These are done via types. A lot of potential errors can be eliminated by limiting what types are allowed to be used in your code.

Historically, these were described as a pyramid. Unit tests are fast and specific and E2E tests are slow and general, so you were supposed to target a lot of unit tests and not as many integration or E2E tests. In modern development, the "trophy" strategy advocated by Kent C. Dodds is preferred. Trophy testing has a smaller proportion of unit and E2E tests, and primarily relies on integration tests.

At each level of test, the goal is the same: Describe how the code should work. This is often as simple as automating what you would manually do to verify that something works. For example, if you have a list of items, you may want to verify that you can add new items to it. If you were doing that manually, you might follow these steps:

1. Go to the list page
2. Verify that there are only 3 items on it
3. Click the link to add a new item
4. Fill out the form to add a new item
5. Verify that you were redirected back to the list page
6. Verify that there are 4 items on the list and the last one is the item you just entered

Written as an E2E test in Playwright, that might look like this:

```js
describe("list page", () => {
  it("adds items to an existing list", async ({ page }) => {
    await page.goto("/list")

    const items = await page.$$(".item")
    expect(items).toHaveLength(3)
    await page.click("text=New")

    await page.fill("[placeholder=New item here]", "New Item")
    await page.click("text=Add")

    expect(page.url).toContain("/list")
    const newItems = await page.$$(".item")
    expect(newItems).toHaveLength(4)
    const content = await newItems[3].textContent()
    expect(content).toBe("New Item")
  })
})
```

A supporting integration test in Jest might verify that the form can be filled out and rejects blank input:

```jsx
describe("<ItemFormNew />", () => {
  it("accepts valid input", () => {
    const submitHandler = jest.fn()
    render(<ItemFormNew submitHandler={submitHandler}>)

    const input = screen.getByLabelText("Content")
    type(input, "New Item{enter}")

    expect(submitHandler).toHaveBeenCalledWith("New Item")
  })

  it("doesn't accept blank input", () => {
    const submitHandler = jest.fn()
    render(<ItemFormNew submitHandler={submitHandler}>)

    const input = screen.getByLabelText("Content")
    type(input, "{enter}")

    expect(submitHandler).not.toHaveBeenCalled()
  })
})
```

A supporting unit test might verify that an individual item renders correctly:

```jsx
describe("<Item />", () => {
  it("renders given content", () => {
    render(<Item content="Hello, world!">)

    const content = screen.getByText("Hello, world!")

    expect(content).toBeVisible()
  })
})
```

In every case, it's also important to note what isn't tested. Don't test internal variables, class names, or anything that a consumer of the code wouldn't care about. You're testing the interface or contract of the code, **not** its implementation. You should be able to completely change an implementation, and as long as the interface is the same the test should still pass. Conversely, if the interface or behavior of the code changes, the tests should fail.

* E2E: Only test things that a user can see and interact with, and try to describe everything in terms a normal user would understand. For example, target a form input by its label or placeholder text, not its tag name or other CSS selector.
* Integration and Unit: Only test parameters, events, public methods, props, or other things a consumer of the code would work directly with. Don't test internal variables, private methods, or other implementation details.

Tests are a conversation with your code. You might not write the correct test the first time, and that's OK. Your tests should shape your code, but it's also OK for your code to influence your tests too. As long as your tests are giving you confidence, documenting how the code works, and running your code, you're writing tests correctly.

## Additional Resources

| Resource | Description |
| --- | --- |
| [Test Automation Panda](https://automationpanda.com/) | Outstanding blog full of articles on testing techniques and philosophy |
| [The Testing Trophy and Testing Classifications](https://kentcdodds.com/blog/the-testing-trophy-and-testing-classifications) | Kent C. Dodd's blog post on different types of testing. |
