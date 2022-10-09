> Convert this function to use default parameters instead of short-circuits:

```ts
function processOrder(order, salesperson){
  salesperson = salesperson ?? "house"

  //
}
```

> Convert this unsafe short-circuit to use nullish coalescing instead of `OR`:

```ts
function deposit(customer, depositAmount){
  setDepositAmount(customer, depositAmount || 1000)
}
```

> Convert this assignment to use short-circuiting instead of conditionals

```ts
let a
if (b){
  a = b
} else {
  a = c
}
```

> Convert this operation to use short-circuiting instead of conditionals

```ts
if (a){
  b()
}
```
