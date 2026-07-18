# Learn Later — Parking Lot

Topics that came up while building but are **out of scope for the current week**. Filed here so they're not lost, and not a distraction. Claude appends to this automatically whenever a "Skim / ignore for now / learn later" item comes up during a session.

Format per entry:
- **Topic** — what it is, in one line
- **Came up:** date + where (which exercise/context)
- **Why deferred:** why it's not needed yet
- **Revisit when:** the phase/point where it becomes relevant

---

### Prime detection — only check divisors up to √n
- **Topic:** To test if a number `n` is prime, you only need to check divisors from 2 up to the square root of `n`, not all the way to `n-1`. Makes the check much faster for large numbers.
- **Came up:** 2026-07-05, prime-number detector (`practice 2.html`), Week 1 loops practice.
- **Why deferred:** the brute-force version (checking every divisor up to `i-1`) is correct and fine for learning loops. The optimization is about efficiency, not correctness — not a Week 1 concern.
- **Revisit when:** later, once loops/logic are second nature — or whenever performance actually matters on a real project. Involves `Math.sqrt()`.

### DOM geometry & advanced events (skipped for the to-do app)
- **Topic:** Element size/scrolling, window sizes, coordinates (the DOM "geometry" sections), plus dispatching custom events, and the deep details of event bubbling/capturing.
- **Came up:** 2026-07-14, Week 2 DOM reading plan.
- **Why deferred:** the to-do app only needs `querySelector`, modifying the DOM (`createElement`/`append`/`remove`/`textContent`), `classList`, and `addEventListener`. Geometry/coordinates are for drag-drop, positioning, infinite scroll — none of which apply yet.
- **Revisit when:** a real project needs positioning/measuring elements (custom dropdowns, drag-drop, sticky/scroll effects) or custom event systems.
