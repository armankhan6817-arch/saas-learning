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

- **Date:** 2026-08-08
- **Error:** Expected try/catch to catch a 400 Bad Request — it fired only by accident via a downstream TypeError (gotData.current was undefined). fetch doesn't reject on HTTP error statuses.
- **Concept:** fetch rejects only when no reply arrives (network/DNS); a 400/404 is a successful fetch. Detect it via response.ok / response.status and throw manually to route into catch.
- **Fix:** if (!response.ok) throw new Error(`status: ${response.status}`); before response.json().

- **Date:** 2026-08-08
- **Error:** Repeated brace scrambling while editing nested blocks: put catch inside the else block; later deleted the if but kept the throw (unconditional throw = success path unreachable) and lost the function's closing brace. Also once replaced throw with console.log + else, creating two separate error paths.
- **Concept:** Block structure — catch pairs with try at the same level; throw exits immediately so no else is needed after it; every { needs its matching }. throw exists to funnel all failures into one catch.
- **Fix:** Edit structure first (matching braces, empty blocks), then fill in statements; let Prettier re-indent to reveal mismatches. Pattern: fetch → if (!ok) throw → parse → render, all flat inside try.

- **Date:** 2026-08-08
- **Doubt:** Wanted to handle "city not found" inside the if (!response.ok) block, and instead of a check renamed the catch-all log to "city not found" — didn't see which code path a not-found city takes.
- **Concept:** APIs choose their own "not found" convention: GitHub sends 404 (.ok false), Open-Meteo geocoding sends 200 OK with no results key (.ok true — status check never fires; crash comes later at results[0]). Envelope check (.ok) ≠ content check (does the parsed data have what I need). Content can only be checked AFTER .json(). Catch stays generic; the thrown message carries the specific reason.
- **Fix:** Order: fetch → if (!ok) throw → gotData = await .json() → if (!gotData.results) throw new Error("City not found") → use data. Inspect real API responses in the browser to learn each API's convention.

- **Date:** 2026-08-10
- **Doubt:** Couldn't read `const [todos, setTodos] = useState([]);` — the two sets of square brackets in one line.
- **Concept:** `useState` returns a 2-item array `[currentValue, setterFunction]`; the left-hand brackets are array destructuring (unpack by position), the inner `[]` is the starting value. Names are arbitrary, position is what matters.
- **Fix:** Long form is `const s = useState([]); const todos = s[0]; const setTodos = s[1];` — destructuring just collapses it. Convention: `thing` / `setThing`.

- **Date:** 2026-08-10
- **Error:** For a yes/no state wrote `const [menu, menuNow] = useState("closed")` — string instead of boolean, and slot-2 name didn't read as a function.
- **Concept:** State type should match the question: booleans for yes/no, "" for text, 0 for numbers, [] for lists. A string yes/no can't toggle cleanly and breaks silently on typos. Slot 2 is always a function.
- **Fix:** `const [menuOpen, setMenuOpen] = useState(false);` then toggle with `setMenuOpen(!menuOpen)`.

- **Date:** 2026-08-10
- **Doubt:** Why `const` for a state value that appears to change (`const [count, setCount] = useState(0)`).
- **Concept:** A component is a function; each render is a fresh call with fresh locals. `count` is a frozen snapshot for that one render — React re-calls the function to show a new value, it never reassigns the variable. `const` also hard-blocks `count = count + 1`, which would silently do nothing (no re-render).
- **Fix:** Never assign to state. Only the setter changes it: `setCount(count + 1)`.

- **Date:** 2026-08-11
- **Doubt:** Tried `{ if (shown) { <p>…</p> } }` inside JSX; didn't know `&&`.
- **Concept:** `{ }` in JSX evaluates an *expression* (produces a value) — `if` is a *statement* (produces none), same rule that bans `if` in a braceless arrow body. `a && b` returns `a` when falsy, else `b`; React renders nothing for `false`/`null`/`undefined`. Trap: `0` is falsy but React *does* print `0`, so use `count > 0 && …`.
- **Fix:** `{shown && <p>…</p>}` or `{shown ? <p>A</p> : <p>B</p>}`. To use a real `if`, compute above the return into a variable and render `{para}` — JSX is just a value.

- **Date:** 2026-08-11
- **Error:** Wrote `{{output && <p>…</p>}}` in JSX — double braces caused a syntax error.
- **Concept:** Braces mean three different things by position: JSX escape, code block, object literal. Outer `{` escapes into JS; the second `{` is then read as an object literal, and `output && <p/>` isn't valid object syntax.
- **Fix:** One pair only — `{output && <p>…</p>}`.

