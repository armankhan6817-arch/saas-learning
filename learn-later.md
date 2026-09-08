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

### Private couples' app (adult content, personal use)
- **Topic:** A private app for me and my wife — browse adult GIFs filtered by mood/preference tags, pulled from an external adult API (Redgifs/Reddit). No Claude API in the loop (mood-to-tag mapping done with a hardcoded object, not an LLM). Optional better variant: a mutual-match layer where both partners answer independently and only overlaps are revealed.
- **Came up:** 2026-09-08, Week 5 Day 3, after the tone-rewriter was committed.
- **Why deferred:** Two reasons. (1) Learning value is low right now — it's fetch + render + tag filter, which is Week 3 material; the genuinely hard parts (adult API auth, rate limits, dead links) teach one vendor's API, nothing transferable. (2) Sending kink tags through the Claude API is a gray area under Anthropic's usage policies, and the account at risk is the one the whole roadmap runs on — so keep the LLM out of it entirely.
- **Revisit when:** After Week 8, as a weekend project — by then auth + Supabase + RLS are in hand, so it's two evenings instead of two weeks. The mutual-match variant is the one worth building; it's a real product shape (Kindu, Spicer) and RLS makes the privacy guarantee real.
- **Cannot become a roadmap product:** payment processors (Razorpay, Paddle, Polar, Stripe) prohibit or heavily restrict adult content, Vercel's AUP restricts it on free tiers, and it can't go in the public build-in-public portfolio.
