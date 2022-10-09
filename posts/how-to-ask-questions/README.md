# How to Ask Questions

Asking technical questions can be difficult. Often, you don't know even know enough to put a decent question together! Here are some guidelines:

## Include The Context

These are good examples of context:

* "I'm working on the 'Implement Wireframe' exercise, and..."
* "I'm building an API with Express, and have 3 routes: `GET /`, `GET /:id`, and `POST /`."
* "I'm trying to scaffold a React app using `create-react-app`."

A lot of questions have different or even opposite answers in different contexts. Also, sometimes the context alone is enough for someone to have a good guess at what your question is.

## Describe What's Happening

There are a couple of parts to this:

* What you're doing
* What happens when you do that
* What you think should be happening when you do that

For example:

* "Every time I submit a form, it refreshes the page. I would expect it to submit the form and redirect to my confirmation screen."
* "When I start my server, I get an error saying that it `Cannot GET /`. I would expect it to show my `index.html` page."
* "When I click on the button, nothing happens and I get error in the console saying: `Reason: CORS header 'Access-Control-Allow-Origin' missing`

Make sure you look for any errors in the console or logs and include them in your description.

## Describe What You've Tried

Before you ask someone else for help, try to help yourself first. There are very few problems a new developer can have that haven't been had by thousands of other developers. Your best resources are search engines and [Stack Overflow](https://stackoverflow.com/). Get used to looking through a wide variety of answers in a short period of time.

If you're not able to find an answer, describe why:

* "When I tried looking up the error code, all I could find were server examples but my error is on the client."
* "I tried comparing it to the example, but the underlying data is so different I couldn't recreate the problem."
* "This example does what I want to do, but I can't tell what's different about what I'm doing."

## Include Stripped-Down Examples

A huge part of troubleshooting is isolating the problem. For example:

* If you're having trouble serving an `index.html` file, what happens if you strip out all of the content?
* If a function isn't returning what you think it should, what happens if you get rid of everything but that one function and it's invocation?
* If a style isn't doing what you think it should, can you delete any extraneous HTML and CSS?

A lot of the time, that will be enough to make the solution clear to you on its own. If not, it will make it much easier for someone else to troubleshoot. It's a lot easier to spot an error in 4 lines of code than it is to understand all of someone else's app before narrowing it down. It's especially help to include links to a [sandbox](https://codesandbox.io) that troubleshooters can use.

## Keep It Concise

"Concise" doesn't necessarily mean "short"; rather, it means that doesn't include unnecessary details. Every extraneous story or detail makes it harder to find the relevant information.

## Things to Avoid

* **Vagueness**: "It's broken." If people have to pull the details of the problem out of you, they're less likely to help.
* **Complaining**: "This stupid thing isn't stupid working!" This does not entice someone to want to help you.
* **Overconfidence**: "That can't be it, I already tried that.". Technical troubleshooting involves doing a lot of things in a very precise order. Just because you did something once doesn't mean that you did it at the correct time or in the correct place.

## A Complete Example

> "I'm working on building a new Rails API. Whenever I try to post data to any endpoint, I get an error saying `ActionController::RoutingError: No route matches` and the data isn't added. I tried working through [these steps](#), but I got stuck on step 4 because I don't know how to "`byebug`" something. I've recreated the problem [here](#)."
