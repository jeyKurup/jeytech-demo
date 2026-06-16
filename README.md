# JeyTech Solutions

A fictional technology consultancy website built with plain HTML5, CSS3, and vanilla JavaScript. This project serves as a hands-on learning environment for the **Advanced Claude Code** course on Pluralsight.

---

## Project Overview

JeyTech Solutions is a five-page static website for a technology consultancy. The site covers the company's services, portfolio, team, and a working contact form. The codebase is intentionally framework-free so the focus stays on Claude Code tooling rather than any particular frontend framework.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Markup | HTML5 with semantic elements |
| Styles | CSS3 with custom properties (design tokens) |
| Behaviour | Vanilla JavaScript (ES6+ modules) |
| Dev server | `serve` (via `npx`) |
| Linting | ESLint |
| Formatting | Prettier |
| Unit tests | Node.js built-in test runner (`node --test`) |
| End-to-end tests | Playwright |

No frontend frameworks or build tools are required to run the site.

---

## Prerequisites

- Node.js 18 or later
- npm (included with Node.js)
- Git

---

## Setup and Installation

### 1. Clone the repository

```bash
git clone https://github.com/nyisztor/JeyTech-demo.git
cd jeytech-demo
```

### 2. Install dependencies

```bash
npm install
```

This installs all development dependencies: Playwright, ESLint, Prettier, and the `serve` package.

### 3. Start the local development server

```bash
npm run dev
```

Then open your browser to:

```
http://localhost:3000/pages/index.html
```

The `serve` package serves the `src/` directory. All internal links use root-relative paths (e.g., `/pages/services.html`), so the site must be accessed through the dev server rather than opened as a file directly.

---

## Project Structure

```
jeytech-demo/
├── src/
│   ├── pages/                  # The five HTML pages
│   │   ├── index.html          # Homepage — hero, feature highlights, CTA
│   │   ├── services.html       # Services listing (development, cloud, consulting, data)
│   │   ├── portfolio.html      # Project gallery with category filter buttons
│   │   ├── team.html           # Team member cards and company values
│   │   └── contact.html        # Contact form with inline validation
│   ├── css/
│   │   ├── variables.css       # Design tokens (colours, typography, spacing, shadows)
│   │   ├── base.css            # CSS reset and global element styles
│   │   ├── components.css      # Shared components (buttons, nav, footer, forms)
│   │   └── pages/
│   │       ├── home.css        # Homepage-specific styles
│   │       ├── services.css    # Services page styles
│   │       ├── portfolio.css   # Portfolio grid and filter styles
│   │       ├── team.css        # Team card and values section styles
│   │       └── contact.css     # Contact form layout styles
│   └── js/
│       ├── navigation.js       # Mobile nav toggle (open/close, Escape key, outside-click)
│       ├── portfolio-filters.js # Category filter logic for the portfolio page
│       ├── contact-form.js     # Form submission handler (uses validation.js)
│       └── validation.js       # Reusable field and form validation utilities
├── tests/
│   ├── e2e/
│   │   ├── navigation.spec.js  # Playwright tests for desktop and mobile navigation
│   │   └── contact-form.spec.js # Playwright tests for the contact form
│   └── unit/
│       └── validation.test.js  # Unit tests for email, phone, and length validation
├── docs/                       # Design specs and API documentation
├── .claude/                    # Claude Code configuration (agents, skills, hooks, commands)
├── .mcp.json                   # MCP (Model Context Protocol) server configuration
├── package.json
└── CLAUDE.md                   # Project conventions and context for Claude Code
```

---

## Available npm Scripts

Run all commands from the project root.

| Script | What it does |
|---|---|
| `npm run dev` | Starts the local server at `http://localhost:3000` |
| `npm run lint` | Runs ESLint against `src/js/` |
| `npm run lint:fix` | Runs ESLint and auto-fixes where possible |
| `npm run format` | Formats all HTML, CSS, and JS files in `src/` with Prettier |
| `npm run format:check` | Checks formatting without writing changes |
| `npm run test` | Runs unit tests then E2E tests |
| `npm run test:unit` | Runs Node.js unit tests in `tests/unit/` |
| `npm run test:e2e` | Runs Playwright E2E tests |
| `npm run test:e2e:ui` | Opens the Playwright UI for interactive test runs |

---

## Code Conventions

### HTML

- Use semantic elements: `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`
- Include ARIA (Accessible Rich Internet Applications) labels and `aria-current` attributes for navigation state
- Keep each page under 200 lines
- Add a skip-link (`<a href="#main-content">`) at the top of every page

### CSS

- Follow BEM (Block Element Modifier) naming: `.block__element--modifier`
  - Example: `.nav__menu`, `.feature-card__title`, `.btn--primary`
- Use CSS custom properties defined in `variables.css` for all colours, spacing, and typography values
- Write mobile-first responsive styles
- All design tokens live in `variables.css` under `:root`

### JavaScript

- ES6 modules with named exports — no default exports
- JSDoc comments on all public functions
- No global variables; module-level constants use `const` with descriptive names
- Each module auto-initialises on `DOMContentLoaded` (or immediately if the DOM is already ready)
- Modules that apply to specific pages are only loaded on those pages via `<script type="module">` tags

---

## Testing

Run tests before committing. The full suite runs unit tests first, then E2E tests:

```bash
npm run test
```

Run each suite individually:

```bash
npm run test:unit    # Node.js built-in runner — no dependencies needed
npm run test:e2e     # Playwright — requires npm install and a running browser
```

### Unit tests

Located in `tests/unit/`. Written with the Node.js built-in `node:test` module and `node:assert`. Currently covers the validation logic in `src/js/validation.js`: email pattern, phone pattern, required-field checks, and minimum-length checks.

### End-to-end tests (E2E)

Located in `tests/e2e/`. Written with Playwright. Cover:

- Desktop and mobile navigation behaviour (`navigation.spec.js`)
- Contact form submission and inline validation (`contact-form.spec.js`)

Playwright tests expect the dev server to be running on `http://localhost:3000` before you run them.

---

## Git Workflow

### Branch naming

| Branch | Purpose |
|---|---|
| `main` | Production-ready code |
| `feature/*` | New features (e.g., `feature/services-redesign`) |
| `bugfix/*` | Bug fixes (e.g., `bugfix/responsive-nav`) |

### Commit message format

```
type: short description
```

| Type | When to use |
|---|---|
| `feat` | A new feature |
| `fix` | A bug fix |
| `docs` | Documentation changes only |
| `style` | Formatting, whitespace — no logic change |
| `refactor` | Code restructure with no behaviour change |
| `test` | Adding or updating tests |

Examples:

```
feat: add contact form validation
fix: correct mobile nav toggle
docs: update README setup instructions
```

---

## Optional: Figma Design File

The Figma design file used in the MCP integration modules is available here:

[JeyTech Solutions on Figma](https://www.figma.com/design/UZ2t3sc5vi2cn9MXHkOfLY/JeyTech-Solutions?node-id=1-2&p=f)

A free Figma account is required to view or duplicate it. This is optional — all course modules can be followed without accessing Figma.

---

## License

Educational project for Pluralsight. All rights reserved.
