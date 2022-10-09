# Modern JavaScript

## Functions

All of these are equivalent:

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

There are some slight differences between, but in Vue, these two rules will serve you well:

**At the component level, use method shorthand**

This goes for `data()` as well as all computed properties and methods:

```js
export default {
  data() {
  },
  computed: {
    someComputedProperty() {
    },
    anotherComputedProperty() {
    },
  },
  methods: {
    someMethod() {
    },
    anotherMethod() {
    },
  },
}
```

**Within those methods, use arrow functions**

```js
export default {
  computed: {
    someComputedProperty() {
      return this.someState.map(item => item * 2)
    },
  },
  methods: {
    someMethod() {
      return this.someState.forEach(item => {
        console.log(item)
      })
    },
  },
}
```

This keep the `this` binding consistent so that you can keep accessing other methods and computed properties.

## Variable Scoping

Once upon a time, you declared variables in JS like so:

```js
var someVariable = "some value"
```

RIP `var`. `var` was scoped to the function, while its successors (`let` and `const`) are scoped to the block. `const` can't be reassigned (but objects and arrays can still be mutated), `let` can be reassigned.

```js
const someVariable = "some value"
someVariable = "reassigning the value" // error

let anotherVariable = "some value"
anotherVariable = "reassigning the value" // fine

const someArrayOrObject = []
someArrayOrObject.push("New element") // fine
```

Default to using `const`. If you want to reassign something at some point, you can always switch it to a `let.` On the other hand, if you default to `let` and _don't_ want an assignment, you won't get an error if an assignment happens anyway.

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

## Template Strings

RIP string concatenation. Previously, you would put JS expressions in strings like this:

```js
const someString = "The highest number in this list is " + Math.max(list) + ", woah!"
```

Never again. Now you can use backticks (```) and interpolation (`${}`) to do them inline:

```js
const someString = `The highest number in this list is ${Math.max(list)}, woah!`
```

You can put any valid JS expression inside the interpolation.

## Spreading

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

## Modules

JavaScript has modules now!

```js
// some-module.js
function someFunction(){
}
function anotherFunction(){
}

export {
  someFunction,
  anotherFunction,
}

// another-module.js
import { someFunction, anotherFunction } from "./some-module.js"
```

In Vue, you'll mostly work with "default" imports and exports where files only export and import one thing:

```vue
// SomeComponent.vue
<script>
export default {
  name: "SomeComponent",
}
</script>

// AnotherComponent.vue
<script>
import SomeComponent from "./SomeComponent.vue"

export default {
  name: "AnotherComponent",
  components: {
    SomeComponent, // Also uses object shorthand!
  },
}
</script>
```

## Fetch and Promises

JS has a massive improvement to XHR for making asynchronous HTTP requests called `fetch`. It works like this:

```js
fetch("https://pokeapi.co/api/v2/pokemon")
  .then(response => response.json())
  .then(response => {
    console.log(response.results)
  }).catch(error => {
    console.error(error.message)
  })
```

Calls to `fetch()` return Promises. Promises represent "eventual values". Since JavaScript is non-blocking, you need to explicitly handle the parts of your app that are asynchronous. If you didn't, the entire UI would lock while you're waiting for the request to come back! The syntax works like this:

```js
somethingThatReturnsAPromise()
  .then(aFunctionThatWillBeCalledWithTheResult)
  .then(aFunctionThatWillBeCalledWithTheReturnValueOfTheLastFunction)
  .then(youCanKeepChainingAsMuchAsYouWant)
  .catch(aFunctionThatWillBeCalledIfAnyErrorsHappenInTheChain)
```

`fetch` in particular resolves to a raw HTTP response. If you want to parse a JSON body into a JavaScript object, you'd do it like this:

```js
fetch(someUrl)
  .then(rawResponse => response.json())
  .then(parsedResponse => {
    // parsedResponse is the JS representation of whatever the body of the HTTP response was
  })
```

You can also configure the request by passing a configuration object to `fetch` as the second argument:

```js
fetch(someUrl, {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({ // Bodies **must** be JSONified prior to sending them, raw objects won't work!
    someKey: "some value"
  })
})
```
