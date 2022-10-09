# Testing React Context

To test a component that consumes a context, wrap the component being tested in a context provider when it's rendered:

```jsx
import SomeContext from "./some-context"
import ComponentBeingTested from "./ComponentBeingTested.js"

test("Something", () => {
  render(
    <SomeContext.Provider value="Hi">
      <ComponentBeingTested />
    </SomeContext.Provider>
  )
})
```

If the `ComponentBeingTested` uses the `useContext` hook with `SomeContext`, it will have access to `"Hi"` since the context provider is its tree.
