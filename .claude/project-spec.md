# JavaScript Project Specs — Beginner to Moderate

Curated from: practical-tutorials/project-based-learning, JavaScript30 (Wes Bos), romeojeremiah/javascript-projects-for-beginners, Xtremilicious/projectlearn-project-based-learning.

Aligned to your roadmap. Pick a project, build it, push to GitHub, move on.

---

## HOW TO USE THIS FILE

1. Find the section matching your current roadmap week.
2. Pick ONE project from that section.
3. Build it yourself — type every line.
4. If stuck, ask Claude Code to **explain or debug**, not to write the feature.
5. Push to GitHub when done (even if imperfect). Move to the next project.

---

## WEEK 1 — Variables, Types, Functions, Conditionals, Loops

### Project 1: Age Calculator
- **Input:** Birth year (prompt or hardcoded)
- **Output:** Current age, days lived, days until next birthday
- **Concepts:** variables, arithmetic, conditionals, Date object basics
- **Files:** `index.html`, `app.js`
- **Stretch:** Add input validation (non-numeric, future year, negative)

### Project 2: FizzBuzz Variations
- **Input:** A number range (1–100)
- **Output:** Print numbers, but replace multiples of 3 with "Fizz", 5 with "Buzz", both with "FizzBuzz"
- **Concepts:** loops, modulo operator, conditionals, string output
- **Stretch:** Make it configurable — user picks the words and divisors

### Project 3: Tip Calculator
- **Input:** Bill amount, tip percentage, number of people
- **Output:** Tip per person, total per person
- **Concepts:** functions, parameters, return values, basic math
- **Files:** `index.html`, `style.css`, `app.js`
- **Stretch:** Render results in the DOM instead of console.log

### Project 4: Temperature Converter
- **Input:** Temperature value and unit (C/F/K)
- **Output:** Converted value in the other two units
- **Concepts:** functions, conditionals, switch statement
- **Stretch:** Build a simple UI with buttons to toggle direction

---

## WEEK 2 — Arrays, Objects, DOM, Events

### Project 5: To-Do List (Vanilla JS)
- **Features:** Add task, mark complete (toggle), delete task, persist in localStorage
- **Concepts:** arrays, array methods (push, filter, map), DOM manipulation, events, localStorage, JSON.parse/stringify
- **Files:** `index.html`, `style.css`, `app.js`
- **No frameworks.** Pure DOM — querySelector, createElement, addEventListener.
- **Source:** JS30 / JSBeginners classic

### Project 6: Grocery List
- **Features:** Add items, edit items inline, delete items, clear all
- **Concepts:** DOM CRUD operations, event delegation, editing existing DOM nodes
- **Stretch:** Add categories (fruits, dairy, etc.) using objects

### Project 7: Color Flipper
- **Features:** Button click generates a random hex color, sets it as background, displays the hex code
- **Concepts:** arrays, Math.random, DOM style manipulation, event listeners
- **Files:** `index.html`, `style.css`, `app.js`
- **Stretch:** Add "copy to clipboard" functionality

### Project 8: Array Cardio (no UI)
- **Input:** A hardcoded array of objects (e.g., inventors with name, birth year, death year)
- **Tasks:** Filter inventors born in the 1500s. Sort by birth date. Calculate total years lived. Sort by last name.
- **Concepts:** filter, map, sort, reduce — all in the console
- **Source:** JavaScript30 Day 4
- **Why this matters:** These array methods are 80% of the JS you'll write in React later.

### Project 9: Drum Kit
- **Features:** Press keyboard keys → play corresponding sound + visual animation
- **Concepts:** keydown events, data attributes, audio API, CSS transitions, transitionend event
- **Files:** `index.html`, `style.css`, `app.js` + sound files (find free .wav online)
- **Source:** JavaScript30 Day 1

---

## WEEK 3 — Async JS, Fetch, Promises, API Calls

