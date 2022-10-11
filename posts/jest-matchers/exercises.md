Revise the following assertions to use more appropriate matchers:

```js
expect(undefined).toEqual(undefined)
```

```js
expect(!someString).toEqual(false)
```

```js
expect(!!someNumber).toEqual(true)
```

```js
const someString = "Hello, world!"
const containsHello = someString.includes("Hello")
expect(containsHello).toEqual(true)
```

```js
const someString = "Hello, world!"
const containsHello = (/hello/i).test(someString)
expect(containsHello).toEqual(true)
```

```js
const five = await Promise.resolve(5)
expect(five).toEqual(5)
```

```js
const array = [1, 2, 3]
expect(array.length).toEqual(3)
```

```js
const length = [1, 2, 3].length
expect(length).toEqual(3)
```

```js
const includesThree = [1, 2, 3].includes(3)
expect(includesThree).toEqual(true)
```

```js
const array = [{ id: 1 }, { id: 2 }, { id: 3 }]
const includesThree = array.filter(item => item.id = 3).length > 0
expect(includesThree).toEqual(true)
```

```js
const person = { id: 1, name: "Kyle" }
const hasName = person.hasOwnProperty("name")
expect(hasName).toEqual(true)
```

```js
const person = { id: 1, name: "Kyle" }
const isKyle = person.name === "Kyle"
expect(isKyle).toEqual(true)
```

```js
const includesThree = [1, 2, 3].includes(3)
expect(!includesThree).toEqual(true)
```

```js
let isError = false
try {
  await somePromise()
} catch(error){
  isError = true
}

expect(isError).toEqual(true)
```
