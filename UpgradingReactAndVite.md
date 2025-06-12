# Migration Guide: React 18 + Create React App to Vite

This document outlines the steps required to migrate our application from React 17 with Create React App (CRA) to React 18 with Vite. All commands should be run from the client directory, and all file modifications should be made to files within the client directory.

## React 18 Upgrade

### 1. Update React Dependencies

```bash
# Update React core packages
npm install react@^18 react-dom@^18 @types/react@^18 @types/react-dom@^18
```

### 2. Update Testing Libraries

```bash
# Update React Testing Library
npm install --save-dev @testing-library/react@13.4.0
```

### 3. Update ReactDOM Import and Rendering Method

The main change in React 18 is the new root API. We updated our `index.tsx` to use the new API:

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

// New React 18 way
import ReactDOM from 'react-dom/client';
// ...
const rootElement = document.getElementById('root') as HTMLElement;
const root = ReactDOM.createRoot(rootElement);

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
npm uninstall react-scripts
```


### 2. Update Node Types for Compatibility with Vite

```bash
npm install --save-dev @types/node@latest
```

### 3. Install Vite and Required Plugins

```bash
npm install --save-dev vite @vitejs/plugin-react vite-tsconfig-paths vite-plugin-node-polyfills
```

### 4. Create Vite Configuration File

Create `vite.config.mjs` in the client directory:

```javascript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import { nodePolyfills } from 'vite-plugin-node-polyfills';
import { fileURLToPath } from 'url';
import { dirname, resolve } from 'path';

const __filename = fileURLToPath(import.meta.url);
const __dirname = dirname(__filename);

export default defineConfig({
  plugins: [
    react(),
    nodePolyfills({
      // Whether to polyfill `node:` protocol imports
      protocolImports: true,
    }),
  ],
  resolve: {
    alias: {
      'src': resolve(__dirname, 'src')
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
  }
});
```

### 5. Create HTML Entry Point

Create `index.html` in the client root directory:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" href="/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Immersive Player</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/index.tsx"></script>
  </body>
</html>
```

### 6. Update Package.json Scripts

Replace CRA scripts with Vite commands:

```json
"scripts": {
  "dev:client": "vite",
  "start": "vite",
  "build": "npm i --production=false && vite build",
  "build-dev": "vite build --mode development",
  "auto-build": "vite build --watch",
  "preview": "vite preview",
  "test": "vitest run"
}
```

### 7. Set Up Testing with Vitest

```bash
# Install Vitest and related packages
npm install --save-dev vitest jsdom
```

Create `vitest.config.ts` file:

```typescript
import { defineConfig } from 'vitest/config';
import react from '@vitejs/plugin-react';
import tsconfigPaths from 'vite-tsconfig-paths';

export default defineConfig({
  plugins: [react(), tsconfigPaths()],
  test: {
    globals: true,
    environment: 'jsdom',
    setupFiles: './src/setupTests.ts',
  },
});
```
