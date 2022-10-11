For the following test cases, organize them using nesting and `before` handlers

```js
test("Delivery estimate is calculated when user is in the delivery zone and has an account in good standing", ({ page }) => {
  page.goto("/delivery")
  const customer = getCustomer("good", "90210")
  const store = getStore("90210")

  expect(getDeliveryEstimate(customer, store)).toBeTruthy()
})
test("Delivery estimate is not calculated when user isn't in the delivery zone but has an account in good standing", () => {
  page.goto("/delivery")
  const customer = getCustomer("good", "10000")
  const store = getStore("10000")

  expect(getDeliveryEstimate(customer, store)).not.toThrow()
})
test("Delivery estimate is not calculated when user is in the delivery zone but the account isn't in good standing", () => {
  page.goto("/delivery")
  const customer = getCustomer("bad", 90210)
  const store = getStore("90210")

  expect(getDeliveryEstimate(customer, store)).not.toThrow()
})
```
