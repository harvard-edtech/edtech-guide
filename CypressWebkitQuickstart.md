<!-- ──────────────────────────────────────────────────────────────────── -->
<!--                 Experimental WebKit Guide for Cypress                -->
<!-- ──────────────────────────────────────────────────────────────────── -->


# Experimental WebKit Support with Cypress  
Last updated 2025-06-12.


# Table of Contents  
- [Prerequisites](#prerequisites)  
- [Enable WebKit in cypress.config.js](#enable-webkit-in-cypressconfigjs)  
- [Install the Playwright WebKit Engine](#install-the-playwright-webkit-engine)  
- [Launch & Verify](#launch--verify)  
- [Known Limitations](#known-limitations)

## Prerequisites
You already have a working local Cypress environment (VSCode or another IDE) and can run normal Chromium/Firefox tests.

## Enable WebKit in cypress.config.js
Open `cypress.config.js` and turn on the `experimentalWebKitSupport` flag in the `e2e` section of the file:


~~~js
const { defineConfig } = require('cypress');

module.exports = defineConfig({
  e2e: {
    setupNodeEvents(on, config) {
      // implement node event listeners here
    },

    /* ─── ADD THIS LINE ─── */
    experimentalWebKitSupport: true,
  },
});
~~~

## Install the Playwright WebKit Engine
Cypress delegates WebKit automation to the Playwright runner.

~~~bash
npm install --save-dev playwright-webkit
~~~

## Launch & Verify
1. Run `npm run cypress`.  
2. Choose “End-to-End Testing”.  
3. In the browser list you should now see **WebKit** alongside Chrome/Firefox/Electron.

If WebKit is missing, re-check:  
– the `experimentalWebKitSupport` flag,  
– that `node_modules/playwright-webkit` exists, and  

## Known Limitations
The experimental driver is **NOT** feature-complete. Plan tests accordingly.

~~~text
• cy.origin()                               – unsupported
• cy.intercept({ forceNetworkError })       – ignored
• experimentalSingleTabRunMode + video      – records only first spec
• cy.type() differences
    – textInput events lack data
    – beforeinput events lack inputType
    – Up/Down arrow on <input type="number"> does not step
• Stack traces may omit function names / locations
~~~

Check this github issue page for a complete list of bugs: [Issues](https://github.com/cypress-io/cypress/issues?q=is%3Aissue+is%3Aopen+sort%3Aupdated-desc+label%3A%22experiment%3A+webkit%22)
