Write tests for the following code without implementing the higher-order functions:

```js
function map(array, transform){
  const newArray = []

  for (let i = 0; i < array.length; i++){
    const oldElement = array[i]
    const newElement = transform(oldElement)
    newArray.push(newElement)
  }

  return newArray
}
```

```js
function filter(array, predicate){
  const newArray = []

  for (let i = 0; i < array.length; i++){
    const element = array[i]
    if (predicate(element)){
      const newElement = JSON.parse(JSON.stringify(element))
      newArray.push(newElement)
    }
  }

  return newArray
}
```

```js
function reduce(array, reducer, default){
  let accumulation = default

  for (let i = 0; i < array.length; i++){
    const element = array[i]
    accumulation = reducer(accumulation, element)
  }

  return accumulation
}
```

---

Assert that `console.log` was called with the provided string:

```js
function log(message){
  console.log(`LOG: ${message}`)
}
```

---

Assert that this function works:


```js
function someFunction(someString, somePromise){
  return somePromise.then(someValue => {
    return `${someString}: ${someValue}`
  })
}
```
