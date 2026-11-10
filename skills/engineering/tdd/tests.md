# Good and bad tests

Paired examples for the anti-patterns named in [SKILL.md](SKILL.md). They are written in TypeScript; the shapes apply in any language and test framework.

## Verify through the interface

```typescript
// BAD: reaches around the interface to check a side effect
test("createUser saves to database", async () => {
  await createUser({ name: "Alice" });
  const row = await db.query("SELECT * FROM users WHERE name = ?", ["Alice"]);
  expect(row).toBeDefined();
});

// GOOD: observes the behavior the way a caller would
test("a created user can be retrieved", async () => {
  const user = await createUser({ name: "Alice" });
  const retrieved = await getUser(user.id);
  expect(retrieved.name).toBe("Alice");
});
```

## Assert on outcomes

```typescript
// BAD: implementation-coupled. Passes only while checkout keeps
// calling this collaborator in this way.
test("checkout calls paymentService.process", async () => {
  const process = jest.spyOn(paymentService, "process");
  await checkout(cart, paymentMethod);
  expect(process).toHaveBeenCalledWith(cart.total);
});

// GOOD: states the capability and checks its result
test("user can checkout with a valid cart", async () => {
  const cart = createCart();
  cart.add(product);
  const result = await checkout(cart, paymentMethod);
  expect(result.status).toBe("confirmed");
});
```

Assertions on call counts or call order are the same mistake in another form.

## Take expected values from outside the code

```typescript
// BAD: tautological. The expected value is computed the way the code computes it.
test("calculateTotal sums line items", () => {
  const items = [{ price: 10 }, { price: 5 }];
  const expected = items.reduce((sum, i) => sum + i.price, 0);
  expect(calculateTotal(items)).toBe(expected);
});

// GOOD: a literal worked out by hand
test("calculateTotal sums line items", () => {
  expect(calculateTotal([{ price: 10 }, { price: 5 }])).toBe(15);
});
```

## Name the behavior, one per test

```typescript
// BAD: the name describes the mechanism, and two behaviors share one test
test("applyCoupon sets discountRate and skips expired coupons", () => {
  /* ... */
});

// GOOD: each name reads as a line of the specification
test("a 10% coupon reduces the total by 10%", () => {
  expect(applyCoupon(cartWorth(200), tenPercentCoupon).total).toBe(180);
});

test("an expired coupon leaves the total unchanged", () => {
  expect(applyCoupon(cartWorth(200), expiredCoupon).total).toBe(200);
});
```

When a test fails, its name alone should say which behavior broke.
