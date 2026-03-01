<br />
<br />
<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://cdn.builder.io/api/v1/image/assets%2FYJIGb4i01jvw0SRdL5Bt%2F160d3724e72b4f88af781e0887df5601">
    <img alt="Builder.io logo" src="https://cdn.builder.io/api/v1/image/assets%2FYJIGb4i01jvw0SRdL5Bt%2F96fa96f7f5a0415f9dff40b41d78b6a7">
  </picture>
</p>
<h3 align="center">
  Know what your Chrome extensions can access
</h3>
<p align="center">
   Free public scan by URL or extension ID and Check permissions, network access, version history, and known threats
</p>

<p align="center">
  <a href="https://github.com/BuilderIO/builder"><img alt="Repo stars" src="https://img.shields.io/github/stars/BuilderIO/builder?style=flat"></a>
  <a href="https://github.com/prettier/prettier"><img alt="code style: prettier" src="https://img.shields.io/badge/code_style-prettier-ff69b4.svg" /></a>
  <a href="https://github.com/builderio/builder/pulls"><img alt="PRs Welcome" src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" /></a>
  <a href="https://github.com/BuilderIO/builder/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/github/license/BuilderIO/builder" /></a>
  <a href="https://www.npmjs.com/package/@builder.io/sdk"><img alt="Types" src="https://img.shields.io/npm/types/@builder.io/sdk" /></a>
</p>
<br />

<p align="center">
  <img alt="Animation of Builder.io Visual Editor" src="https://github.com/user-attachments/assets/6972696e-bfb5-4c6d-b987-ea6a07816655" >
</p>

## How the Builder.io platform works

