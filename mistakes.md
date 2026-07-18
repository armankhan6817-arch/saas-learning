# Mistake Log

Errors made and doubts raised while learning, logged as they happen — a concise record for future relearning. (Broadened 2026-07-18 from "only repeat mistakes" to "log errors and notable doubts as they come up," at Armaan's request.)

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

- **Date:** 2026-07-18
- **Error:** Called `list.innerHTML("<li>...</li>")` with parentheses; browser said "innerHTML is not a function" (`testing the week 2.html`).
- **Concept:** Property vs method. `innerHTML`/`textContent`/`value` are **properties** — set with `=`, no `()`. Methods like `.append()`/`.push()` are **called** with `()`.
- **Fix:** `element.innerHTML = "..."` (assign), not `element.innerHTML("...")`.

- **Date:** 2026-07-18
- **Error:** Put `document.createElement("li")` *outside* the click handler, so every click reused the same one `<li>` instead of adding new ones.
- **Concept:** Code outside the handler runs once (at page load); code that must happen on every click belongs inside the handler. Appending an element that's already on the page moves it, doesn't duplicate it.
- **Fix:** Create the fresh element **inside** the handler so a new one is made per click.

- **Date:** 2026-07-18
- **Doubt/Error:** Confused `element.value` with `string.value` — tried `taskValue.value = ""` and `document.querySelector("#task") = ""` to clear the input.
- **Concept:** `.value` is a property of the input **element**. `element.value` reads/sets the box; once you extract the string (`let taskValue = el.value`) that string has no `.value`. Also can't assign to a `querySelector(...)` call itself.
- **Fix:** Clear the box with `document.querySelector("#task").value = ""` — `.value` hangs off the element, never off the extracted string.

- **Date:** 2026-07-18
- **Error:** Used `text-color: red;` in CSS to color text — nothing happened.
- **Concept:** `text-color` is not a real CSS property; the browser silently ignores unknown properties. Text color is just `color`; background is `background-color`.
- **Fix:** `color: red;` for text color. There is no `text-color`.

- **Date:** 2026-07-18
- **Doubt:** What `classList` / `.toggle()` do, and whether clicking again re-adds the class.
- **Concept:** `classList` is an element's set of CSS classes with methods `.add()`, `.remove()`, `.contains()`, `.toggle()`. `.toggle("x")` adds the class if absent, removes it if present — alternates each call (like a light switch). Good for on/off states like done/not-done.
- **Fix:** `el.classList.toggle("done")` flips the class every click; no need to check the current state yourself.

- **Date:** 2026-07-18
- **Doubt:** Why not add the `done` class directly in HTML when appending the `<li>`.
- **Concept:** "Done" is a runtime state that changes on user action, not a fixed property. Baking it in would make every new item start struck-through. Fixed things → HTML/CSS; things that change with user actions → toggled by JS.
- **Fix:** Create items without `done`; add/remove it dynamically with `classList.toggle` on click.
