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

### Server-side auth in Next.js (`@supabase/ssr`, middleware, cookie sessions)
- **Topic:** Keeping the Supabase session in cookies instead of browser localStorage, so Server Components, Route Handlers and `middleware.js` can also see who is logged in. The `@supabase/ssr` package plus a `createServerClient` / `createBrowserClient` split, and a middleware that refreshes the token on every request.
- **Came up:** 2026-09-20, Week 7 kickoff (auth + RLS depth calibration).
- **Why deferred:** Week 7's deliverable is a client-side app — `"use client"` at the top of `page.js`, every query fired from the browser. A browser-only session is enough for that, and RLS (not the server) is what actually enforces privacy. Adding SSR auth now means two clients, a middleware, and cookie plumbing before the basic flow is even understood.
- **Revisit when:** a page must render already-personalised HTML on the server, or a route needs to block unauthenticated requests before any JS runs — realistically Week 9+ when an API route calls the Claude API on a logged-in user's behalf.

### Other auth methods: OAuth providers, password login, MFA
- **Topic:** `signInWithOAuth` (Google/GitHub), `signInWithPassword`, phone OTP, multi-factor auth.
- **Came up:** 2026-09-20, Week 7 kickoff.
- **Why deferred:** every one of these produces the exact same thing — a session with a `user.id` — and RLS doesn't care which one made it. Learning one login method properly beats learning four shallowly. Magic link is the one with no password reset flow to build.
- **Revisit when:** a real product has users who bounce off email links (Week 14+ paid product). Adding Google login later is a ~20-line change, not a rebuild.

### Postgres column-level privileges (`grant insert (name) on habits to authenticated`)
- **Topic:** Restricting which *columns* a role may insert/update, so the browser literally cannot send a `user_id` value — the column default is the only way it gets filled.
- **Came up:** 2026-10-04, Week 8 habits schema — "why do we even allow the user to insert into `user_id`?"
- **Why deferred:** An RLS `with check (user_id = auth.uid())` policy already makes sending `user_id` harmless (you can only send your own uuid, same result as the default). Column grants are a second permission system on top of RLS; learning both at once blurs which one is doing the protecting.
- **Revisit when:** a table has a column users must never set even to their own value (e.g. `is_admin`, `plan`, `credits_remaining`) — realistically when payments/free-tier limits arrive in Weeks 10–17.
