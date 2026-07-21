# Example: TESTMODE

**Input** — a small utility function:

```js
function calculateDiscount(price, discountPercent) {
  if (discountPercent < 0 || discountPercent > 100) {
    throw new Error('Invalid discount percentage');
  }
  return price - (price * discountPercent / 100);
}
```

**Prompt used:**
```
TESTMODE for calculateDiscount
```

**Output:**

```js
describe('calculateDiscount', () => {
  // Happy path
  test('applies a standard discount correctly', () => {
    expect(calculateDiscount(100, 20)).toBe(80);
  });

  test('handles a 0% discount (no change)', () => {
    expect(calculateDiscount(100, 0)).toBe(100);
  });

  test('handles a 100% discount (free)', () => {
    expect(calculateDiscount(100, 100)).toBe(0);
  });

  // Edge cases
  test('handles decimal prices without rounding errors', () => {
    expect(calculateDiscount(19.99, 10)).toBeCloseTo(17.991, 3);
  });

  test('handles a very small price', () => {
    expect(calculateDiscount(0.01, 50)).toBeCloseTo(0.005, 3);
  });

  // Invalid input / failure modes
  test('throws on a negative discount percentage', () => {
    expect(() => calculateDiscount(100, -5)).toThrow('Invalid discount percentage');
  });

  test('throws on a discount percentage over 100', () => {
    expect(() => calculateDiscount(100, 150)).toThrow('Invalid discount percentage');
  });

  test('does not validate a negative price (documents current behavior)', () => {
    // Note: the function has no price validation — this test documents that gap
    // rather than assuming it's intended. Flagged for the author to confirm.
    expect(calculateDiscount(-50, 20)).toBe(-40);
  });
});
```

> Coverage priorities, per the mode's instruction: happy path (3 tests), edge cases around precision and boundary values (2 tests), and failure modes (2 tests) — plus one test that surfaces an *unhandled* edge case (negative price) rather than silently ignoring it. That last one is the kind of thing generic "write some tests" requests tend to skip, because it requires noticing what the function doesn't check, not just what it does.

---

Note the difference from a generic "write tests for this" request: `TESTMODE`'s instruction explicitly asks for tests that would *catch a real regression*, which is why the output includes a boundary-value test and a "documents current behavior" test instead of just three near-identical happy-path cases padding a coverage number.
