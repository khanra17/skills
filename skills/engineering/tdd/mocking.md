# Mocking

Substitute only at **system boundaries**: the points where the code leaves what this project controls. Everything on the project's side of a boundary runs for real in tests, including its own modules and internal collaborators.

| Boundary | In tests |
| --- | --- |
| Third-party APIs (payment, email) | A fake adapter, passed in |
| Time and randomness | An injected clock; a seeded generator |
| Database | A real local instance or in-memory equivalent; a fake only when neither exists |
| Filesystem | A temporary directory |

Examples are TypeScript; the shapes apply in any language.

## Prefer a fake to a mock

A **fake** is a small working implementation of the boundary. A **mock** is a script of expected calls. A fake lets the test assert on outcomes; a mock pulls the test toward asserting on calls, which couples it to the implementation.

```typescript
// Fake: behaves like the real thing, in memory
function fakePaymentClient() {
  const charges: number[] = [];
  return {
    charge: async (amount: number) => {
      charges.push(amount);
      return { status: "succeeded" };
    },
    charges,
  };
}

test("checkout charges the cart total", async () => {
  const payments = fakePaymentClient();
  await checkout(cartWorth(40), payments);
  expect(payments.charges).toEqual([40]);
});
```

## Pass the boundary in

A dependency the code constructs for itself cannot be substituted. Accept it as a parameter.

```typescript
// Substitutable
function processPayment(order, paymentClient) {
  return paymentClient.charge(order.total);
}

// Not substitutable
function processPayment(order) {
  const client = new StripeClient(process.env.STRIPE_KEY);
  return client.charge(order.total);
}
```

## One function per external operation

Shape the boundary as specific operations, each returning one shape. A single generic fetcher forces every fake to re-implement routing logic.

```typescript
// GOOD: each operation is faked independently
const api = {
  getUser: (id) => fetch(`/users/${id}`),
  getOrders: (userId) => fetch(`/users/${userId}/orders`),
  createOrder: (data) => fetch("/orders", { method: "POST", body: data }),
};

// BAD: the fake has to branch on endpoint and options
const api = {
  fetch: (endpoint, options) => fetch(endpoint, options),
};
```
