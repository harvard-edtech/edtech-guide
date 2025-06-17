# Uploading IC Test Videos

### A. Turn on Opencast Dev 10

If you have your own way to turn on the opencast-dev-10 instance (immersive-oc-ecs), feel free to use your way.

1. Open the top-level folder for IC in the terminal
2. Run `npm run dev:wizard`
3. Choose "Related Instances" and turn it on

Wait around 30min for the instance to come online.

### B. Pull test updates

1. Open the top-level folder for the Katalon tests (folder should be named "immersive-classroom-tests") in Terminal
2. Run `git pull`

### C. Open the tests in Katalon

1. Open Katalon
2. Open the "immersive-classroom-tests" project
3. Under Test Suites, select the "All Tests" suite
4. Near the top, use the dropdown to select the appropriate profile (ticket will define this)

### D. Run the test suite

1. Use the dropdown next to the play button to select a browser
2. Keep track of which tests fail
