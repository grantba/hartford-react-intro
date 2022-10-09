# Guide to JavaScript and TypeScript If You're Coming From Another Language

JavaScript is a dynamically typed, JIT-compiled language that can either run via a browser or standalone via Node.js. It was originally designed for web page interactivity but now functions as a general-purpose language. It's the only language that runs natively in most browsers, and its exceptional support for asynchronous programming and the non-blocking nature of Node makes it a strong choice for web servers as well.

Static typing is available via TypeScript, a third-party tool maintained by Microsoft. TypeScript offers static analysis and type-safety during development but ultimately compiles to plain JavaScript that can be run in any JS environment. TypeScript is not fully sound, but the small compromises it makes in soundness allow it to infer most types automatically and several other practical benefits.

## High Level

* Syntax: C-style
* Typing: Dynamic, with static types from TypeScript. Types are generally postfixed to the value (instead of prefixed).
* Paradigm: Procedural/Functional/Object-Oriented. Functional approaches tend to be cleaner in plain JavaScript as its native Object-Oriented features are relatively weak. TypeScript adds several OO features (such as interfaces), and makes greater use of procedural control structures for things like type narrowing.
* Scoping: Block-level for all modern JavaScript

## Types

These common primitive types are built into JavaScript:

* `string`
* `boolean`
* `number` (all numbers, including floats)
* `undefined` (never had a value)
* `null` (intentionally doesn't have a value)

Most other types in JavaScript, including arrays, functions, promises, and errors are kinds of objects. All primitives are passed by value, all objects are passed by reference.

You can coerce primitives by wrapping a value in a constructor (type name PascalCased, such as `Boolean(0)`). There are also some common shorthands:

* Prefixing with `+` coerces to number, such as `+"1"`
* Prefixing with `!!` ("not-not") coerces to boolean, such as `!!1`
* Wrapping with ` ``${}`` ` coerces to string, such as ` ``${1}`` `

Objects in JavaScript are much lighter than they are in most Object-Oriented languages, functioning closer to simple key-value stores, hashes, or dictionaries. However, in JavaScript functions are first-class, which means they can be used as values in objects. Additionally, JavaScript objects support a lighter form of inheritance called prototyping.

Functions can be used as repeatable code (procedures), transforms (pure functions), and as actions on state (methods). There are several different syntaxes for functions, many of which have minor variations in behavior.

TypeScript adds a couple of utility types, namely:

* `any` - Turn off typechecking for this value (dangerous, tends to infect otherwise safe code)
* `unknown` - Top type, everything is assignable
* `void` - Used for functions that don't return anything
* `never` - Bottom type, nothing is assignable

## Don't Use These

If you've seen or written legacy JavaScript, you may have used these language features. Feel free to take them out of your vocabulary!

* **`var`**: This was the original way to declare variables. It was replaced by `const` and `let`.
* **`==`/`!=`**: These were the original boolean comparison operators, which coerced types and always worked inconsistently. They were replaced with `===` and `!==`.
* **`eval()`**: There are very few secure ways to use this
* **Function expressions**: Since functions in JavaScript are values, you can save them in variables and even write them inline. This should be done with fat arrows (eg. `[1, 2, 3].map(number => number * 2)`) rather than traditional function expressions (`[1, 2, 3].map(function(number){ return number * 2})`).

## Syntax

Review the following concise syntax examples:

* [JavaScript](https://learnxinyminutes.com/docs/javascript/)
* [TypeScript](https://learnxinyminutes.com/docs/typescript/)

## Guide

Review the appropriate [Get Started](https://www.typescriptlang.org/docs/) guide for your background.
