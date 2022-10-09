# React: Iteration

Iteration in JSX templates is done with mapping. For example:

```jsx
const SomeList = () => {
  const list = [{
    id: 1,
    content: "A",
  },{
    id: 2,
    content: "B",
  },{
    id: 3,
    content: "C",
  }]

  const items = list.map(item => {
    return <li key={ item.id }>{ item.content }</li>
  })

  return <ul>{ items }</ul>
}
```

This produces the following HTML:

```html
<ul>
  <li>A</li>
  <li>B</li>
  <li>C</li>
</ul>
```

[Play with this code](https://codesandbox.io/s/loving-carson-uthpx)

## Keys

When iteratively generating JSX elements, each one is expected to have a unique `key` attribute, which React uses for several internal reasons. Keys can be any value as long as they're unique, but are most often ids generated by a database:

```jsx
const items = list.map(item => {
  return <li key={ item.id }>{ item.content }</li>
})
```

If some other value in each item is unique (such as an employee ID), you can use that instead.

## Watch Out!

Array indexes are not suitable for the `key` attribute because they can change. For example, if an array is sorted, elements will potentially have new indexes.

## Additional Resources

| Resource | Description |
| --- | --- |
| [React: Lists and Keys](https://reactwithhooks.netlify.app/docs/lists-and-keys.html) | React's guide to iteration |
| [Video: Loop with Map](https://www.youtube.com/watch?v=9U3IhLAnSxM&t=5951s) | React Hooks Crash Course: Iteration |
| [Video: The `key` Prop](https://www.youtube.com/watch?v=9U3IhLAnSxM&t=6354s) | React Hooks Crash Course: Keys |