### Project 10: Weather App
- **API:** OpenWeatherMap (free tier, needs API key)
- **Features:** Enter city name → fetch weather → display temp, description, icon
- **Concepts:** fetch, async/await, JSON parsing, API keys, error handling (city not found)
- **Files:** `index.html`, `style.css`, `app.js`
- **Important:** API key goes in your JS file for now (it's a free public API). In Next.js later, it goes in .env + API route.

### Project 11: GitHub Profile Viewer
- **API:** GitHub REST API (no key needed)
- **Features:** Enter username → fetch profile → display avatar, name, bio, repo count, top repos
- **Concepts:** fetch, promises, DOM rendering from API data, error states
- **Stretch:** Click a repo → fetch its details (languages, stars)

### Project 12: Random Quote Generator
- **API:** quotable.io or similar free quote API
- **Features:** Load page → show random quote + author. Button to fetch new quote.
- **Concepts:** fetch on page load, button click → new fetch, loading states
- **Stretch:** Add "share on Twitter" link (construct URL with quote text)

### Project 13: Type Ahead Search
- **API:** Use a JSON endpoint (cities, countries, or any list)
- **Features:** Text input → as user types → filter and display matching results with highlights
- **Concepts:** fetch, filtering arrays, regex for highlighting matches, input event
- **Source:** JavaScript30 Day 6

---

## WEEK 4 — Next.js Intro, Tailwind, First Deploy

### Project 14: Personal Landing Page (Next.js + Tailwind)
- **Setup:** `npx create-next-app@latest` with Tailwind
- **Features:** Name, one-liner, 3–4 sections (about, projects, contact), responsive
- **Concepts:** Next.js file structure, pages/app router, Tailwind utility classes, components
- **Deploy to Vercel.** Your first live URL.
- **Tailwind focus:** Only learn `p-`, `m-`, `text-`, `bg-`, `flex`, `gap-`, `rounded-`, `shadow-`, `w-`, `h-`

### Project 15: Multi-Page Site (Next.js Routing)
- **Features:** Home, About, Projects pages with shared layout/nav
- **Concepts:** Next.js routing (app directory), Link component, layout.js, shared components
- **Stretch:** Add a dark/light mode toggle using Tailwind's dark: prefix

---

## WEEK 5 — React Hooks + First AI Tool

### Project 16: Counter + Form (React State Practice)
- **Features:** Counter with increment/decrement/reset. Separate form that takes text input and displays it.
- **Concepts:** useState, event handling in React, controlled inputs
- **This is NOT a product — it's deliberate practice for useState before building the AI tool.**

### Project 17: Text Rewriter (Your First AI App)
- **THE MAIN BUILD FOR WEEK 5.** This is in your roadmap.
- **Features:** Textarea input → pick tone (funny / formal / Gen Z / pirate) → hit "Rewrite" → Claude API returns rewritten text
- **Stack:** Next.js page → API route (`/api/rewrite`) → Claude API → return response
- **Concepts:** API routes, environment variables (.env.local), server-side API calls, loading states, error handling
- **Critical:** API key NEVER in client code. Always in .env.local, only accessed in API route.

---

## WEEK 6 — Supabase + Saving Data

### Project 18: Quick Notes App
- **Features:** Type a note → save to Supabase → see all saved notes below (newest first)
- **Concepts:** Supabase client setup, INSERT, SELECT, ordering, real-time display
- **No auth yet.** All notes are public/shared. That's fine — auth comes next week.
- **Stretch:** Add delete button per note. Add character count.

### Project 19: Bookmark Saver
- **Features:** Paste a URL + title → save to Supabase → display bookmarks list → delete bookmarks
- **Concepts:** Supabase CRUD (insert, select, delete), form handling in React
- **Stretch:** Auto-fetch page title from URL using an API route

---

## WEEK 7 — Authentication + Row Level Security

### Project 20: Notes App with Auth
- **Take Project 18 and add:** Supabase email magic-link login. Each user sees ONLY their own notes.
- **Concepts:** Supabase auth, sessions, user_id on every row, Row Level Security (RLS) policies
- **Critical learning:** RLS. If you skip this, every user's data leaks. Get this right once.
- **Test it:** Create two accounts, verify one can't see the other's notes.

---

## WEEK 8 — Habit Tracker (Full Skeleton App)

### Project 21: Habit Tracker
- **THE MAIN BUILD FOR WEEK 8.** This is in your roadmap.
- **Features:** Login → add habits → mark today as done → see streak per habit → calendar/grid view of history
- **Stack:** Next.js + Tailwind + Supabase auth + Supabase DB
- **DB tables:** `habits` (id, user_id, name, created_at), `completions` (id, habit_id, date)
- **RLS:** User can only read/write their own habits and completions
- **Stretch:** Weekly summary, longest streak calculation
- **Public post:** Share the link on Twitter/X or LinkedIn. 4–5 lines. No metrics expectation — you're practicing posting.

---

## WEEK 9 — First AI + Auth + DB App

### Project 22: Pick ONE of These (Your Choice)

**Option A: Resume Tailor**
- Paste resume + job description → Claude API rewrites resume for that JD → save versions to Supabase
- Tables: `resumes` (id, user_id, original, tailored, jd, created_at)

**Option B: Study Notes Summarizer**
- Paste long notes → Claude API returns bullet summary → save in folders
- Tables: `folders` (id, user_id, name), `summaries` (id, folder_id, original, summary, created_at)

**Option C: Code Explainer**
- Paste code → Claude API explains it line by line → save explanations
- Tables: `explanations` (id, user_id, code, explanation, language, created_at)

**All three use the same skeleton:** Next.js + Tailwind + Supabase auth + DB + Claude API.

---

## WEEKS 10–11 — Polish + Second Build

### Project 23: Polish Week 9's App
Not a new build. Take your Week 9 project and add:
- Clean landing page (hero + one CTA)
- Error handling that doesn't crash
- Loading spinner during AI calls
- Free-tier limit (e.g., 5 uses/day before sign-up required)
- Public post with link

### Project 24: Speed Build — Same Skeleton, Different Problem
- **Goal:** Prove you can ship the full skeleton (auth + DB + AI + deploy) in ONE WEEK.
- Pick a different problem than Week 9. Ship it. Don't polish — just ship.
- Ideas: AI email drafter, workout logger with AI suggestions, daily journal with AI mood analysis

---

## MODERATE — Standalone Practice Projects (Do Anytime After Week 4)

These are optional skill-sharpeners. Do one when you want a break from the roadmap.

### CSS Clock
- Analog clock using CSS transforms + JS to update hands every second
- Concepts: setInterval, CSS transform/rotate, Date methods
- Source: JavaScript30 Day 2

### Countdown Timer
- Pick a future date → show days, hours, minutes, seconds counting down
- Concepts: setInterval, Date math, DOM updates
- Stretch: Add confetti animation when timer hits zero

### Image Gallery with Lightbox
- Grid of images → click one → fullscreen overlay with close button
- Concepts: CSS Grid, event delegation, DOM manipulation, transitions

### Expense Tracker
- Add income/expense entries → running balance → list with delete
- Concepts: array of objects, reduce for totals, localStorage persistence, DOM rendering

### Markdown Previewer
- Textarea on left → rendered HTML preview on right (live update)
- Concepts: textarea input event, a markdown parsing library (marked.js), innerHTML
- Stretch: Add copy-to-clipboard for the rendered HTML

### Pomodoro Timer
- 25 min work → 5 min break cycle. Start/pause/reset buttons. Audio alert.
- Concepts: setInterval/clearInterval, state management, Audio API

---

## SOURCES & LINKS

- practical-tutorials/project-based-learning: https://github.com/practical-tutorials/project-based-learning
- JavaScript30: https://javascript30.com/ | https://github.com/wesbos/JavaScript30
- JSBeginners: https://github.com/romeojeremiah/javascript-projects-for-beginners
- ProjectLearn: https://projectlearn.io/ | https://github.com/Xtremilicious/projectlearn-project-based-learning