Builder connects to your existing site or app, so you can visually edit and generate code using your existing components. Use Figma designs or our drag-and-drop editor. Export your code or publish your updates via our [SDKs](https://www.builder.io/c/docs/developers).

Read more about [How Builder works](https://www.builder.io/c/docs/how-builder-works-technical).

<p align="center">
  <img alt="How it works" src="https://github.com/user-attachments/assets/7ef9ca00-22f2-49b7-9b29-1df1eb7daba7" />
</p>

## Try it out

[Sign up for a free account](https://builder.io/signup) to dive right in. 

## What's in this repository

This repo houses all of the various [SDKs](packages), [usage examples](examples), [starter projects](starters), and [plugins](plugins).

## Join the community

Questions, requests, or feedback? Chat with us on the [Builder.io Forum](https://forum.builder.io).

## We're hiring!

Help us enable anyone to build digital experiences and bring more ideas to life. [View openings](https://www.builder.io/m/careers) now.


## Frontend Overview

ExtensionScanner’s frontend is a **React single-page application** built with **Vite** and **Tailwind CSS**, designed to provide a fast, responsive UI for scanning and inspecting browser extensions.

- **Build tool**: Vite (`vite`, React plugin)
- **UI framework**: React 18
- **Routing**: `react-router-dom`
- **Head management / SEO**: `react-helmet-async`
- **HTTP client**: `axios`
- **UI primitives**: Radix UI (`@radix-ui/react-*`)
- **Icons**: `lucide-react`
- **Styling**: Tailwind CSS 4 + `tailwindcss-animate`, `class-variance-authority`, `tailwind-merge`, `clsx`

At the moment, the repo contains the frontend **tooling and configuration** (Vite, Tailwind, ESLint, PostCSS) and the HTML entrypoint. The actual React `src/` tree will be added as the project is fully open‑sourced.

---

## Project Layout (Frontend)

From the repository root:

- **`frontend/`** – Vite + React frontend
  - **`index.html`** – HTML shell and entrypoint that mounts the React app into `#root` and loads `src/main.jsx`.
  - **`public/`**
    - `robots.txt` – search engine crawling rules.
    - `sitemap.xml` – public sitemap for the marketing / app pages.
    - `vite.svg`, `world-map.svg` – static assets.
  - **`vite.config.js`** – Vite configuration and dev server proxy to the backend.
  - **`tailwind.config.js`** – Tailwind CSS configuration and content paths.
  - **`postcss.config.js`** – PostCSS pipeline (Tailwind + Autoprefixer).
  - **`eslint.config.js`** – Linting rules for the React codebase.
  - **`scripts/generate-sitemap.js`** – Node script to regenerate `sitemap.xml` before builds.
  - **`package.json` / `package-lock.json`** – Node dependencies and scripts.

> Note: The future `frontend/src/` directory will contain all React components, pages, hooks, and routing configuration. The HTML template already points to `src/main.jsx`.

---

## Tooling & Dependencies

### NPM Scripts

Defined in `frontend/package.json`:

- **`npm run dev`** – Start the Vite dev server (hot-reloading React app).
- **`npm run build`** – Run `generate:sitemap` then build the production bundle via Vite.
- **`npm run preview`** – Serve the production build locally using Vite’s preview server.
- **`npm run lint`** – Run ESLint against the frontend.
- **`npm run format`** – Format source files using Prettier.
- **`npm run format:check`** – Check formatting without writing changes.
- **`npm run generate:sitemap`** – Execute `scripts/generate-sitemap.js` to update `public/sitemap.xml`.

### Runtime Libraries

- **React / ReactDOM** – Core UI rendering.
- **React Router (`react-router-dom`)** – Client-side routing and navigation.
- **React Helmet Async (`react-helmet-async`)** – Dynamic document head management (titles, meta tags, canonical links).
- **Axios** – Promise-based HTTP client for talking to the backend API under `/api`.
- **Radix UI**:
  - `@radix-ui/react-dialog` – Modal dialogs.
  - `@radix-ui/react-dropdown-menu` – Menus for user actions and context menus.
  - `@radix-ui/react-select` – Accessible select controls.
  - `@radix-ui/react-tabs` – Tabbed interfaces for switching between views.
  - `@radix-ui/react-tooltip` – Tooltips for affordances and extra info.
- **lucide-react** – Icon set used throughout the UI.

### Styling & Design System

- **Tailwind CSS** – Utility-first styling.
- **tailwindcss-animate** – Animation utilities built on top of Tailwind.
- **class-variance-authority** – Pattern for defining “variant-aware” components (e.g., button sizes/variants).
- **tailwind-merge** – Safely merges Tailwind class strings, used when composing classes dynamically.
- **clsx** – Conditional className builder.

---

## Vite Configuration & Backend Integration

The Vite config (`frontend/vite.config.js`) wires up React and proxies API calls:

- **React plugin**: `@vitejs/plugin-react` enables fast refresh and JSX/TSX.
- **Dev server proxy**:
  - Requests to paths starting with **`/api`** are proxied to `http://localhost:8007`.
  - `changeOrigin: true` ensures the Host header is rewritten, which helps with some backend setups.

**Implications for frontend code:**

- In development, you can call the backend via relative paths like `axios.get('/api/scan/...')` without worrying about CORS.
- In production, the frontend should be served behind the same origin as the backend (or with an equivalent reverse proxy) so that `/api` continues to resolve correctly.

---

## Tailwind & Global Styles

`tailwind.config.js`:

- **`content`**:
  - `./index.html`
  - `./src/**/*.{js,ts,jsx,tsx}`
- **`plugins`**:
  - `tailwindcss-animate`

This means:

- Tailwind will scan **all JSX/TSX files under `src/`** plus the root `index.html` for class usage.
- Any new React component you add under `src/` will automatically participate in Tailwind’s JIT compilation, as long as it uses Tailwind class names.

Global font setup is defined in `index.html`:

- Uses **Instrument Serif** and **JetBrains Mono** from Google Fonts.
- The React root is mounted into `<div id="root"></div>`.

---

## Linting & Code Quality

ESLint is configured in `eslint.config.js` using the modern flat config:

- **Base config**: `@eslint/js` recommended rules.
- **React hooks**: `eslint-plugin-react-hooks` with `recommended-latest`.
- **React Refresh**: `eslint-plugin-react-refresh` with `vite` config (ensures components play nicely with fast refresh).
- **Environment**:
  - `globals.browser` so common browser globals (e.g. `window`, `document`) are recognized.
  - ECMAScript latest + JSX enabled.
- **Custom rules**:
  - `'no-unused-vars': ['error', { varsIgnorePattern: '^[A-Z_]' }]`
    - Allows “constant-like” variables (e.g. `FOO_BAR`) to be unused without throwing an error, which is convenient for static config objects or enum-like constants.

Run linting locally via:

```bash
cd frontend
npm run lint
```

---

## Local Development Workflow

1. **Install dependencies**

   ```bash
   cd frontend
   npm install
   ```

2. **Start the backend API**

   - Ensure the Python backend is running on `http://localhost:8007` (the dev proxy target).
   - If you change the backend port, update `vite.config.js` accordingly.

3. **Run the frontend dev server**

   ```bash
   npm run dev
   ```

   - By default, Vite runs on `http://localhost:5173` (or the next available port).
   - All calls to `/api/...` from the browser will be proxied to the backend.

4. **Build for production**

   ```bash
   npm run build
   ```

   - This will:
     - Regenerate `public/sitemap.xml` via `scripts/generate-sitemap.js`.
     - Output a production-optimized bundle in `dist/`.

5. **Preview the production build**

   ```bash
   npm run preview
   ```

---

## React App Architecture (Planned)

While the repository does not yet include the `src/` directory, the dependencies and tooling hint at the intended architecture:

- **Entry point**: `src/main.jsx`
  - Mounts the React app into `#root`.
  - Wraps the app with routers and providers (e.g., `BrowserRouter`, `HelmetProvider`).
- **Routing**: `react-router-dom`
  - The app is likely organized into route-based pages (e.g., dashboard, extension details, organization policy views).
  - Use nested routes and layout components for shared chrome (top nav, sidebars, etc.).
- **Head management**: `react-helmet-async`
  - Each page can set its title and meta tags for better SEO and social previews.
- **UI components**:
  - Radix primitives form the base for dialogs, dropdowns, selects, tabs, and tooltips.
  - Tailwind + class-variance-authority enforce consistent styling across components.
  - lucide-react provides consistent iconography.

When the `src/` tree is available, this document can be extended with:

- A **routes map** (paths → components).
- A **components hierarchy** (core shared components vs. feature-specific components).
- **State management** patterns (e.g., hooks for fetching data, caching, and error handling).

---

## API Usage Patterns (Frontend)

Given the `/api` proxy and `axios` dependency, the frontend is expected to:

- Use `axios` instances configured with:
  - `baseURL: '/api'` for all HTTP calls.
  - Interceptors for auth headers and error handling (e.g., global toasts, logging).
- Call endpoints such as:
  - `GET /api/extensions/:id` – fetch details about a specific browser extension.
  - `POST /api/scan` – trigger a new scan by extension ID, store URL, or manifest.
  - `GET /api/scans/:id` – retrieve scan reports and risk scores.

The exact endpoint set lives in the backend; the frontend should keep API interactions encapsulated in a small number of modules (e.g. `src/api/client.ts`, `src/api/extensions.ts`) to keep the rest of the UI decoupled from HTTP details.

---

## Conventions & Best Practices

Once the `src/` tree is present, aim to follow these conventions:

- **File structure**
  - Group by **feature** (e.g., `src/features/extensions`, `src/features/scans`) rather than by type.
  - Keep shared primitives in something like `src/components/ui`.
- **Components**
  - Prefer functional components with hooks.
  - Co-locate component styles, tests, and stories (if using Storybook) with the component.
- **Styling**
  - Tailwind classes for layout and spacing.
  - `cva` for reusable, variant-based component styling (buttons, badges, alerts).
  - Use `tailwind-merge` and `clsx` to compose `className` props safely.
- **Accessibility**
  - Leverage Radix primitives for accessible interactions (modals, tooltips, menus).
  - Always provide labels and ARIA attributes on interactive elements.
- **Networking**
  - Centralize axios configuration.
  - Avoid calling `axios` directly from deeply nested components; instead, use custom hooks or API utility modules.

---

## Extending the Frontend

When adding new features:

1. **Create a feature folder** under `src/features/` (or equivalent).
2. **Add routes** via `react-router-dom` and link them from existing navigation.
3. **Use shared primitives** (buttons, inputs, dialogs) rather than re‑creating UI from scratch.
4. **Respect API boundaries**: add new endpoints to the dedicated API modules, keep types and response shapes documented near those modules.
5. **Update SEO** via `react-helmet-async`:
   - Unique page titles.
   - Relevant description meta tags.

As the repository evolves and the full frontend source is published, this document can be expanded with concrete examples and code references.



