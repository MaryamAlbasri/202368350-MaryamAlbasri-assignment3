# Technical Documentation
 
## 1. Overview
 
A static, single-page portfolio built with HTML, CSS and vanilla JavaScript. There is no framework, build tool or backend. All logic runs in the browser from `js/script.js`, and all styling is in `css/styles.css`.
 
| File | Purpose |
|---|---|
| `index.html` | Page structure: navbar, About, Projects, GitHub, Contact, lightbox, footer |
| `css/styles.css` | Theme variables, layout (Flexbox/Grid), components, responsive rules |
| `js/script.js` | All interactive features (described below) |
| `assets/images/` | Compressed project images |
 
The script is loaded at the end of `<body>`, so every element exists before the JavaScript runs.
 
## 2. Features and Implementation
 
### 2.1 GitHub API Integration
- **Endpoint:** `https://api.github.com/users/MaryamAlbasri/repos?sort=updated&per_page=6`
- `loadRepos()` uses `fetch` with `async/await` inside `try/catch`.
- Because `fetch` does not throw on HTTP errors (e.g. 404), the code checks `response.ok` and throws manually.
- **States:** a "Loading repositories..." message, a "No public repositories yet" message for an empty list, the repo cards, or a friendly error message if anything fails.
- Cards are built with `createElement` and `textContent` rather than `innerHTML`, so data from the API cannot inject HTML into the page.
- Limit: the unauthenticated GitHub API allows about 60 requests per hour per IP, which is enough for a portfolio.
### 2.2 Projects: Filter, Search and Sort
- Each card has `data-category` (`web` / `hardware`) and `data-date` (`YYYY-MM-DD`).
- `updateProjects()` hides a card unless it matches **both** the active filter and the search text. If nothing matches, an empty-state message is shown.
- `sortProjects()` copies the cards into an array, sorts by date (newest/oldest) or by title with `localeCompare`, and re-appends them with `appendChild`, which moves existing elements instead of creating new ones.
- Filtering only toggles a `.hidden` class, while sorting changes DOM order. The two are independent, so they combine correctly.
### 2.3 Contact Form Validation
- The form uses `novalidate`, and validation is done in JavaScript on `submit` (with `preventDefault`).
- **Rules:** name not empty; email not empty and matches `/^[^\s@]+@[^\s@]+\.[^\s@]+$/`; message at least 10 characters.
- `showError()` writes the message under the field and adds an `.invalid` red border. The confirmation only appears when every rule passes, and the form is then reset.
### 2.4 Visit Timer
- The start time is saved once with `Date.now()`. `setInterval` runs every second and calculates the elapsed time from the start time, which stays accurate even if the tab was in the background.
- It shows seconds, then minutes and seconds after the first minute.
### 2.5 Time-Based Greeting and Image Lightbox
- The greeting text depends on the current hour (morning / afternoon / evening).
- Clicking a project image opens it in a full-screen popup. It closes with the ✕ button, a click on the background, or the Esc key.
- An `IntersectionObserver` highlights the navbar link of the section in the middle of the screen.
## 3. State Management
 
State is stored in `localStorage` so it survives a page refresh.
 
| Key | Values | Used for |
|---|---|---|
| `theme` | `"dark"` / `"light"` | Dark mode toggle. Read on load, written on every toggle |
| `visitorName` | visitor's name | Personalised greeting. Saved on "Save", removed on "Change name" |
 
`showGreeting()` reads the saved name and also controls which UI is visible: the name input when there is no name, and the "Change name" button when there is one. Empty names are ignored.
 
## 4. Styling Notes
- Colors are CSS variables in `:root`. Dark mode only overrides the variables on `body.dark`, so no component needs its own dark styles.
- The project grid is 2 columns on desktop and 1 column below 768px. Below 480px, the nav text and section padding get smaller.
- `#name-box.hidden` is needed in addition to `.hidden`: `#name-box` sets `display: flex` with an ID selector, which is more specific than the `.hidden` class, so the class alone cannot hide it.
## 5. Performance
- Project images were resized to 1200px wide and compressed (with Squoosh), and they load with `loading="lazy"`.
- A duplicate `.project-card` rule and unused blank code were removed.
- A `<meta name="description">` tag was added.
- **Lighthouse (desktop, localhost):** Performance 100 · Accessibility 100 · Best Practices 96 · SEO 100.
## 6. Compatibility and Accessibility
- Uses only standard features supported by current Chrome, Safari, Firefox and Edge (`fetch`, `localStorage`, `IntersectionObserver`, CSS Grid and variables).
- The layout was tested at desktop, tablet and phone widths.
- Accessibility: all images have `alt` text, form fields have `<label>`s, and the icon-only buttons and inputs have `aria-label`s.
## 7. Known Limitations
- The contact form does not send email. It only validates and shows a confirmation, because there is no backend.
- The GitHub section needs an internet connection and is subject to the API rate limit.
- `localStorage` is per browser, so the saved name and theme don't carry over to other devices.
 