- **Date:** 2026-08-11
- **Doubt/trap:** In a handler that calls `setTone(chosenTone)`, reading `tone` on the next line gives the OLD tone (output lags one click behind).
- **Concept:** State is a frozen snapshot per render; setters schedule the next render, they don't mutate the current variable.
- **Fix:** Use the handler's own argument (`chosenTone`), not the state variable you just set.
- **2026-08-15:** / **Doubt:** Expected state variable to update immediately after setting it, causing confusing console logs. / **Concept:** React State as a Snapshot / **Fix:** State updates are scheduled for the next render; they do not mutate the const variable in the current render's closure.
- **Date:** 2026-08-15
- **Error/Doubt:** Expected React state setter to update the variable immediately inside the same handler.
- **Concept:** React state updates are scheduled; each render has a fixed state snapshot.
- **Fix:** After setText(...), the current handler still sees the old text. The new text appears on the next render.

- **Date:** 2026-08-15
- **Error/Doubt:** Wondered whether tone state alone is enough for API response flow, without separate output state.
- **Concept:** Separate state for user input/selection versus generated result; local variables do not persist/render UI.
- **Fix:** Use chosenTone/tone to tell the API what style to use, and output state to store/display the API reply.


- **Date:** 2026-08-19
- **Error:** In the Next.js API route, read Claude's reply as `response.choices[0].message.content` — that is OpenAI's response shape, not Anthropic's. Would crash with "Cannot read properties of undefined (reading '0')".
- **Concept:** Every API defines its own response shape; SDKs are not interchangeable. Anthropic returns `content` as an *array of content blocks*, each with a `.type` and (for text blocks) a `.text`.
- **Fix:** `response.content[0].text`. When unsure of a response shape, `console.log` the whole object once and read it, don't guess from another API's docs.

- **Date:** 2026-08-19
- **Error/Doubt:** Prompt built as `Rewrite in ${tone} tone:\n\n${text} and return only the rewritten text...` — the instruction was glued onto the end of the user's text with no separator, so the model can read the instruction as part of the text to rewrite.
- **Concept:** Prompt structure matters: instructions and user-supplied data must be visibly separated, or the model can't tell where one ends and the other begins (same class of problem as prompt injection).
- **Fix:** Put all instructions before the data, and delimit the data (blank lines, quotes, or XML-ish tags like `<text>...</text>`).

- **Date:** 2026-08-19
- **Doubt:** Confused `JSON.stringify()` with `response.json()` — why "json" appears before the dot sometimes and after it other times.
- **Concept:** Two different things share the name. `JSON` (capitals) is a built-in global toolbox object holding `.stringify()` and `.parse()`, which work on any string/object you pass as an argument. `.json()` (lowercase) is a method belonging to a Response/Request object that reads *its own* body and parses it — hence empty parentheses and `await`. General rule: whatever sits before the dot owns the function after it.
- **Fix:** `JSON.stringify(obj)` → data goes in the parentheses. `await response.json()` → parentheses empty, the data is already inside `response`.

- **Date:** 2026-08-19
- **Doubt:** Why `await req.json()` instead of `JSON.parse(req)`.
- **Concept:** `req` is a Request *object* (method, url, headers, body), not a string — `JSON.parse` needs a string, and would receive `"[object Request]"`. Also the body is a *stream* still arriving in chunks, so there is nothing complete to parse yet.
- **Fix:** `await req.json()` = wait for all body chunks → assemble into a string → `JSON.parse` it. The manual equivalent is `const raw = await req.text(); const body = JSON.parse(raw);`. A body can only be read once.

- **Date:** 2026-08-19
- **Doubt:** "Why `JSON.stringify` in the return when `response.content[0].text` is already a string?"
- **Concept:** stringify isn't being applied to the text — it's applied to `{ output: text }`, which is an *object* wrapping the string. Braces = object, even when every value inside is a string.
- **Fix:** Read `JSON.stringify(X)` by asking what X is, not what's nested inside it. Wrapping the reply in an object (rather than sending the bare string) leaves room to add fields later — error, tone, usage — without breaking the client.

- **Date:** 2026-09-08
- **Error:** Wrote `${Loading === "true" ? ... }` to test a boolean state variable against the *string* `"true"`. `false === "true"` and `true === "true"` are both false, so the condition never fires.
- **Concept:** `===` compares type as well as value. A boolean is never equal to a string that looks like it. Booleans don't need a comparison at all.
- **Fix:** Use the boolean directly: `disabled={loading}`, `${loading ? "..." : "..."}`. Only compare with `===` when the value really is a string (like `tone === "casual"`).

- **Date:** 2026-09-08
- **Error:** Tried to disable a button by putting the word `disabled` inside `className`. CSS classes can't disable anything — the button stayed clickable.
- **Concept:** `disabled` is an HTML *attribute* on the element (like `onClick`), not a class. In JSX it takes a boolean in braces. Tailwind's `disabled:` **variant** is a separate thing — it only styles an element that is *already* disabled by the attribute.
- **Fix:** `<button disabled={loading} className="... disabled:opacity-50 disabled:cursor-not-allowed">`. Attribute controls behaviour; variant controls appearance.
