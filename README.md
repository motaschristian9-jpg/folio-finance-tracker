# Folio — Offline personal finance

A mobile-first installable PWA with React, Vite, and **SQLite (sql.js WebAssembly)** persisted in **IndexedDB**. No account, no API, no server-side database.

## Features
- Dashboard with balance, monthly income/expenses, spending donut
- Add/edit/delete income and expense transactions
- Search and filter activity
- Monthly category budgets with progress
- Savings goals with editable saved amount
- Six-month chart, light/dark theme, currency selection
- Export/restore real SQLite `.sqlite` database files
- Install from Chrome; works offline after the first successful online load and cache warm-up

## Deploy from a phone
1. Download and unzip the project. Upload its **contents** to a new GitHub repository using GitHub's web interface (or a phone Git client). Do not upload `node_modules`.
2. On [vercel.com](https://vercel.com), import the repository.
3. Framework: **Vite**; Build command: `npm run build`; Output directory: `dist`.
4. Deploy. Open the HTTPS URL in Chrome. After it loads, use Chrome menu → **Add to Home screen** or **Install app** (depending on browser/device).
5. Open it once online and allow the page to finish loading before going offline.

Local development: `npm install` then `npm run dev`.

## Data and limitations
- SQLite runs **in the browser**, not on Vercel. The database file is stored in IndexedDB for that browser and origin.
- No cross-device sync. Export a backup from Settings regularly; clearing site data or removing the app can erase everything.
- Currency changes **labels only**; no exchange-rate conversion.
- Budgets reset their spending calculation by calendar month. Savings progress is edited manually, not deducted from transaction balance.
- An installed PWA can only work offline once its JS, CSS and WASM assets have been loaded and cached. Service worker registration and installation depend on browser support and HTTPS.
- No authentication or server means anyone with access to the unlocked device/browser profile may access the data.

## Design & architecture
The app follows a simple action-first UI with accessible labels, reduced-motion support, clear empty states, responsive mobile bottom navigation, and short copy. SQLite queries live in `src/db.js`; UI lives in `src/main.jsx`; tokens and responsive styles live in `src/style.css`. Product and architecture notes are in `docs/`.
