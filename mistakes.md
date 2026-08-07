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

- **Date:** 2026-07-18
- **Doubt:** Didn't know clicking the delete button inside an li also triggers the li's own click listener (invisible here because the item is removed instantly).
- **Concept:** Event bubbling — a click on a child element also fires click handlers on all its ancestors. Fix concept: event.stopPropagation() in the child's handler.
- **Fix:** In the delete button's listener, call event.stopPropagation() so the li's toggle handler doesn't also run.

- **Date:** 2026-07-18
- **Error:** After localStorage.setItem("array", ...), tried array.push(...) — expected the storage KEY to exist as a variable. Also called JSON.parse but never assigned the result, then wondered where the array went.
- **Concept:** Storage keys are labels inside localStorage, not JS variables; and any expression result is lost unless assigned (let todos = JSON.parse(...)).
- **Fix:** Full cycle: let todos = JSON.parse(localStorage.getItem(key)); todos.push(x); localStorage.setItem(key, JSON.stringify(todos)).

- **Date:** 2026-07-18
- **Error:** Typed json.stringify — ReferenceError.
- **Concept:** JS is case-sensitive; the global object is JSON (all caps).
- **Fix:** JSON.stringify / JSON.parse.

- **Date:** 2026-07-18
- **Error:** Defined saveTodos inside the click handler (and without let/const) but never called it — expected defining a function to run it. Then, when loading, wrote let todos = [getItem(...) ? getItem(...) : []] — wrapped the whole thing in [ ], creating a nested array, and forgot JSON.parse on the stored string.
- **Concept:** Defining vs calling a function; [x] builds a NEW one-element array around x; getItem always returns a string (or null) so it must go through JSON.parse.
- **Fix:** Define saveTodos once at top level, call it after each change; load with: let todos = JSON.parse(localStorage.getItem("todos")) || [];

- **Date:** 2026-07-22
- **Error:** In delete handler, compared against showTasks.textContent — but the li contains the "x" button too, so textContent is "milkx" and filter matched nothing (same textContent-includes-children trap as earlier the same session).
- **Concept:** textContent returns ALL text inside an element including children. Capture the clean input value in a variable at add time and reuse it (closure), instead of re-reading the DOM.
- **Fix:** let taskName = textBox.value at top of add handler; use taskName for li text, push, and filter comparison.

- **Date:** 2026-07-22
- **Doubt:** Thought the delete listener could not see textBox because it wasn't declared in the immediate outer function.
- **Concept:** Scope is a chain up to the top level — top-level variables are visible to every function. The real issue with textBox.value in a later-running handler is WHEN it reads: .value is a live read at click time (empty after clearing), vs a variable captured at add time via closure.
- **Fix:** Distinguish live DOM reads (now) from closure-captured variables (frozen per add-run).

- **Date:** 2026-07-22
- **Error:** Repeatedly put the render loop INSIDE showTodos(todo) and ignored the parameter (looped todos[i] over one reused li, read textBox.value in a render function). Struggled 3 attempts with extracting a per-item function.
- **Concept:** Division of labor: a render function handles ONE item via its parameter; the loop (forEach) lives OUTSIDE and calls it once per element. Also re-hit: one element appended N times = one item overwritten N times.
- **Fix:** function showTodos(todo) builds one li from todo.taskname (no loop, no DOM reads); todos.forEach(showTodos) at top level; add handler pushes then calls showTodos(newTodo).

- **Date:** 2026-08-03
- **Error:** Used fetched data (myProfile.login) in top-level code before the fetch resolved — ReferenceError. Then chained a third .then expecting the same data, but each .then receives only what the previous callback RETURNED (console.log returns undefined).
- **Concept:** Async timing — fetched data exists only inside the .then callback that receives it; .then chains pass return values, not the original data.
- **Fix:** Do all work with the data inside its callback; one callback body ({ }) can hold many statements — no extra .then needed.

- **Date:** 2026-08-03
- **Error:** Multi-statement arrow function without { } braces — syntax error.
- **Concept:** Braceless arrow bodies allow exactly one expression; multiple statements need { }.
- **Fix:** .then((data) => { stmt1; stmt2; });

- **Date:** 2026-08-03
- **Doubt:** Thought first .then gives "the data from the url as a whole object."
- **Concept:** First .then gives a Response object (envelope: status/headers, unread body); response.json() reads the body and returns ANOTHER promise — hence the second .then.
- **Fix:** .then(r => r.json()).then(data => ...) — two waits, two thens.

- **Date:** 2026-08-07
- **Doubt:** Described the Response as "headings of the web page" — conflated HTTP response headers with page headings; fuzzy on what each await in fetch waits for.
- **Concept:** First await = server replied (Response object: status + headers, body unread); second await = body fully read and parsed into a JS object. Headers are response metadata, unrelated to <h1> headings.
- **Fix:** "Did they reply?" then "read the reply into an object" — two waits, two awaits.
