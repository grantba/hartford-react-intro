# React Performance

Two easy ways to improve performance in a React app are the `useMemo` and `useCallback` hooks.

## `useMemo`

The `useMemo` hook caches values so that once they're only calculated the first time.

```js
import { useMemo } from "react"

function FilteredMovieList({ allMovies, searchTerm }){
  const filteredMovies = useMemo(() => {
    return allMovies.filter(movie => movie.name.includes(searchTerm))
  }, [allMovies, searchTerm])

  return (
    <div className="MovieList">
      {filteredMovies.map(movie => (
        <li key={movie.id}>{movie.name}</li>
      ))}
    </div>
  )
}

export default FilteredMovieList
```

## `useCallback`

`useCallback` is the same as `useMemo`, but works with functions instead of values.

```js
import { useCallback } from "react"

function FilteredMovieList({ allMovies, searchTerm }){
  const filterMovies = useCallback(movie => movie.name.includes(searchTerm), [allMovies, searchTerm])
  const filteredMovies = allMovies.filter(filterMovies)

  return (
    <div className="MovieList">
      {filteredMovies.map(movie => (
        <li key={movie.id}>{movie.name}</li>
      ))}
    </div>
  )
}

export default FilteredMovieList
```

## Preserving Part of a Complex Object

```ts
setSomeState(previousState => {
  return {
    ...previousState,
    someProperty: "Only value that will be updated",
  }
})
```

## Watch Out!

* To know where these optimizations are helping or hurting, you need to measure them.
* `useMemo` only makes sense if the data is deterministic.
* You can only cache expensive calculations with with `useMemo`, not `useCallback`

## Additional Resources

| Resource | Description |
| --- | --- |
| [Kent C. Dodds: When to use `useMemo` and `useCallback`](https://kentcdodds.com/blog/usememo-and-usecallback) | Blog post on the dangers of premature optimization |
