> Combine these arrays using spreading instead of concatenation:

```ts
const oldSubscribers = [1, 2, 3]
const newSubscribers = [4, 5, 6]
const allSubscribers = oldSubscribers.concat(newSubscribers)
```

> Append an item to this array using spread instead of `.push()`:

```ts
const oldSubscribers = [1, 2, 3]
oldSubscribers.push(4)
```

> Prepend an item to this array using spread instead of `.unshift()`

```ts
const newSubscribers = [2, 3, 4]
newSubscribers.unshift(1)
```

> Build this array using spreading instead of `.splice()`

```ts
const oldSubscribers = [1, 2]
const newSubscribers = [4, 5]
const allSubscribers = oldSubscribers.concat(newSubscribers).splice(2, 0, 3)
```

> Copy this array using spreading instead of `.slice()`

```ts
const allSubscribers = [1, 2, 3, 4, 5]
const allSubscribersCopy = allSubscribers.slice()
```

> Shallow copy this object using spreading instead of `Object.assign`

```ts
const user = {
  id: 1,
  name: "Stan Getz",
}
const userCopy = Object.assign({}, user)
```

> Add this array to this object using spread instead of `Object.assign()`:

```ts
const user = {
  id: 1,
  name: "Stan Getz",
}
const albums: ["Getz/Gilberto", "Jazz Samba", "Focus"]
const userWithAlbums = Object.assign(user, { albums })
```

> Overwrite the `name` property using spread instead of an assignment

```ts
let user = {
  id: 1,
  name: "Stan Getz",
}
user.name = "Getz, Stan"
```

> Combine these two objects using spread instead of `Object.assign`

```ts
const user = {
  id: 1,
  name: "Stan Getz",
}
const malibuResident = {
  city: "Malibu",
  state: "CA",
}
const userWithResidence = Object.assign(user, malibuResident)
```
