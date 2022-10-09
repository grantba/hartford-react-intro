# Intro to React Context

React's Context API is a tool for tunneling state from one part of an app to another. For example, you can track a logged-in user in the `App` component, and then use a Context Provider and the `useContext` hook to send it to other components. For example, in an app that has a header bar with a user profile in it, you can store the data in the `<App />` component and tunnel it to the `<UserProfile />` component without needing to go through the `<HeaderBar />` component.

```jsx
import { createContext, useState } from "react"
import Avatar from "../assets/miles.jpg"

export const UserContext = createContext()

export const UserContextProvider = ({ children }) => {
  const [currentUser, setCurrentUser] = useState({
    name: "Miles Davis",
    imageUrl: Avatar,
  })

  return (
    <UserContext.Provider value={{ currentUser, setCurrentUser }}>
      {children}
    </UserContext.Provider>
  )
}
```

1. A new `UserContext` object is created, as well as exported
2. Some state is declared to track the current user
3. A `UserContext` Provider is wrapped around any children that are given to this component, which makes any of those children able to access this state

```jsx
import { UserContextProvider } from "./contexts/user-context"
import HeaderBar from "./components/HeaderBar"
import "./App.css"

const App = () => {

  return (
    <div className="App">
      <UserContextProvider>
        <HeaderBar />
      </UserContextProvider>
    </div>
  )
}

export default App
```

The context provider component wraps the `<HeaderBar />` component and all its children.

```jsx
import NavBar from "./NavBar"
import UserProfile from "./UserProfile"
import "./HeaderBar.css"

const HeaderBar = () => {
  return (
    <header className="HeaderBar">
      <h1>Star Lucky Coffee</h1>
      <NavBar />
      <UserProfile />
    </header>
  )
}

export default HeaderBar
```

The `<HeaderBar />` component is not given anything as props.

```jsx
import { useContext } from "react"
import { UserContext } from "../contexts/user-context"
import "./UserProfile.css"
import avatar from "../assets/miles.jpg"

const UserProfile = () => {
  const { currentUser, setCurrentUser } = useContext(UserContext)
  const handleLogout = () => setCurrentUser(null)
  const handleLogin = () => setCurrentUser({
    name: "Miles Davis",
    imageUrl: avatar,
  })

  return (
    <div className="UserProfile">
      {
        currentUser
          ? (
            <>
              <img src={currentUser.imageUrl} alt={`Avatar of ${currentUser.name}`} />
              <button onClick={handleLogout}>Logout</button>
            </>
          )
          : <button onClick={handleLogin}>Login</button>
      }
    </div>
  )
}

export default UserProfile
```

[Play with this code](https://codesandbox.io/s/sad-neumann-rgm1k)

A child of `<HeaderBar />` can import the original context object, pass it into the `useContext` hook, and access anything in the `value` the provider was given. It bypassed the hierarchy entirely, tunneling the state from the context provider to the context consumer.

---

Some key concepts with React Context:

* React Context is not itself a tool for state management; React already has `useState` for that. Rather, Context is a tool for making that state easily available throughout the app.
* The Context provider's `value` property determines what will be available to child components. It can contain anything from a static value to a complex object.
* An app can have an arbitrary number of Context objects and Context providers.
* The Context object itself can be thought of as a reference that connects a `useContext` hook to a specific Context provider.

## Additional Resources

| Resource | Description |
| --- | --- |
| [React: Context](https://reactwithhooks.netlify.app/docs/context.html) | React's complete guide to Context |
| [React Context: Updating state from a nested component](https://reactwithhooks.netlify.app/docs/context.html#updating-context-from-a-nested-component) | Official guide to updating state from a nested component |
| [Video: React State Management Tutorial](https://www.youtube.com/watch?v=35lXWvCuM8o) | Dev Ed's tutorial on the context API |
