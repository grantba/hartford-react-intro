# Running JavaScript Code

There are few ways to run JavaScript code:

## Node

You can also run JavaScript code on the CLI with node.

```js
function sayHelloWorld(){
  console.log("Hello, world!")
}

sayHelloWorld()
```

Try putting that code in a file called `index.js` and run `node index.js` to see its output. The `node` command takes any JavaScript file as an argument and attempts to run it.

## Browser Console

Browsers run JavaScript code natively. That means you can always pull up a developer console and start typing! Refreshing the page will clear out any saved variables.

## Node REPL

Similar to the browser console, you can open a programmer that lets you write JavaScript in place without saving it to a file first by just running `node` (no arguments). To quit, type `.exit`. You can also type `.help` to see a list of other commands you can run.

## Code Sandbox

You can also run Node code on [CodeSandbox](https://codesandbox.io). Create a new sandbox, choose the "Vanilla" template, and write your code in the `src/index.js` file. Your output will be shown in the console of the CodeSandbox browser.
