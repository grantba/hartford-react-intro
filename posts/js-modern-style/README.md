# Modern JavaScript Style

Since 2015, JavaScript has added several operators and features that make low-level operations more powerful and expressive.

## Spreading To Copy and Combine

You can spread arrays and objects with the `...` operator. This is the equivalent of dropping the `[]` or `{}` from the object:

```js
const oneList = [1, 2, 3]
const twoList = [4, 5, 6]
const bothLists = [...oneList, ...twoList]

const result = sum(...bothLists) // Can use to pass in an array of arguments separately

const person = {
  firstName: "Kyle",
  lastName: "Coberly",
}
const boatCaptain = {
  firstName: "Captain",
}

const captainKyle = {
  ...person,
  ...boatCaptain, // clobbers firstName: "Kyle"
  rank: "Captain",
}
```

These are handy for combining and making shallow copies of things.

## `const` and `let`

RIP `var`. `var` was scoped to the function, while its successors `let` and `const` are scoped to the block. `const` can't be reassigned (but objects and arrays can still be mutated), `let` can be reassigned.

```js
const someVariable = "some value"
someVariable = "reassigning the value" // error

let anotherVariable = "some value"
anotherVariable = "reassigning the value" // fine

const someArrayOrObject = []
someArrayOrObject.push("New element") // fine
```

Usually, there are advantages to defaulting to `const`. If you want to reassign something at some point, you can always switch it to a `let.` On the other hand, if you default to `let` and _don't_ want an assignment, you won't get an error if an assignment happens anyway.

## Object Shorthand

It's common in JS to need to assign a key in an object to a variable with the same name as the key:

```js
const user = { id: 1 }
const body = {
  user: user,
}
```

You can now condense those:

```js
const user = { id: 1 }
const body = {
  user,
}
```

## Function Syntaxes

All of these are ways to declare functions:

```js
// Functional declaration - Hoists
function someFunction(someParameter){
  return someParameter
}

// Function expression - Doesn't hoist
const someFunction = function(someParameter){
  return someParameter
}

// Arrow function - Maintains `this` binding
const someFunction = (someParameter) => {
  return someParameter
}

// One-line Arrow function - Maintains `this` binding and has an implicit return
const someFunction = someParameter => someParameter

// Multi-line Arrow function - Uses parentheses to implicitly return
const someFunction = someParameter => (
  someParameter * 2
)

// As part of an object, method shorthand
{
  someFunction(someParameter) {
    return someParameter
  }
}

// As part of an object, function expression
{
  someFunction: function(someParameter) {
    return someParameter
  }
}
```

Hoisting means that you can use a declaration before you've defined it.

```ts
someFunction() // Hoisted, fine

function someFunction(){
}

someOtherFunction() // Not hoisted, error
const someOtherFunction = function(){
}
```

## Template Literals Instead of String Concatenation

Previously, JS expressions were concatenated into strings like this:

```js
const someString = "The highest number in this list is " + Math.max(list) + ", woah!"
```

Now you can use backticks (```) and interpolation (`${}`) to do them inline:

```js
const someString = `The highest number in this list is ${Math.max(list)}, woah!`
```

You can put any valid JS expression inside the interpolation.

## Safe Method and Property Access with Optional Chaining

If any property or method is `null` or `undefined`, the entire expression evaluates to `undefined`.

```ts
const someObject = {
  a: {
    b: null
  }
}

console.log(someObject.a.b.c) // Error
console.log(someObject.a.b?.c) // `undefined`
```

Note that the operator is `?.`, not just `?`. You can also use it with bracket notation:

```ts
console.log(someObject.a.b?.["c"]) // `undefined`
```

## Short-circuit evaluation

When building a boolean expression with `&&`, the compiler will stop or "short-circuit" at the first falsy value:

```ts
const a = "a"
const b = "b"
const c = ""
const d = "d"

const result = a && b && c && d // ""
```

Note that it evaluates to the falsy value, _not_ to the boolean `false`. Similarly, `||` will evaluate to the first truthy value, not `true`:

```ts
const a = ""
const b = ""
const c = "c"
const d = ""

const result = a || b || c || d // "c"
```

`OR` short-circuiting works with _all_ falsy values (including `""`, `0`, and `false`), which is usually not what you want. To treat `""`, `0`, and `false` as truthy expressions in an `OR` chain, use the nullish coalescing operator, `??`:

```ts
const a = ""
const b = ""
const c = "c"
const d = ""

const result = a ?? b ?? c ?? d // "", value of `a`
```

## Destructuring

Individual properties can be pulled out of objects by using `{}` on the left-hand side of a variable assignment:

```ts
const { a, c } = {
  a: "a",
  b: "b",
  c: "c",
}
console.log(a, c) // "a", "c"
```

This is equivalent to doing this:

```ts
const someObject = {
  a: "a",
  b: "b",
  c: "c",
}
const a = someObject.a
const b = someObject.b

console.log(a, c) // "a", "c"
```

This also works with arrays:

```ts
const someArray = ["a", "b", "c"]
const [a, b] = someArray
console.log(a, b) // "a", "b"
```

This is equivalent to:

```ts
const someArray = ["a", "b", "c"]
const a = someArray[0]
const b = someArray[1]
console.log(a, b) // "a", "b"
```

Note that when destructuring arrays, you can't skip indexes.

## Function Defaults

```js
function showListings(listings, includeDeactivateListings = true){
  //
}
```

Only use this feature if the value is a true _default_ that is occasionally overridden, not just because a value is especially common.

## Additional Resources

| Resource | Description |
| --- | --- |
| [ES Compatibility Table](https://kangax.github.io/compat-table/es2016plus/) | Comprehensive table showing support for different JavaScript features. Use the tabs to show different eras of features. |
