# Migration Guide: React 19 + Create React App to Vite

This document outlines the steps required to migrate our application from React 17 with Create React App (CRA) to React 19 with Vite. All commands should be run from the client directory, and all file modifications should be made to files within the client directory.

## Prerequisites

Current versions of Vite require Node 20.19+ or 22.12+. Check your version with `node -v` and upgrade Node first if needed.

## React 19 Upgrade

### 1. Update React and Related Dependencies

React, fortawesome, and the testing libraries all have peer dependencies on each other, so upgrading any one of them on its own fails with an `ERESOLVE` error. Upgrade them all in a single command:

```bash
npm install "react@^19" "react-dom@^19" "@types/react@^19" "@types/react-dom@^19" "@fortawesome/fontawesome-svg-core@latest" "@fortawesome/free-brands-svg-icons@latest" "@fortawesome/free-regular-svg-icons@latest" "@fortawesome/free-solid-svg-icons@latest" "@fortawesome/react-fontawesome@latest" "@testing-library/react@latest" "@testing-library/dom@latest" "@testing-library/jest-dom@latest" "@testing-library/user-event@latest"
```

Before running it, edit the command for your project:
- **fortawesome:** only include the `@fortawesome/*` packages your project already uses (React 19 needs 6.7.2 or higher). Remove them all if your project doesn't use fortawesome.
- **Testing libraries:** `@testing-library/react` v16+ no longer bundles `@testing-library/dom`, so it must be installed alongside it. `@testing-library/jest-dom` v6+ is needed for Vitest support later on. Remove `@testing-library/user-event` if your project doesn't use it.
- **Other React libraries:** if the command still fails with `ERESOLVE`, the error names another dependency (e.g. `react-bootstrap`, `react-router-dom`, `react-select`) that doesn't support React 19 at the version you have. Add `<package>@latest` for it to the same command and run it again, rather than using `--force` or `--legacy-peer-deps`. You can see which packages depend on React with `npm ls react`.

The command doesn't use `--save` or `--save-dev`: npm keeps packages that are already in `package.json` in their current section.

### 2. Double-Check Icon Spacing

Skip this step if your project doesn't use fortawesome.

Installing fortawesome `@latest` brings in Font Awesome 7, which changed how icons are sized and spaced. Most notably, icons are now fixed width by default. As a result, icons next to text may have more space around them than before, and any custom margins or `fixedWidth` props you added to line icons up may no longer be needed.

Once the app is running, click through the pages that use icons (buttons, nav bars, lists, tables) and compare them with how they looked before the upgrade. To find every icon in the code:

```bash
grep -rn "FontAwesomeIcon" src
```

Fix any icons that look off, for example by removing extra margins or `fixedWidth` props that are now redundant.

### 3. Run the React 19 Codemods

React 19 removes several deprecated APIs (`propTypes` and `defaultProps` on function components, string refs, legacy context, `react-dom/test-utils`), and `@types/react@19` changes some types (e.g. `useRef()` now requires an argument, and the global `JSX` namespace is now `React.JSX`). Run the official codemods to fix most of these automatically:

```bash
npx codemod@latest react/19/migration-recipe
```

```bash
npx types-react-codemod@latest preset-19 ./src
```

Review the changes with `git diff` afterwards, and fix any remaining TypeScript errors by hand.

### 4. Update ReactDOM Import and Rendering Method

`ReactDOM.render` has been removed in React 19. Update `index.tsx` to use the root API:
```tsx
// Old React 17 way
import ReactDOM from 'react-dom';
// ...
ReactDOM.render(
  <React.StrictMode>
    <AppWrapper>
      <App />
    </AppWrapper>
  </React.StrictMode>,
  document.getElementById('root')
);

// New React 19 way
import { createRoot } from 'react-dom/client';
// ...
const rootElement = document.getElementById('root') as HTMLElement;
const root = createRoot(rootElement);
root.render(
  <React.StrictMode>
    <AppWrapper>
      <App />
    </AppWrapper>
  </React.StrictMode>,
);
```

## Create React App to Vite Migration

### 1. Uninstall Create React App
```bash
npm uninstall --save react-scripts
```

`react-scripts` also provided the `react-app` ESLint config. If your `.eslintrc.js` (or the `eslintConfig` field in `package.json`) extends `react-app` or `react-app/jest`, remove those entries or ESLint will fail to start. You can also delete the `eslintConfig`, `jest`, and `browserslist` fields from `package.json` if present, since nothing uses them anymore.

### 2. Update Node Types for Compatibility with Vite
```bash
npm install --save-dev @types/node@latest
```

### 3. Install Vite and Required Plugins
```bash
npm install --save-dev vite @vitejs/plugin-react vite-tsconfig-paths vite-plugin-node-polyfills vite-plugin-svgr vitest jsdom
```

### 4. Ignore vite.config.mjs from ESLint

Add the following to your `.eslintrc.js` file (merge it into the existing `ignorePatterns` if there already is one):
```js
  ignorePatterns: [
    'vite.config.*',
  ],
```

### 5. Create Vite Configuration File

Create `vite.config.mjs` in the client directory. This one file configures both Vite and Vitest (tests), so aliases and plugins apply in both places:

