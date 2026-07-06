# Mistake Log

Recurring errors and the concepts behind them. An entry gets added when the same *type* of mistake shows up a second time — so patterns are visible and can be turned into a proper rep.

Format:
- **Date:**
- **Error:** what went wrong (one line)
- **Concept:** the underlying JS concept misunderstood
- **Fix:** the correct pattern, in one or two lines

---

- **Date:** 2026-07-06
- **Error:** Used loose equality (`==` / `!=`) in the prime detector after being told to prefer strict, twice (`practice 2.html`).
- **Concept:** `==` does type coercion before comparing; `===` compares value *and* type with no conversion. Defaulting to `==` is a habit worth breaking early.
- **Fix:** Use `===` / `!==` by default. Reach for `==` only with a deliberate reason.
