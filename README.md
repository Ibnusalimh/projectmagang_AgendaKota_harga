# AgendaKota — Biaya / Harga Landing Page (CRA Scaffold)

A Create-React-App scaffold reserved for the **AgendaKota — Biaya** ("Pricing") marketing page. As of the current commit the repository only contains the default CRA template; the working Pricing implementation lives inside the sibling [`projectmagang`](https://github.com/zXmill/projectmagang) repo at `src/modules/biaya/`.

> Bootstrapped with [Create React App](https://github.com/facebook/create-react-app).
> Sibling repos in the same series: [`projectmagang_AgendaKota_klinikpage`](https://github.com/zXmill/projectmagang_AgendaKota_klinikpage), [`projectmagang_AgendaKota_fiturpage`](https://github.com/zXmill/projectmagang_AgendaKota_fiturpage).

---

## Table of Contents

1. [Overview](#overview)
2. [Current Status](#current-status)
3. [Tech Stack](#tech-stack)
4. [Project Structure](#project-structure)
5. [Getting Started](#getting-started)
6. [Available Scripts](#available-scripts)
7. [How This Repo Fits the AgendaKota Project](#how-this-repo-fits-the-agendakota-project)
8. [Roadmap](#roadmap)
9. [Code Review Notes](#code-review-notes)
10. [Screenshots](#screenshots)
11. [License](#license)

---

## Overview

`projectmagang_AgendaKota_harga` is one of three single-page apps spun off from the AgendaKota internship project, each meant to host one marketing page:

| Repo                                             | Page                                      |
| ------------------------------------------------ | ----------------------------------------- |
| `projectmagang_AgendaKota_klinikpage`            | "Untuk Klinik"                            |
| `projectmagang_AgendaKota_fiturpage`             | "Fitur" (Features)                        |
| **`projectmagang_AgendaKota_harga`** (this)      | **"Biaya" (Pricing)**                     |

While the **klinik** sibling has a complete component tree (`Header`, `BenefitSection`, `PricingSection`, `PricingCard`, `FAQSection`, …), this repo currently ships the unmodified CRA template.

## Current Status

`src/App.js` is the default CRA welcome screen:

```jsx
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>Edit <code>src/App.js</code> and save to reload.</p>
        <a className="App-link" href="https://reactjs.org" target="_blank" rel="noopener noreferrer">
          Learn React
        </a>
      </header>
    </div>
  );
}
```

The Biaya page UI that was screenshotted in the previous README is implemented in the parent monorepo at:

- `projectmagang/src/modules/biaya/App.jsx`
- `projectmagang/src/modules/biaya/components/`
- `projectmagang/src/modules/biaya/layouts/`

This repo is currently a **placeholder** intended to host an extracted, deployable copy of that module. The `PricingSection` / `PricingCard` components that already exist in `projectmagang_AgendaKota_klinikpage/src/components/` are a good starting point for re-use.

## Tech Stack

| Concern         | Library                                                    |
| --------------- | ---------------------------------------------------------- |
| UI              | `react` 18, `react-dom`                                    |
| Build           | `react-scripts` 5 (Create React App)                       |
| Testing         | `@testing-library/jest-dom`, `@testing-library/react`, `@testing-library/user-event` |
| Web Vitals      | `web-vitals`                                               |

> Note: this repo **does not** include TailwindCSS (no `tailwind.config.js`, no `tailwindcss` in `package.json`), unlike `…_klinikpage`. Add it when porting the real implementation.

## Project Structure

```
projectmagang_AgendaKota_harga/
├── public/
│   ├── index.html
│   ├── favicon.ico
│   ├── logo192.png
│   ├── logo512.png
│   ├── manifest.json
│   └── robots.txt
├── src/
│   ├── index.js              # CRA entry point
│   ├── App.js                # Default CRA welcome screen
│   ├── App.css
│   ├── App.test.js
│   ├── index.css
│   ├── logo.svg
│   ├── reportWebVitals.js
│   └── setupTests.js
├── package.json              # name: "biayalanpage"
└── package-lock.json
```

## Getting Started

### Prerequisites

- Node.js 18+ and npm

### Install & run

```bash
git clone https://github.com/zXmill/projectmagang_AgendaKota_harga.git
cd projectmagang_AgendaKota_harga
npm install
npm start                # http://localhost:3000
```

You should see the default React welcome screen until the real Biaya content is migrated in.

### Build for production

```bash
npm run build            # outputs to ./build
```

## Available Scripts

| Script           | Purpose                                                |
| ---------------- | ------------------------------------------------------ |
| `npm start`      | CRA dev server with HMR at `http://localhost:3000`     |
| `npm test`       | Interactive Jest watcher                               |
| `npm run build`  | Production build to `build/`                           |
| `npm run eject`  | Eject CRA config (one-way!)                            |

## How This Repo Fits the AgendaKota Project

Across the AgendaKota internship work there are two patterns:

1. **Monorepo (`projectmagang`)** — a single React app with five modules (`tentangkami`, `fitur`, `biaya`, `klinik`, `hubungikami`) plus a Strapi CMS. This is where the working implementations live.
2. **Per-page repos** — `…_klinikpage`, `…_fiturpage`, `…_harga` (this). Spun out so each page can be deployed independently (e.g., separate Netlify/Vercel deployments per page).

If you're looking at this repo and wondering "where's the actual code?" the short answer is: it hasn't been moved over yet. Track the [Roadmap](#roadmap) section below.

## Roadmap

- [ ] Port `projectmagang/src/modules/biaya/` into this repo's `src/`.
- [ ] Add TailwindCSS (mirror the setup in `…_klinikpage`).
- [ ] Build / re-use a real `PricingSection` driven by data (e.g., monthly vs. yearly plans).
- [ ] Wire the page to the shared Strapi CMS in `projectmagang/strapi/` (content type: `cta`, plus a new `pricing` type if needed).
- [ ] Modernize `src/index.js` to use `createRoot` (React 18 API) instead of `ReactDOM.render`.
- [ ] Add a deploy workflow (Netlify / Vercel / GitHub Pages).
- [ ] Add basic SEO meta tags (`react-helmet-async`) and Open Graph.

## Code Review Notes

Since this repo is still the CRA scaffold, the review is necessarily light:

1. **Package name** — `"biayalanpage"`. A typo of "biaya-landing-page"? Consider renaming to `agendakota-biaya` for clarity. Not user-visible since `package.json` `"private": true`, but a clean name helps when grepping logs.
2. **No production source yet** — the real Biaya page lives in `projectmagang/src/modules/biaya/`. When porting, also copy `images/`, `layouts/`, and any required entries from `projectmagang/src/utils/menu.js`.
3. **CRA + React 18 pitfall** — when porting code, switch `ReactDOM.render` to `createRoot`:
   ```js
   import { createRoot } from 'react-dom/client';
   createRoot(document.getElementById('root')).render(<React.StrictMode><App /></React.StrictMode>);
   ```
4. **CRA is in maintenance mode** — if you're starting fresh, consider switching to Vite or Next.js. The migration from CRA-on-`react-scripts@5` to Vite is usually a couple of hours and saves significant dev-server time.
5. **Reuse pricing components** — `projectmagang_AgendaKota_klinikpage/src/components/PricingSection.jsx` and `PricingCard.jsx` already exist; extract them into a shared package (or copy them in) rather than rebuilding from scratch.
6. **Tests** — `App.test.js` is the CRA default ("renders learn react link"). Replace it once the real `App` is in.

## Screenshots

Reference screenshots from the original README (intended page design — not what the current CRA scaffold renders):

- ![Biaya — section 1](https://github.com/user-attachments/assets/fa94ccb3-df2e-4c80-ac92-d504b1c565cf)
- ![Biaya — section 2](https://github.com/user-attachments/assets/2a6a96a7-8d0b-4daf-8795-84a327910572)

## License

No `LICENSE` file is present. Treat the contents as **All Rights Reserved** until one is added. Intended for internship / academic use.
