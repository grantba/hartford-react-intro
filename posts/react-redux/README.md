# Redux

## Installing

With Create React App:

```bash
npx create-react-app my-app --template redux
```

In an existing React app:

```bash
npm install @reduxjs/toolkit
```

## Setup

Create a store, passing in a root reducer. This is run once to determine the initial state of the app.

```js
// app/store.js
import { configureStore } from "@reduxjs/toolkit"
import somethingReducer from "../features/something/somethingSlice"
import anotherThingReducer from "../features/something/anotherThingSlice"
import { apiSlice } from "../features/api/apiSlice"

export default configureStore({
  reducer: {
    something: somethingReducer,
    anotherThing: anotherThingReducer,
    [apiSlice.reducerPath]: apiSlice.reducer,
  },
  middleware: getDefaultMiddleware => getDefaultMiddleware().concat(apiSlice.middleware),
})
```

Import the store and the Provider component and wrap the app with it.

```js
// index.js
// Other imports
import { Provider } from "react-redux"
import store from "./app/store"

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
)
```

## Vocab

* **Action**: An object with a `type` and an optional `payload`
* **Action Creator**: A function that returns an action, used to prevent having to write every action by hand
* **Reducer**: A function that takes the state of the app and an action object and returns a new state
* **Root Reducer**: A function that runs once to determine the initial state of the app
* **Slice**: Reducer logic and actions for a single feature

## Slices

```js
import { createSlice } from "@reduxjs/toolkit"

const incrementAsync = createAsyncThunk("something/incrementAsync", async(somePayload) => {
  return await somePayload
})

export const somethingSlice = createSlice({
  name: "something",
  initialState: {
    someState: 1,
  },
  reducers: {
    increment: (state, action) => {
      state.someState = state.someState + action.payload
    },
    incrementAsync: (state, action) => {
      state.someState = state.someState + action.payload
    },
  },
  extraReducers: {
    [incrementAsync.fulfilled]: (state, action) => {
      state.someState += action.payload
    },
  },
})

export const { increment } = somethingSlice.actions
export default somethingSlice.reducer
```

## RTK

* `configureStore()`
* `createReducer()`
* `createSlice()`
* `createAsyncThunk()`
* `createSelector()`
* `createAction()`
* `createApi()`
* `fetchBaseQuery()`
* `<ApiProvider />`
* `<Provider>`
* `createEntityAdapter()`
* `setupListeners()`

```js

```

## APIs

```js
import { createApi, fetchBaseQuery } from "@reduxjs/toolkit/query/react"

export const apiSlice = createApi({
  reducerPath: "api",
  baseQuery: fetchBaseQuery({
    baseUrl: "https://some-api.com/api"
  }),
  endpoints: build => {
    getPosts: builder.query({
      query: () => "/posts",
      providesTags: ["Post"],
    }),
    getPost: builder.query({
      query: id => `/posts/${id}`,
    }),
    addPost: builder.mutation({
      query: post => ({
        url: "/url",
        method: "POST",
        body: post,
      }),
      invalidatesTags: ["Post"],
    })
  },
})

export const { useGetPostsQuery, useGetPostQuery, useAddPostMutation } = apiSlice
```

## Interacting With The Store

```js
import { useSelector, useDispatch } from "@reduxjs/toolkit"
import { increment } from "./someSlice"
import { useGetPostsQuery, useAddPostMutation } from "../api/apiSlice"

export default function SomeComponent(){
  const someState = useSelector(state => state.something.someState)
  const dispatch = useDispatch()
  const {
    data: posts,
    isLoading,
    isSuccess,
    isError,
    error,
  } = useGetPostsQuery()
  const [addNewPost, { isLoading }] = useAddPostMutation()

  return (
    <>
      <div>{ someState }</div>
      <button onClick={() => dispatch(increment(1))}></button>
    </>
  )
}
```

## What Goes In Redux

* Do other parts of the application care about this data?
* Do you need to be able to create further derived data based on this original data?
* Is the same data being used to drive multiple components?
* Is there value to you in being able to restore this state to a given point in time (ie, time travel debugging)?
* Do you want to cache the data (ie, use what's in state if it's already there instead of re-requesting it)?
* Do you want to keep this data consistent while hot-reloading UI components (which may lose their internal state when swapped)?

## Watch Out!

* You can write mutating logic inside a redux toolkit reducer. This is because RTK wraps a library called `immer` that makes copies of your state that you're working on.
* Redux Query errors need to be unwrapped for `try`/`catch` to work
