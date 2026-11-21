# Maryam Albasri – Portfolio (Assignment 3)
 
A personal portfolio website built with HTML, CSS and vanilla JavaScript for SWE363 Web Engineering at KFUPM. It builds on Assignments 1 and 2 and adds API integration, more advanced logic, state management and performance work.
 
**Live site:** https://maryamalbasri.github.io/202368350-MaryamAlbasri-assignment3/
 
## Features
 
- **GitHub API:** shows my latest public repositories, with a loading message and a friendly error message if the request fails.
- **Projects filter, search and sort:** filter by category (Web / Hardware), search by text, and sort by newest, oldest or name. All three work together.
- **Contact form validation:** checks for empty fields, a valid email format and a minimum message length before showing a confirmation.
- **Visitor name:** the visitor can save their name and is greeted by it (with a time-of-day greeting) on later visits.
- **Dark / light mode:** the chosen theme is remembered after a refresh.
- **Visit timer:** shows how long the visitor has been on the page.
- **Extras:** image popup (lightbox), active section highlight in the navbar, responsive layout for phones and tablets.
## Technologies
 
- HTML5, CSS3 (Flexbox, Grid, CSS variables, media queries)
- JavaScript (ES6+, `fetch`, `async/await`, `localStorage`, `IntersectionObserver`)
- GitHub REST API (no key required)
## Setup – Run Locally
 
No installation or build step is needed.
 
1. Clone the repository:
```bash
git clone https://github.com/MaryamAlbasri/202368350-MaryamAlbasri-assignment3.git
cd 202368350-MaryamAlbasri-assignment3
```
2. Open `index.html` in any modern browser.
   Or run a small local server (needed for tools like Lighthouse):
```bash
python3 -m http.server 8000
```
   then visit `http://localhost:8000`.
 
An internet connection is needed for the GitHub repositories section.
 
## Project Structure
 
```
├── README.md
├── index.html
├── css/styles.css
├── js/script.js
├── assets/images/
├── docs/
│   ├── ai-usage-report.md
│   └── technical-documentation.md
└── .gitignore
```
 
## Performance
 
Images were resized and compressed, project images use lazy loading, and duplicate CSS and unused code were removed. Lighthouse (desktop): **Performance 100 · Accessibility 100 · Best Practices 96 · SEO 100**.
 
## AI Use
 
I used Claude (Anthropic, Opus 5.5) to understand the requirements, plan the work, generate starter code for the GitHub API section, sorting, visit timer and visitor name features, and review my CSS. I tested every feature, edited the code to fit my site and made sure I understand it. Commits containing AI-assisted code are marked with `Assisted-by: Claude (Opus 5.5)`. Full details, the usage log and my declaration are in [docs/ai-usage-report.md](docs/ai-usage-report.md).
 
## Author
 
Maryam Albasri – Computer Science, KFUPM
 