```javascript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import tsconfigPaths from 'vite-tsconfig-paths';
import svgr from 'vite-plugin-svgr';
import { nodePolyfills } from 'vite-plugin-node-polyfills';
import { fileURLToPath } from 'url';

export default defineConfig({
  plugins: [
    react(),
    // Supports absolute imports configured in tsconfig.json (e.g. "baseUrl": "src")
    tsconfigPaths(),
    // Allows importing SVGs as React components with `?react`
    svgr(),
    nodePolyfills({
      // Whether to polyfill `node:` protocol imports
      protocolImports: true,
    }),
  ],
  resolve: {
    alias: {
      'src': fileURLToPath(new URL('./src', import.meta.url)),
    },
  },
  server: {
    port: 3000,
    open: false,
    proxy: {
      '/api': {
        target: 'http://localhost:8080',
        changeOrigin: true,
      }
    }
  },
  build: {
    outDir: 'build',
  },
  test: {
    globals: true,
    environment: 'jsdom',
    setupFiles: './src/setupTests.ts',
  },
});
```

Adjust the following for your project:
- **Proxy:** CRA configured the dev proxy with the `"proxy"` field in `package.json`. Use that value as the `target` above, then delete the `"proxy"` field.
- **Base path:** if `package.json` has a `"homepage"` field (i.e. the app is served from a subpath), set Vite's `base` option to that path and delete the `"homepage"` field.

### 6. Create HTML Entry Point

Move `index.html` from the `public` folder to the client root directory. Make sure no `index.html` remains in `public`: Vite copies everything in `public` into the build output, where it would clash with the generated `index.html`.

```bash
git mv public/index.html index.html
```

Then update the moved file:
1. Replace any `%PUBLIC_URL%` references with nothing (e.g. `%PUBLIC_URL%/favicon.ico` becomes `/favicon.ico`)
2. Add the script tag for the main entry point inside `<body>`

Example (use your own app's title and description):
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" href="/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="theme-color" content="#000000" />
    <meta name="description" content="Hello Harvard: a system for getting your course set up" />
    <link rel="apple-touch-icon" href="/logo192.png" />
    <link rel="manifest" href="/manifest.json" />
    <title>Hello Harvard</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/index.tsx"></script>
  </body>
</html>
```

### 7. Update Environment Variables

CRA exposes environment variables as `process.env.REACT_APP_*`. Vite only exposes variables prefixed with `VITE_`, through `import.meta.env`. Code that still reads `process.env.REACT_APP_*` will silently get `undefined`.

1. In every `.env*` file, rename `REACT_APP_` variables to `VITE_` (e.g. `REACT_APP_API_URL` becomes `VITE_API_URL`)
2. In code, replace the references:

| CRA | Vite |
| --- | --- |
| `process.env.REACT_APP_API_URL` | `import.meta.env.VITE_API_URL` |
| `process.env.NODE_ENV === 'production'` | `import.meta.env.PROD` |
| `process.env.NODE_ENV === 'development'` | `import.meta.env.DEV` |
| `process.env.PUBLIC_URL` | `import.meta.env.BASE_URL` |

You can find all the places to change with:

```bash
grep -rn "process.env" src
```

### 8. Update SVG Component Imports

CRA let you import an SVG as a React component with `ReactComponent`. This doesn't work in Vite. Use the `?react` suffix instead (provided by `vite-plugin-svgr`):

```tsx
// Old CRA way
import { ReactComponent as Logo } from './logo.svg';

// New Vite way
import Logo from './logo.svg?react';
```

Plain SVG imports that are used as an image URL (`import logo from './logo.svg'`) don't need to change.

### 9. Update Package.json Scripts

Replace the CRA scripts (`react-scripts start`, `react-scripts build`, `react-scripts test`, `react-scripts eject`) with Vite commands:
```json
"scripts": {
  "dev:client": "vite",
  "start": "vite",
  "build": "npm i --include=dev && vite build",
  "build-dev": "vite build --mode development",
  "auto-build": "vite build --watch",
  "preview": "vite preview",
  "test": "vitest run"
}
```

### 10. Replace `react-app-env.d.ts`

The old file references `react-scripts`, which is no longer installed, and TypeScript will error on it. Delete `src/react-app-env.d.ts` and create `src/vite-env.d.ts`:

```ts
/// <reference types="vite-plugin-svgr/client" />
/// <reference types="vite/client" />
/// <reference types="vitest/globals" />

// Allow SCSS imports
declare module '*.scss';
```

`vite/client` already provides types for SVG, image, and CSS module imports as well as `import.meta.env`, so don't redeclare `*.svg` yourself. `vitest/globals` provides types for `describe`, `it`, `expect`, etc. in tests. The `vite-plugin-svgr/client` line must come before `vite/client`.

### 11. Update Tests for Vitest

Vitest is mostly compatible with Jest, but a few changes are needed:

1. In `src/setupTests.ts`, replace the jest-dom import:
   ```ts
   // Old
   import '@testing-library/jest-dom';
   // New
   import '@testing-library/jest-dom/vitest';
   ```
2. Replace the `jest` global with `vi` in tests, e.g. `jest.fn()` becomes `vi.fn()`, `jest.mock()` becomes `vi.mock()`, and `jest.spyOn()` becomes `vi.spyOn()`. Find them with:
   ```bash
   grep -rn "jest\." src
   ```
3. Any imports from `react-dom/test-utils` should be changed: `act` is now imported from `react` (the React 19 codemod should have done this).

Then run the tests to make sure they pass:

```bash
npm test
```

### 12. Update SCSS Files: Replace @import with @use

`@import` is deprecated in current versions of Sass and prints a warning for every use. Replace all `@import` statements with `@use` statements in your SCSS files. `@use` must come before any other rules in the file. Variables from `shared.scss` must now be accessed as `shared.$variable-name`, and `math.div` requires `@use 'sass:math';`.

```scss
// Old way with @import
@import './shared.scss';

.my-component {
  color: $primary-color;
  margin: 16px / 2;
}

// New way with @use
@use 'sass:math';
@use './shared.scss';

.my-component {
  color: shared.$primary-color;
  margin: math.div(16px, 2);
}
```
