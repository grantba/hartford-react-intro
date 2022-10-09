# Procedural Programming with JavaScript

Programming languages use different mental models for organizing code called _paradigms_.

* In functional programming, programs are a series of inputs and outputs chained together
* In object-oriented programming, programs are a collection of nouns that communicate with each other through messages
* In procedural programming, programs are a set of instructions for the computer that start at the top and execute in order

Most programming problems have solutions in every paradigm. Some programming languages support only one paradigm, while others can be used to write code in multiple paradigms. JavaScript is a multi-paradigm language.

Procedural programming in particular is ideal for implementing algorithms and many types of puzzles. Procedural programs are known for being relatively easy to read and blazing fast to run, with the tradeoff of being difficult to extend and reuse, as well as being the easiest to create difficult to diagnose errors in. These are characteristics of JavaScript written in procedural style:

## Variables

Normally in JavaScript, `const` is preferable to `let`. If a value shouldn't be reassigned, `const` will help us by throwing an error. If a value should be reassigned, you can change it `let`. If you transform a piece of data, the transformed data should get its own variables.

In procedural programming, reusing variables is more common. Many low-level operations, such as updating the current item or index in a loop even require reusing variables. As such, `let` is more commonly used in procedural programs.

It's also common to see variable declarations chained:

```js
// Instead of this:
let a = 1;
let b = 2;
let c = 3;

// Chain them into one statement:
let a = 1, b = 2, c = 3;
```

## Procedures

A function takes an input and uses it to generate an output:

```js
function double(number){
  return number * 2;
}
const someNumber = double(3) // 6
```

In contrast, a procedure is just a collection of statements that want to be able to call anytime you want:

```js
let someNumber = 3;
function double(){
  someNumber = someNumber * 2 // Could also have been written `someNumber *= 2;`
}

double()
console.log(someNumber) // 6
double()
console.log(someNumber) // 12
```

Procedures can accept inputs, but usually don't return values. Instead, they mutate other values.

## Increment / Decrement

The increment (`++`) and decrement (`--`) operators are more common in procedural programming than their long-hand equivalents:

```js
let a = 0;

// Instead of this:
a = a + 1; // a is 1 now
a = a - 1; // a is 0 now

// Do this:
a++; // a is 1 now
a--; // a is 0 now
```

Be careful using these operators. They don't just evaluate to a value with the new number, they actually change the stored number too.

## Loop Control Structures

The most common procedural looping structures are `for` and `while`.

### `for`

```js
let people = ["Alice", "Bob", "Carol"];
for (let i = 0, length = people.length; i < length; i++){
  console.log(people[i])
} // Logs "Alice", "Bob", then "Carol"
```

A `for` loop has 3 parts:

* **Initialization**: This statement runs once at the beginning of the loop.
* **Condition**: This is a boolean expression that is evaluated before every loop. If it's truthy the block executes, if it's falsy the loop ends.
* **Update**: This runs at the end of every block before the condition is checked again. It usually changes something that's part of the condition to get it closer to being false.

It's really easy to write a `for` loop incorrectly:

![Places that mistakes can hide in a `for` loop ](https://ik.imagekit.io/sikaeducation/procedural-programming/bad-for-loop_u_UNegfQJ.png?ik-sdk-version=javascript-1.4.3&updatedAt=1647926957353&fr=w-1000)

In particular, make sure that the operators in the condition are correct (eg. `<` isn't mixed up with `>` or `<=`) and that the update gets the condition closer to being false. Otherwise, you may create an infinite loop that never resolves.

Most `for` loops initialize a counter to `0` and a length to the size of an array, check that the counter is less than the length, and increment the counter after every run. The power of `for` loops is that they can do other things, such as looping backward through an array:

```js
let people = ["Alice", "Bob", "Carol"];
for (let i = people.length - 1; i >= 0; i--){
  console.log(people[i])
} // Logs "Carol", "Bob", then "Alice"
```

Compare this to the first `for` loop, paying attention to the differences in each of the 3 parts of the `for` loop.

### `while`

`while` is the most fundamental looping structure. It checks a condition, executes a block of code if it's truthy, and repeat this until the condition is falsy.

```js
let count = 1;
while (count <= 3){
  console.log(`The current count is ${count}`)
  count += 1;
}
```

It's **critical** that something happen in the block that could cause the condition to be false. Otherwise, it will never stop running; this is called an _infinite loop_. You'll know this happens when your computer becomes unresponsive and all of your computer's fans turn on to try to cool down your processor while it works as fast as it can to process a loop that will never complete.

You can recreate any other kind of loop with a while loop. For example, this code doubles every number in an array:

```js
let numbers = [1, 2, 3];
console.log(numbers) // [1, 2, 3]

let currentIndex = 0;
while (currentIndex < numbers.length){
  numbers[currentIndex] = numbers[currentIndex] * 2;
  currentIndex++;
}

console.log(numbers) // [2, 4, 6]
```

The equivalent `for` loop would be:

```js
let numbers = [1, 2, 3];
console.log(numbers) // [1, 2, 3]

for (let i = 0, length = numbers.length; i < length; i++){
  numbers[i] = numbers[i] * 2;
}

console.log(numbers) // [2, 4, 6]
```

The equivalent `.map()` would be:

```js
let numbers = [1, 2, 3];
console.log(numbers) // [1, 2, 3]

const doubledNumbers = numbers.map(number => number * 2)

console.log(doubledNumbers) // [2, 4, 6]
```

## Skipping and Exiting

To skip the rest of the block in any looping structure, use a `continue` statement:

```js
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
for (let i = 0, length = numbers.length; i < length; i++){
  if (numbers[i] % 2 === 0) {
    continue;
  }
  console.log(numbers[i])
} // Will log "1", "3", "5", "7", "9"
```

To exit a loop entirely, use a `break` statement:

```js
let people = ["Alice", "Bob", "Carol"]
let foundPerson;
for (let i = 0, length = people.length; i < length; i++){
  if (people[i] === "Bob") {
    foundPerson = people[i];
    break;
  }
}
console.log(foundPerson) // "Bob"
```

You can use these to make your loops more efficient by keeping them executing a block if you don't need to.

## Conditional Control Structures

The procedural control structures in JavaScript are `if`/`else if`/`else` and `switch`:

```js
if (a === true){
  console.log("It was A!")
} else if (b === true) {
  console.log("It was B!")
} else {
  console.log("I'm not sure what it was.")
}

switch (c){
  case "1":
    console.log("C was 1");
    break;
  case "2":
    console.log("C was 2");
    break;
  default:
    console.log("I'm not sure what C was.");
}
```

`if` statements are most commonly used for branching logic. `switch` is usually used to branch logic if a single expression could be one of multiple values.

## Additional Resources

| Resource | Description |
| --- | --- |
| [MDN: Loops and Iteration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration) | MDN's guide to all the looping control structures in JavaScript |
| [MDN: Making Decisions In Your Code](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/conditionals) | MDN's guide to conditionals |
| [Functional, Object-Oriented, and Procedural Programming](https://levelup.gitconnected.com/functional-object-oriented-procedural-programming-644feda5bcfc) | Blog post constrasting procedural, functional, and object-oriented code |
