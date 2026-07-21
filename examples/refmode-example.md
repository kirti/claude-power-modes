# Example: REFMODE

**Input** — a working but tangled function:

```js
function proc(d) {
  let r = [];
  for (let i = 0; i < d.length; i++) {
    if (d[i].status == 'active') {
      if (d[i].type == 'premium') {
        r.push({ id: d[i].id, name: d[i].name, tier: 'P', val: d[i].price * 1.2 });
      } else {
        r.push({ id: d[i].id, name: d[i].name, tier: 'S', val: d[i].price });
      }
    }
  }
  return r;
}
```

**Prompt used:**
```
REFMODE on this function.
```

**Output:**

```js
function getActiveAccountSummaries(accounts) {
  return accounts
    .filter(isActive)
    .map(toAccountSummary);
}

function isActive(account) {
  return account.status === 'active';
}

function toAccountSummary(account) {
  const isPremium = account.type === 'premium';
  return {
    id: account.id,
    name: account.name,
    tier: isPremium ? 'P' : 'S',
    val: isPremium ? account.price * 1.2 : account.price,
  };
}
```

> Changes made (no behavior change):
> - Renamed `proc`/`d`/`r` to names that describe what they hold — readability without a diff in logic.
> - Split filtering (`isActive`) and transformation (`toAccountSummary`) into named functions — each is independently testable and the top-level function reads as a sentence.
> - Replaced the nested `if`/`else` with a ternary inside the mapper — same branching, less visual nesting.
> - Switched `==` to `===` — stricter equality, matches existing comparison intent, no behavior change for the string comparisons used here.

---

Note what `REFMODE` does *not* do: it doesn't add error handling, doesn't change the output shape, and doesn't "improve" the logic — because the instruction explicitly scopes it to maintainability only, with zero behavior changes. That's the point of naming the mode instead of just saying "clean this up," which often produces a much larger, riskier diff.
