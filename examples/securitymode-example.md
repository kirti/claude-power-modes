# Example: SECURITYMODE

**Input** — a messy Express route handling login:

```js
app.post('/login', async (req, res) => {
  const { username, password } = req.body;
  const query = `SELECT * FROM users WHERE username = '${username}'`;
  const user = await db.query(query);

  if (user && user.password === password) {
    req.session.user = user;
    res.json({ success: true, token: jwt.sign({ id: user.id }, 'secret123') });
  } else {
    res.json({ success: false });
  }
});
```

**Prompt used:**
```
SECURITYMODE on this login route.
```

**Output:**

> Reviewed as a threat-focused security audit. Ranked by severity:
>
> **Critical**
> 1. **SQL injection** — `username` is interpolated directly into the query string. An attacker can pass `' OR '1'='1` to bypass authentication entirely or exfiltrate data. Fix: use parameterized queries (`db.query('SELECT * FROM users WHERE username = ?', [username])`).
> 2. **Plaintext password comparison** — `user.password === password` implies passwords are stored in plaintext. Any database leak exposes every user's real password. Fix: store bcrypt/argon2 hashes, compare with a constant-time hash comparison function.
> 3. **Hardcoded JWT secret** — `'secret123'` is committed to source. Anyone with repo access can forge valid tokens for any user. Fix: load from an environment variable, rotate it, and never commit secrets.
>
> **Medium**
> 4. **No rate limiting** — this endpoint has no protection against credential-stuffing or brute-force attempts. Fix: add rate limiting (e.g. `express-rate-limit`) keyed by IP and/or username.
> 5. **Verbose failure response** — returning a generic `{ success: false }` is fine, but confirm the response timing doesn't differ between "user not found" and "wrong password" — that timing difference is itself an information leak (user enumeration).
>
> **Low**
> 6. **No input validation** — `username`/`password` aren't validated for type or length before use, which compounds the injection risk above even after parameterizing.

---

This is what turns "please review this for security issues" (which often gets a shallow scan) into a structured, severity-ranked audit — because the mode explicitly tells Claude what categories to check and how to prioritize findings.
