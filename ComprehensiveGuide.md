# Comprehensive EdTech Development Guide

Last updated by Gabe Abrams in 2025. This will probably be out of date within minutes of this guide being published. Be alert and be flexible.

<style>
  /* Rule element for team rules */
  Rule {
    display: block;
    font-weight: bold;
    color: #CB3048;

    border: 0.15rem solid #CB3048;
    border-top-left-radius: 0.3rem; border-top-right-radius: 0.3rem;

    padding-top: 0.2rem;
    padding-bottom: 0.2rem;
    padding-left: 0.5rem;
    padding-right: 0.5rem;
  }
  Rule::before {
    content: '\2605  Rule: ';
    font-weight: normal;
  }
  
  /* <Rule tall> for rules that don't have a following pre with explanation */
  Rule[tall] {
    margin-bottom: 0.7rem;
    border-bottom-left-radius: 0.3rem;
    border-bottom-right-radius: 0.3rem;
  }

  /* Extend rule border around following pre with explanation */
  Rule + .highlighter-rouge pre {
    border-bottom: 0.15rem solid #CB3048;
    border-left: 0.15rem solid #CB3048;
    border-right: 0.15rem solid #CB3048;

    border-top-left-radius: 0 !important;
    border-top-right-radius: 0 !important;
    border-bottom-left-radius: 0.3rem;
    border-bottom-right-radius: 0.3rem;
  }

  /* Exercise block with an assignment */
  Exercise {
    display: block;
    font-weight: bold;
    color: #54d2e2;

    background-color: white;
    position: relative;
    z-index: 10;

    border: 0.15rem solid #54d2e2;
    border-top-left-radius: 0.3rem; border-top-right-radius: 0.3rem;

    padding-top: 0.2rem;
    padding-bottom: 0.2rem;
    padding-left: 0.5rem;
    padding-right: 0.5rem;
  }
  Exercise::before {
    content: '\270F  Exercise: ';
    font-weight: normal;
  }

  /* <Exercise tall> for exercises that aren't followed by a pre with explanation */
  Exercise[tall] {
    margin-bottom: 0.7rem;
    border-bottom-left-radius: 0.3rem;
    border-bottom-right-radius: 0.3rem;
  }

  /* Extend exercise border around following pre with explanation */
  Exercise + .highlighter-rouge pre {
    border-bottom: 0.15rem solid #54d2e2;
    border-left: 0.15rem solid #54d2e2;
    border-right: 0.15rem solid #54d2e2;

    border-top-left-radius: 0 !important;
    border-top-right-radius: 0 !important;
    border-bottom-left-radius: 0.3rem;
    border-bottom-right-radius: 0.3rem;
  }

  /* Example response extend below exercise as a visual add-on */
  details {
    margin-left: 1em;
    margin-right: 1em;

    position: relative;

    transform: translate(0, -1rem);

    padding-left: 0.5rem;
    padding-right: 0.5rem;
    padding-top: 0.3rem;
    padding-bottom: 0.3rem;
    
    background-color: #54d2e2;

    border-bottom: 0.15rem solid #54d2e2;
    border-left: 0.15rem solid #54d2e2;
    border-right: 0.15rem solid #54d2e2;

    border-bottom-left-radius: 0.3rem;
    border-bottom-right-radius: 0.3rem;
  }

  /* Fix spacing below pre inside of example */
  details pre {
    margin-bottom: 0.3rem !important;
  }

  /* Bold, white text for example title */
  summary {
    text-align: center !important;
    font-weight: bold;
    color: white;
  }

  /* Highlight color for code inside of example that's important <b>code</b> */
  details b {
    font-weight: bold;
    color: #d14;
  }

  /* Boxes around main titles */
  h1 {
    border-radius: 0.5rem;
    background-color: #333;
    color: white;
    padding-bottom: 0.5rem;
    padding-left: 0.7rem;
    padding-right: 0.7rem;
    padding-top: 0.5rem;
  }

  /* Hide footer */
  .footer {
    display: none;
  }

  /* Wrap text in text-based pre tags */
  pre[text] {
    white-space: pre-wrap;
  }
</style>

Although everything in this guide should be followed closely, pay special attention to `Rule` blocks, as those are even more non-negotiable.

# Table of Contents

Getting Set Up:

- [Set Up Your Workspace](#set-up-your-workspace)
- [Get Access to Harvard Tools](#get-access-to-harvard-tools)

Team Info:

- [Mission](#mission)
- [Overview of Technologies](#overview-of-technologies)
- [Team Norms](#team-norms)

Programming and Testing:

- [Project and File Management](#project-and-file-management)
- [Typescript Basics](#typescript-basics)
- [Typescript Advanced Stuff](#typescript-advanced-stuff)
- [React](#react)
- [Logging](#logging)
- [Express Server](#express-server)
- [React Component Unit Tests](#react-component-unit-tests)
- [Helper Unit Tests](#helper-unit-tests)
- [Automated UI Testing](#automated-ui-testing)
- [Commonly Used Dependencies](#commonly-used-dependencies)

Creating Projects:

- [Creating React Projects](#creating-react-projects)
- [Creating Component Libraries](#creating-component-libraries)
- [Creating Support Libraries](#creating-support-libraries)

# Set Up Your Workspace

_Note:_ if using windows, start by installing a terminal replacement like Git Bash. It must function like a Mac OS or Linux machine. Otherwise, virtualize Linux.

In each new project, switch to standard unix-style line breaks:

```bash
git config core.autocrlf false 
git rm --cached -r . 
git reset --hard
```

Always make sure your git config is set to detect case-sensitive filename changes:

```bash
git config --global core.ignorecase false
```

## Typescript

Javascript environment:

1. Install NVM
1. Install Node.js LTS via NVM

NPM setup

1. Install npx using `npm i -g npx`

<Exercise>
  Check your Node setup
</Exercise>

```bash
# Open terminal, check the version you're running:
username@MyLaptop % node --version
x.x.x

# Change to a different version of node
username@MyLaptop % nvm use 16

# Make sure the version switched
username@MyLaptop % node --version
16.x.x

# Switch back to the current version
username@MyLaptop % nvm use default

# Open the Node interpreter
username@MyLaptop % node

# Test Node operations
Welcome to Node.js v18.15.0.
Type ".help" for more information.
> console.log(10 + 5);
15
> const name = 'Divardo';
Divardo
> 
```

## Code Editor

Install required VSCode extensions:

1. `Code Spell Checker` by Street Side Software - flags spelling errors in your code
1. `ESLint` by Microsoft - required for eslint enforcement
1. `TODO Highlight` by Wayou Liu (alternative is okay) - highlights TODOs

Remove banned extensions or disable them on all our projects:

1. `Prettier` - formats in ways that do not necessarily follow our rules

If you want, install optional VSCode extensions:

1. `Path Intellisense` by Christian Kohler - helps auto-complete local imports
1. `npm Intellisense` by Christian Kohler - helps auto-complete lib imports
1. `gitignore` by michelemelluso - right click and add to gitignore
1. `Thunder Client` by Ranga Vadhineni - lets you easily send api requests for testing
1. `Duplicate action` by mrmlnc - lets you easily duplicate files
1. `vscode-icons` by vscodeicons.team - makes folders much more visual in the file tree

Update these VSCode settings:

1. Change "EOL" style to "\n" (LF)
1. Use two spaces instead of tabs
1. Emmet: Show Expanded Abbreviation = inMarkupAndStylesheetFilesOnly
1. Turn on "Bracket Pair Colorization"
1. Typescript Preferences > Quote Style = "single"

Troubleshooting ESLint:

If eslint isn't working on the project, first try reinstalling it: Shift + CMD/Ctrl + P > Reinstall Extension > ESLint.

If that doesn't fix it, try the solutions in this [ESLint Troubleshooting Checklist](https://dev.to/tillsanders/eslint-not-working-in-vscode-help-build-a-troubleshooting-checklist-fdc).

If opening the project in VSCode, try only opening the project itself (not a parent directory).

## Set Up a Sandboxes

### Typescript Sandbox

1. Create a folder on your machine, call it `ts-sandbox`
1. Visit the folder in terminal and run `npm init -y` (don't add the "-y" except for creating sandboxes)
1. Run `npm init dce-eslint@latest` and confirm to set up eslint
1. Install node types by running `npm install --save-dev @types/node`
1. Open the `.eslintrc` file and remove the following lines: `'react-app',` and `'react-app/jest',` under the `extends` section
1. Create a `tsconfig.json` file in the top directory and paste in the following content:
    ```json
    {
      "compilerOptions": {
        "target": "es5",
        "lib": [
          "esnext"
        ],
        "allowJs": true,
        "skipLibCheck": true,
        "esModuleInterop": true,
        "allowSyntheticDefaultImports": true,
        "strict": true,
        "forceConsistentCasingInFileNames": true,
        "noFallthroughCasesInSwitch": true,
        "module": "commonjs",
        "moduleResolution": "node",
        "resolveJsonModule": true,
        "isolatedModules": true,
        "noEmit": false,
        "outDir": "./build",
        "rootDir": "./src",
        "removeComments": false,
        "declaration": true
      },
      "include": [
        "src"
      ]
    }
    ```
1. Create a `/src` folder. Note that all your sandbox typescript files should go into this folder

Each time you want to create a new sandbox file, simply go into the `/src` folder and create a new `nameOfFile.ts` file.

To run one of your sandbox files:
1. In the terminal, navigate to the `/src` folder
1. Run `ts-node nameOfFile.ts`

Note: if you get an error saying `ts-node: command not found`, install `ts-node` using `npm install -g ts-node`

### React Sandbox

Visit the [CACCL Docs](https://bit.ly/caccl) and set up a react-based project, using `npm init caccl@latest`.

# Get Access to Harvard Tools

If you don't have a HarvardKey, claim your HarvardKey:

1. Visit the HarvardKey page: [https://key.harvard.edu/](https://key.harvard.edu/)
1. Click "Claim HarvardKey"
1. Follow instructions

Set up Direct Deposit:

1. Make sure you can log into [https://peoplesoft.harvard.edu](https://peoplesoft.harvard.edu)
1. Follow instructions in the "Direct Deposit" PDF that HR sent you via email when you signed paperwork

Become familiar with reporting time via Peoplesoft:

1. Make sure you can log into [https://peoplesoft.harvard.edu](https://peoplesoft.harvard.edu)
1. Follow instructions in the "Reporting Time and Absences" PDF that HR sent you via email when you signed paperwork

Get access to Canvas:

1. Visit Canvas [https://canvas.harvard.edu](https://canvas.harvard.edu)
1. Log in
1. If you get an error message, contact Gabe and they will help you continue. If you are able to get in, you're all set

Generate a Canvas access token:

1. Visit Canvas [https://canvas.harvard.edu](https://canvas.harvard.edu)
1. Click your profile image
1. Click "Settings"
1. Scroll down and click "+ Access Token"
1. Set the purpose to "DCE EdTech Testing" and set the expiry date for the end date of your employment term with DCE
1. Copy down the access token into a secure place (on mac, I recommend using notes in the built-in keychain app, otherwise a password manager will do)

Get access to the team slack:

1. Send Gabe your preferred slack email address and they will add you

Get access to GitHub projects:

1. Send Gabe your GitHub handle and they will add you to the appropriate projects

# Mission

Everything we do will be aligned with our mission. The skills we develop, the projects we work on, and the designs we create will all be informed by and aligned with our mission.

What is a mission? It is something to _align_ your work with. It is not something that we expect to achieve, but rather, something that we expect to move toward. We think of our mission more as a _direction_ than a _mandate_. 

## 1. Inclusive and Flexible

Focus on diversity, equity, inclusion, and belonging: build tools that use inclusive language, foster a sense of belonging, and empower users to be themselves.

Advance accessibility and improve access: meet and exceed accessibility standards, provide solutions for people with mobile devices, and prepare for weak internet connections and slow devices. Use simple, standard language.

Design for synchronous, asynchronous, in-person, and distance users: incorporate flexible teaching and learning pedagogy into the technology we build.

## 2. Scalable and Self-Service

Support increased scale: build to enable the increasing number of courses and term startups.

Design for self-service administration and support: all admin functionality, debugging, analytics, and tracking must be exposed through a simple and intuitive admin dashboard. Software developers should not be required for diagnosing issues, debugging user behavior, or handling any tool-specific non-bug issues.

Design for self-service usage: teaching team members and students should be able to perform as much as possible on their own before requiring the attention or assistance of a staff member.

Choose efficient and scalable technologies: use simple and scalable technologies, shift as much of the complex logic as possible to the front end.

## 3. Seamless and Intuitive

Always choose the simplest technology: whether it's a small or large library, always choose the simplest tech so we can focus on impact. This helps users understand our tools and helps programmers work on and understand each other's code.

Standardize design and UI: to create a seamless user experience, we will use the same design language and user interface elements across all projects. Gabe oversees the designs and makes sure UI and UX decisions are consistent across all tools. We also design to match the design of 3rd party tools (Canvas, Zoom, etc.) to create a seamless user experience.

Standardize dependencies and libs: every API, every 3rd party tool, and every small dependency should be standardized across all projects. For example, CACCL always handles Canvas integration, ZACCL always handles Zoom integration, and so on. With libraries, we always use the same library for cloning, for example. This reduces cognitive load while reducing app bundle sizes because of merged auto-bundling.

Meet users where they are: always design to meet the user where they are. Have buttons in convenient locations, place relevant actions in locations that will be visible when those actions need to be performed.

Write human-readable error messages and codes: all errors must have both a human-readable error message and a machine-readable error code. Our error messages are written to be short, concise, and not require any technical or domain-level knowledge and definitely do not expose any of the inner workings of our products.

## 4. Informed and Impactful

Know your users: we design our tools for staff, teaching team members, and students. With each project, we'll take time to talk about and learn about our users.

Listen to teaching and learning experts: combine your own passion about education with the expert advice, attention to research, and studies/focus groups that the teaching and learning team conducts. Gabe serves as the team's representative on the teaching and learning team, explaining updates and new findings as they come from the teaching and learning team.

Prioritize impact over tech: we design for impact, we design to improve our courses, help students learn and find community, and help TTMs (Teaching Team Members) teach in exciting and engaging ways. Prioritizing impact over tech means that impact comes first and then we find the technologies that make that impact possible, instead of choosing technologies that we like and then seeing how we can make an impact with them.

Collect data and provide analytics: work to collect data and analytics to help improve our tools and improve our courses, and create dashboards that provide insight to the teaching and learning team. This is important but cannot be an excuse for compromising student safety and privacy.

## Placement for our Mission

Let's take a moment to go over the DCE Senior Leadership Team's DCE-wide list of goals for 2025 and beyond and take a moment with each one to work on placing our work within that greater vision.

The first two parts of the DCE list of goals clearly and directly align with our work:

### A. Build and enhance technology solutions to empower program innovation, and experimentation that can help ensure that DCE remains a leader in open enrollment learning and fosters greater student engagement and success.

### B. Cultivate te a more agile and innovative learning organization at DCE where experimentation and innovation without fear of failure is encouraged and supported.

That said, the rest of the missions also align with our mission. Let me explain one by one:

### C. Build a stronger pipeline of new students to grow enrollments

DCE is working to grow its enrollments, so this is a general mission targeted at increasing the size of our student population, thus increasing our budgets. This mission is broad and covers the DCE marketing team, enrollment services, alumni network, and lots of outreach and community work. Although our work might not obviously fit into the work of recruitment, we do have the ability to make an impact here.

One thing we see over and over again is that, with online eduction, powerful and seamless technologies are becoming the baseline for what students expect. Of course, this connects with our mission: `Seamless and Intuitive`. That said, student's don't stop there; they search for learning environments that give them a sense of community, a sense of belonging, the opportunity to build peer networks, and the feeling that our programs and technologies are human-centered and learning-centered. That is why our `Informed and Impactful` mission is key with this DCE-wide mission. If we can create informed and impactful technologies, students will see that our technologies help them learn and they will return for more classes, tell others about our courses, and will share positive reviews and build the DCE brand. Finally, surveys show that students stick around because they feel a sense of community and purpose. We don't just want students who come for one class and then leave. We want students who feel like they're part of something bigger, students who feel like they belong and are part of our community. Those are the students who come back and grow our enrollments. That's why our `Inclusive and Flexible` mission is so important here.

We advance this DCE-wide mission through our `Seamless and Intuitive`, `Informed and Impactful`, and `Inclusive and Flexible` missions.

### D. Enhance future-focused student-centered engagement philosophy and built strategies to support it for both new and returning students

This DCE-wide mission articulates what is our bread and butter: creating student-centered engagement opportunities that push the envelope of what's possible with technology. We are the EdTech Innovations team and we are a huge part of bringing this DCE-wide mission to life. Our work, partnered with other Teaching and Learning Team work on teaching practice and pedagogy, builds the "strategies" to support new and returning students. In summary, our team exists because of this DCE-wide mission.

We advance this DCE-wide mission through the combination of all of our missions because all of our projects are chosen to advance this mission.

### E. Explore shorter term credit programming with digital badging and micro credentials

This DCE-wide mission focuses on smaller engagement opportunities (weekends, professional development programs, etc.) that require enormous scaling all while maintaining a standard of pedagogy-first design and student-centered engagement. Because these shorter programs happen more frequently and in larger numbers, it becomes really important that we build tools that help with scalability and make self-service more available. For example, instead of three rounds of setting up courses (Spring, Summer, Fall), we might need to set up new courses every few weeks. This is where our `Scalable and Self-Service` mission becomes critical. We simply don't have the staff time to make this new shorter term programming model possible, and so we turn to scaling and self-service.

We advance this DCE-wide mission through our `Scalable and Self-Service` mission.

### F. Recruit and engage FAS (and Harvard) faculty to teach in DCE programs through targeted outreach strategies

This DCE-wide mission aims to make it very appealing for Harvard teachers to join our programs. Other teams at DCE work on outreach. The Teaching and Learning Team is called in once faculty have already decided to join DCE. Our contribution to this mission is to make that onboarding process as easy as possible (our `Seamless and Intuitive` mission), give teachers tools and insight that they don't get at other parts of Harvard (the `Self-Service` part of our `Scalable and Self-Service` mission), tools that help them teach in exciting new ways (our `Informed and Impactful` mission), and give them flexibility to teach how they dream of teaching (the `Flexible` part of `Inclusive and Flexible`).

We advance this DCE-wide mission through our `Scalable and Self-Service`, `Informed and Impactful` and `Inclusive and Flexible` missions.

### G. Utilize Harvard Summer School as an innovation incubator

This DCE-wide mission is pretty simple: the goal is to use our summer programs as an opportunity to test out new teaching practices and tools. We're already doing this because most of our projects start their pilots during the summer.

We advance this DCE-wide mission not through our own missions, but through our piloting schedule and process.

### H. Create and execute an international strategy meant to drive enrollments, increase classroom diversity, and further cultivate a DCE global presence

This DCE-wide mission aims to bring in students across the world, increase our enrollments, and increase classroom diversity. There are two steps to this DCE-wide mission: first, we need to recruit those students and bring them into our programs, second, we need to help those students learn and feel like they belong. The first step is driven by our marketing and enrollment services teams, but the second step is driven by the Teaching and Learning Team and by the tools that we build. In particular, especially with international students, we need tools that are extremely scalable and lightweight (slow internet connections, VPNs), but also self-service so that they can use our tools during hours where our teams are offline, thus calling forth our `Scalable and Self-Service` mission. It's not enough to simply have a more diverse student body. We need to embrace their different time zones, educational backgrounds, identities, cultures, and learning styles. Thus, we build tools that are both `Informed and Impactful` and `Inclusive and Flexible`. 

We advance this DCE-wide mission through our `Scalable and Self-Service`, `Informed and Impactful` and `Inclusive and Flexible` missions.

### I. Identify/create explicit opportunity pairings between academic units (EXT, HSS, PDP, HILR) and departments. 

Many of our tools are used across all DCE courses and programs. Thus, creating `Informed and Impactful` tools already requires us to work across different academic units. The very structure of our team is already situated between two teams, so it's fair to say that we are the embodiment of such explicit opportunities for collaborative pairings.

We advance this DCE-wide mission through our `Informed and Impactful` mission.

### J. Re-imagine our master’s degree offerings for the 21st century adult learner

This DCE-wide mission is mostly targeted toward our curriculum planning and program development groups at DCE. That said, their work requires new technologies to scale the new programs and degree offerings. Once these programs are created, we will begin to work with program heads and experts on the Teaching and Learning Team to identify projects to advance this DCE-wide mission.

We will work to advance this DCE-wide mission once our new master's degree offerings have been developed. Gabe is in meetings where they will get updates on the progress of this work and they will loop in the team once those projects have matured to the point where clear technologies are needed.

### K. Develop a noncredit strategy across DCE and develop and launch new programs

This DCE-wide mission aims to create other reasons for students to come to our programs, instead of only coming for credit.

We will work to advance this DCE-wide mission once our noncredit strategy has been developed. Gabe is in meetings where they will get updates on the progress of this work and they will loop in the team once those projects have matured to the point where clear technologies are needed.

# Overview of Technologies

Our technologies were chosen to fit our missions. Thinking about consistency, stability, scalability, etc. we've landed on the following stack:

**Front-end:** Typescript, React + SCSS + Bootstrap

**APIs**: REST

**Server-side:** Typescript, Node + Express

**Databases:** Mongo/Amazon DocDB

# Team Norms

## 1. Wellbeing is Top Priority

Our top priority is health, wellbeing, a sense of belonging, and a feeling that you can bring your full authentic self to work. In some ways, this means a culture of learning, flexibility, and kindness: we will work hard to flex our work processes to be mindful of teammates' health, wellbeing, and sense of belonging. In some ways, this means inflexibility where necessary in order to create a culture of uncompromising inclusion: we require usage of people's names and pronouns and respect for people's cultures and identities.

Health is extremely important. Remember that [flexible work arrangements](https://hr.harvard.edu/flexwork) and [workplace accommodations](https://accessibility.harvard.edu/workplace-accommodations) are available!

To keep everyone healthy and safe, team members agree to not join in-person meetings while sick in any way. This includes colds and other minor sicknesses. Further, if a teammate isn't well enough to work or meet, we fully support that teammate in taking time to fully recover. This includes physical health, mental health, and general wellbeing. 

## 2. Welcome Sharing, but Don't Mandate

We work hard to create safe spaces for everyone to feel like they can be their authentic selves at work. That said, it is everyone's choice to share. To advance the feeling of a safe space, we adopt a "model, don't mandate" mentality. Gabe might share things about themselves to create a space of openness, but this doesn't mean that sharing is required in any way. For example, Gabe will share their pronouns, but you needn't do that. If you don't share your pronouns, Gabe will simply not use gendered pronouns when referring to you and it'll be easy as pie.

## 3. Flexibility for Work-life Balance

We work hard to have flexible hours, schedules, and workloads to account for stuff in our lives that creates stress or anxiety (if possible, give warning to minimize impact on other team members).

Because we're part of a collaborative team, equity becomes important. Thus, while prioritizing flexibility and work-life balance, we must be careful that such flexibility does not encroach on other teammates own wellbeing, flexibility, and work-life balance. Basically, we don't grant flexibility where it will cause hardship to another teammate, where it will create blockers for other people's creativity or work, or where it will impact another teammate's wellbeing.

## 4. Clear and Constructive Feedback

We build a culture of constructive feedback. Gabe welcomes (and practically begs for) feedback. In return, Gabe works hard to give feedback to everyone on the team. If you ever feel unsure about how you're doing, please ask for feedback. Good conversations and sharing of feedback are how we create clarity and openness.

All feedback should be structured in a way that is constructive and respectful. In return, when receiving feedback, start by assuming that the person giving feedback is doing it with the best intent.

If you have feedback and you'd like to remain anonymous, submit it through [https://bit.ly/feedback-for-gabe](https://bit.ly/feedback-for-gabe)

## 5. Prompt and Respectful Communication

We use Slack for communication. If communication is happening outside of Slack, ping people in Slack. For example, if you left comments on someone's GitHub PR, ping them in Slack with a link to the GitHub PR. We expect prompt communication (get back to people within a day or two) but we only expect responses from each other on Monday, Tuesday, Wednesday, and Thursday (not Friday) from 9am to 4pm ET. Note: it's okay to send messages outside of hours, but there's no expectation to respond.

If you're very busy and don't have time to fully respond within one or two days, try to acknowledge the message (a quick thumbs up, for example) or give a time frame (e.g. "super busy, can we talk next week?"). Prompt communication is important because that teammate might be relying on you or blocking on you, but remember that we want to be kind and understanding; we all have a lot on our plates, so understand that prompt communication can be tough.

## 6. Take Space, Make Space

If you're someone who often takes up more space than others, try taking a little less space and leaving room for others to speak and contribute. If you're someone who often takes up less space than others, challenge yourself to speak and contribute more. Taking space can take multiple forms depending on collaboration style - not just speaking up in meetings, but also things like contributing ideas via chat or Slack, offering help and giving feedback, helping with organization and brainstorming, and so much more.

## 7. No Friday/Weekend Standing Meetings

We don't schedule regular meetings for Fridays and we don't schedule any meetings on Saturdays or Sundays.

## 8. Respect People's Time

Be punctual to meetings, end meetings on time. For foreseeable circumstances, give at least 2 days of notice if you can't attend a meeting or if you need to cancel/move a meeting. Be understanding for emergency circumstances.

## 9. Ask for Help, Offer Help

If you need help, ask for it. If you're worried that you're falling behind, running into roadblocks, or are making a big decision and need help thinking through the decision, ask for help. In exchange, take time to offer help as well. It's hard to ask for help. This takes effort, but it's worth it! We all help balance each other's workloads if we get help when we need it and offer help when we have extra bandwidth.

Time that you take to help others on the team is considered part of your work. This is not "above and beyond" work, this is not an extra thing on top of your work. Thus, of course, it goes on your time sheet and may mean that you will need rethink the schedule of your own work. Chat with Gabe to re-set expectations, deadlines, schedules, etc. instead of trying to squeeze everything in, potentially adding stress or tension for yourself.

## Thoughts?

Please share your thoughts on the norms, suggest new norms, and help improve our norms.

<Exercise tall>
  Come up with one challenge that we might face (tough deadlines, misunderstanding, someone said something hurtful, etc.)
</Exercise>

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre text>
Two teammates are working together and one person is dictating how the code should be developed while not listening to the other person's ideas
</pre>
</details>
<!-- End Example -->

<Exercise tall>
  Discuss which norms are relevant in this situation. How could we rely on our norms to resolve this? What norms might need to be added?
</Exercise>

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre text>
The most relevant norm would be "Take Space, Make Space" because it seems that one of the teammates doesn't have space to share their thoughts and opinions on the direction of the project.

Either the teammates could work it out together or one of them might ask Gabe for advice and Gabe could remind people of the "Take Space, Make Space" norm, asking the dominant team member to make space for the other teammate to share.
</pre>
</details>
<!-- End Example -->

# Project and File Management

## Assigned Tasks

We use GitHub Projects as our task management system. To see what you're assigned, visit the repo, click `Projects`, click our project, and take a look at the `Assigned` column. Cards with your picture on them are yours to do this week.

We'll be adding cards together, and sometimes you'll be in charge of creating cards to represent the tasks and work that you're doing. This is meant to be a collaborative process. Instead of purely dictating tasks, Gabe likes to discuss the task and then either work together to fill out the card or leave the creation of the card up to you. When you create cards, write down your understanding of the task, and Gabe will use it as a way to make sure everyone's on the same page about what the task entails.

When you start working on a task, drag the card to `In Progress`. 

When you finish a task, drag the card to `In Review`.

We'll peer-review each-other's work before moving cards to `Done`.

## GitHub

The main branch of the project is managed by Gabe. Anything that makes it to `main` is Gabe's responsibility, so please do not merge into `main`.

<Rule tall>
  Never commit, merge, or push to main
</Rule>

For each task you work on, check the title and type of the card in GitHub Projects. If there is no card, do your best to determine the type of work you're doing. That type may be "enhancement" or "feature" or "bugfix" etc.

Before starting to work on that task, create a new branch labeled `<type>/<lowercase-dashed-title>`.

<Rule>
  One branch per task, named appropriately
</Rule>

```bash
# For an "update" task called "Add Simplification Algorithm"
git checkout stage
git pull
git checkout -b update/add-simplification-algorithm
```

For your own public credit on GitHub and for traceability, we prefer that you commit and push to your branch very often.

<Rule>
  Commit and push to your branch frequently
</Rule>

```bash
# Always push after you commit
git add ...
git commit -m "description of what you did"
git push ...
```

When done with your task, submit a pull request to `stage` and describe everything you did in detail. Finally, request a review from a peer or from Gabe and let everyone know in Slack.

<Rule tall>
  When submitting a PR, always take time to do a self-review first: have you included documentation, fixed typos, fixed small issues?
</Rule>

## File Management

We use a strict file structure for all our projects. This helps us get around each other's code and greatly improves modularity and encourages code reuse.

Modules can take one of two structures: one/two files or folder. A module must be a folder if it has any helpers, sub-components, or more than two files for any other reason. There is one exception to this: test files are not included in this count, so you may end up with three files instead of a folder if one of them is a test.

<Rule>
  Modules must be folders if they have helpers, sub-components, or more than 2 files
</Rule>

```ts
// Allowed: 
MyComponent.tsx
MyComponent.scss

// BUT MUST BE A FOLDER...

// If there are 3+ files:
MyComponent/
  index.tsx
  style.scss
  logo.png

// OR

// If there are helpers:
MyComponent/
  index.tsx
  helpers/
    myHelper.tsx

// Or if there are sub-components:
MyComponent/
  index.tsx
  MySubComponent.tsx
  MySubComponent.scss
```

## Modules

Our npm projects are divided into modules. We use es6 import/export syntax.

### Creating a Module

To create a module, create a `.tsx` file and at the end of the file, on one line, export the item of interest as the default export.

<Rule>
  Default export must be at the end of the file
</Rule>

```ts
...

export default MyComponent;
```

The file name must match the name of the default export. This helps with consistency and helps with automatic documentation.

<Rule>
  Default export name must match file name
</Rule>

```ts
// Chart/index.tsx
export default MyComponent;

// MyButton.tsx
export default MyButton;
```

If an item takes up more than one line, define it above and then export it on one line.

<Rule>
  Export must be on a single line
</Rule>

```ts
const MyCar = {
    ...
};

export default MyCar;
```

### Importing a Module

When importing a module, leave out the extension if it's a `.ts` or `.tsx` file.

<Rule>
  When importing, leave off extension if ".tsx"
</Rule>

```ts
import MyComponent from '../shared/MyComponent';
```

If a module is a folder, leave off `index.tsx` when importing.

<Rule>
  Leave off "index.tsx" when importing file modules
</Rule>

```ts
// File structure
MyComponent/
  index.tsx
  style.scss
  MyButton.tsx

// Bad:
import MyComponent from './MyComponent/index';

// Good:
import MyComponent from './MyComponent';
```

# Typescript Basics

## Types

### Primitives

- `number` - all number types (int, float, etc.)
- `string` - text of any length
- `boolean` - either true or false
- `undefined` - unset
- `null` - no value
- `void` - either `undefined` or `null` - but we refrain from using it except for with function return types

### Important Data Structures

- `Array` - array of elements
- `Map` - dictionary with keys and values
- `Set` - set where items can only exist once in the list
- `Object` - unordered map where keys must be strings

### Types and Enums

- `Type/Interface` - a data type/interface
- `Enum` - an enum (does not support dynamic keys or values that are objects)

<Exercise>
  Match each of the following values to their type
</Exercise>

```ts
const a = 5 < 10;
const b = 'Hanalei';
const c = [1, 7, 5];
const d = 27;
const e = { name: 'Gabe' };
const f = e.age;
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
const a = 5 < 10; <b>// boolean</b>
const b = 'Hanalei'; <b>// string</b>
const c = [1, 7, 5]; <b>// number[]</b>
const d = 27; <b>// number</b>
const e = { name: 'Gabe' }; <b>// object, { [k: string]: string }</b>
const f = e.age; <b>// undefined</b>
</pre>
</details>
<!-- End Example -->

## Creating Variables

Use `const` when defining variables. Only use `let` if absolutely necessary (a variable's value changes). It is unforgivable to use `var`.

<Rule>
  Use const to define variables. Only use let if necessary
</Rule>

```ts
// Good
const name = 'Divardo';

// Good
const getName = () => { ... };

// Good only because age is modified later
let age = 10;
...
age += 1;
```

Object property modifications do **not** count as re-assigning:

```ts
// Still use const
const user = {
  name: 'Divardo',
  age: 10,
};

// These do not modify user
user.name = 'Jane';
user.age += 1;
```

An easy way to choose between `const` and `let` is simply to always start with `const` and only change it to `let` if the editor complains.

<Exercise>
  Fill in the let/const blank
</Exercise>

```ts
/**
 * Format a last name to indicate ownership (e.g. Calicci becomes Calicci's and Abrams becomes Abrams')
 * @author Gabe Abrams
 * @param lastName the last name of the person
 * @returns last name in ownership form
 */
____ genOwnershipForm = (lastName: any) => {
  // Last name that ends with "s" gets an apostrophe only
  if (lastName.endsWith('s')) {
    return `${lastName}'`;
  }

  // Other last names get "'s" suffix
  return `${lastName}'s`;
};

// Print account status
____ lastName = 'Calicci';
console.log(`This is ${genOwnershipForm(lastName)} laptop.`);

// Bonus points for finding other errors in the code
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
/**
  * Format a last name to indicate ownership (e.g. Calicci becomes Calicci's and Abrams becomes Abrams')
  * @author Gabe Abrams
  * @param lastName the last name of the person
  * @returns last name in ownership form
  */
<b>const</b> genOwnershipForm = (lastName: <b>string</b>) => {
  // Last name that ends with "s" gets an apostrophe only
  if (lastName.endsWith('s')) {
    return `${lastName}'`;
  }

  // Other last names get "'s" suffix
  return `${lastName}'s`;
};

// Print account status
<b>const</b> lastName = 'Calicci';
console.log(`This is ${genOwnershipForm(lastName)} laptop.`);
</pre>
</details>
<!-- End Example -->

<Exercise>
  Fill in the let/const blank
</Exercise>

```ts
// Create a bank account
____ checking: BankAccount = {
  firstName: 'Gabe',
  lastName: 'Abrams',
  balance: 29,
};

// Deduct money from the account balance
checking.balance -= 10;
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
// Create a bank account
<b>const</b> checking: BankAccount = {
  firstName: 'Gabe',
  lastName: 'Abrams',
  balance: 29,
};

// Deduct money from the account balance
checking.balance -= 10;
</pre>
</details>
<!-- End Example -->

We favor longer variable names that are descriptive: `mouseX` is better than `x`. When apps are bundled and built, variable names are minified anyway. Don't minimize number of chars, minimize confusion and ambiguity.

<Rule>
  Use appropriate naming conventions, be descriptive
</Rule>

```ts
// Variable:
favoriteFruits

// Constant:
FAVORITE_FRUITS // (all caps with underscores)

// Enum:
FavoriteFruit // (notice this is not pluralized)

// Typescript Class (not a css class):
FavoriteFruits

// Component:
FavoriteFruits

// CSS class:
.FavoriteFruits-container
```

If a variable is an optional boolean, always name it such that `false` is the default value. For example, if users are usually online while using the tool, an optional status boolean should be named `isOffline` so that `false` can be the default value (instead of `isOnline` where `true` is the default value). You'll really appreciate this consistency farther down the line and when reading other people's code. This is especially useful in React with optional boolean component props which are only added if the boolean is true (if the default is false, it saves a lot of useless extra code).

<Rule>
  Name optional booleans such that false is the default value
</Rule>

```ts
// If users are usually teachers...

// Bad:
const isNotStudent?: boolean = ...

// Good
const isStudent?: boolean = ...
```

<Exercise>
  Create better names for the following variables
</Exercise>

```ts
// NOTE: This class represents a user in the database
class customUser {
  ...
}

// NOTE: This css class is used in the component called "MyButton"
.button-label {
  ...
}

// NOTE: Comments are usually not included
let noComments = true;

// NOTE: User age is usually included
let userAgeKnown = false;
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
// NOTE: This class represents a user in the database
class <b>CustomUser</b> {
  ...
}

// NOTE: This css class is used in the component called "MyButton"
.<b>MyButton-label</b> {
  ...
}

// NOTE: Comments are usually not included
let <b>commentsIncluded</b> = true;

// NOTE: User age is usually included
let <b>userAgeUnknown</b> = false;
</pre>
</details>
<!-- End Example -->

All variables must have types. If typescript cannot infer a type, one must be explicitly defined.

<Rule>
  All variables must have specific types (if not defined or inferred)
</Rule>

```ts
const name: string = getName();
// Note: always include a space before the type
```

All numbers must include units, either in the variable name itself or in a comment at the variable's declaration:

<Rule>
  All numbers must include units
</Rule>

```ts
// Good:
const heightFt = 5;
// or
const height = 5; // ft

// Bad:
const height = 5;
```

If you have the option to choose units, here are our preferred set of units:

- timestamp/time = ms
- age = years
- date = ms since epoch (number)
- video timestamp = seconds since start of video

<Exercise>
  Create acceptable names for the following variables
</Exercise>

```ts
// NOTE: This is the time since the user was last active
const lastActive = ...;

// NOTE: This is the time to wait before playing the next video
const videoDelay = 10;

// NOTE: This is the current "feels like" temperature outside
const feelsLike = 74;
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
// NOTE: This is the time since the user was last active
const <b>lastActiveTimestamp</b> = ...;

// NOTE: This is the time to wait before playing the next video
const <b>videoDelaySec</b> = 10;

// NOTE: This is the current "feels like" temperature outside
const <b>feelsLikeDeg</b> = 74; <b>// Fahrenheit</b>
</pre>
</details>
<!-- End Example -->

We reserve single quotes for typescript and double quotes for JSX. This makes our code differentiable and nestable.

<Rule>
  Only use single quotes in typescript, reserve double quotes for jsx props
</Rule>

```ts
// Import other components
import toggleButton from 'toggle-button';

const name = 'Divardo';
```

Arrays that start off empty must have a declared type.

<Rule>
  Arrays must have declared types
</Rule>

```ts
const names: string[] = [];
```

Objects must be defined with proper spacing to preserve clarity.

<Rule>
  Space out object properties
</Rule>

```ts
// Good:
const user = { name: 'Divardo' };

// Bad:
const user = {name: 'Divardo'};
```

If adding a variable to an object with the same name, use shorthand.

<Rule>
  Used object property shorthand
</Rule>

```ts
const name = 'Divardo';
const age = 10;

// Good:
const user = { name, age };

// Bad:
const user = { name: name, age: age };
```

### Simple Operations

Always use `===` for equality. If you're using `==` there had better be a really good reason.

<Rule>
  Always use === or !== for equality comparisons ("==" is banned)
</Rule>

```ts
if (name === 'Divardo') {
    ...
}
```

Triple equals (`===`) compares type and value. Thus, `'5' === 5` is false.

If you want to compare just value and not type, convert the variables first: `Number.parseInt('5', 10) === 5`, which will now return true.

If you want to do a deep comparison of two objects, use a library.

Math must be readable and grouped. Only one operation can happen in each parentheses group.

<Rule>
  Wrap each mathematical operation in parentheses
</Rule>

```ts
const x = (((a + b) * (c + d)) / e);
```

It turns out few people understand the subtleties of `num++` or `num--`, so we do not use those operators except in for loops, where its use is well-understood.

<Rule>
  Only use ++ or -- in for loop declarations
</Rule>

```ts
// Bad:
age++;

// Good:
age += 1;
```

This works nicely with other mathematical operations:

- Add: `age += 2`
- Multiply: `age *= 3`
- Divide: `age /= 5`
- Subtract: `age -= 1`

<Exercise>
  Update this code to match our rules
</Exercise>

```ts
// Get the restaurant hours
const hours = await getHoursFromDB();

// Create restaurant info object
const restaurantInfo = {
  name: 'Dosa House',
  hours: hours,
};

// Create the order
const foodOrder = { timestampMs: 12093840982,
  cost: 12.78,
  restaurantInfo: restaurantInfo,
};

// Ask the user for a tip
const tip = await askUserForTip();

// Update the cost to include the tip
foodOrder.cost = (foodOrder.cost * (tip + 1));

// Add a dollar to the cost as a kitchen surcharge
foodOrder.cost++;
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
// Get the restaurant hours
const hours = await getHoursFromDB();

// Create restaurant info object
const restaurantInfo = {
  name: 'Dosa House',
  <b>hours,</b>
};

// Create the order
const foodOrder = {
  <b>timestampMs: 12093840982,</b>
  cost: 12.78,<b> // USD</b>
  <b>restaurantInfo,</b>
};

// Ask the user for a tip
const tip = await askUserForTip();<b> // percent</b>

// Update the cost to include the tip
foodOrder.cost <b>*= (tip + 1)</b>;

// Add a dollar to the cost as a kitchen surcharge
foodOrder.cost <b>+= 1</b>;
</pre>
</details>
<!-- End Example -->

String addition must always be done using template strings.

<Rule>
  Only use template strings for string addition
</Rule>

```ts
const weather = `The temperature is ${temp} today`;
```

Never nest ternaries and always wrap them in parentheses, even if they're short.

<Rule>
  Never nest ternaries
</Rule>

```ts
// Bad:
const beingType = (age > 150 ? (allergy === 'sun' ? 'vampire' : 'zombie') : 'human');

// Good:
const monsterType = (allergy === 'sun' ? 'vampire' : 'zombie');
const beingType = (age > 150 ? monsterType : 'human');
```

<Rule>
  Put complex ternaries on multiple lines
</Rule>

```ts
// Bad
const carStatus = (miles > getCarMiles() ? `${make} is older than ${standard}` : 'new');

// Good
const carStatus = (
  miles > getCarMiles()
    ? `${make} is older than ${standard}`
    : 'new'
);
```

<Rule>
  Wrap multiline ternaries with parentheses, place condition on its own line
</Rule>

```ts
// Bad
const carStatus = miles > getCarMiles()
  ? `${make} is older than ${standard}`
  : 'new'
;

// Bad
const carStatus = (miles > getCarMiles()
  ? `${make} is older than ${standard}`
  : 'new'
);

// Good
const carStatus = (
  miles > getCarMiles()
    ? `${make} is older than ${standard}`
    : 'new'
);
```

<Rule>
  Operators always start lines
</Rule>

```ts
// Bad:
const carStatus = (
  miles > getCarMiles() ?
    `${make} is older than ${standard}` :
    'new'
);

// Good
const carStatus = (
  miles > getCarMiles()
    ? `${make} is older than ${standard}`
    : 'new'
);

// Bad:
const isInClass = (
  joinedZoom ||
  sittingInPerson ||
  watchedVideo
);

// Good:
const isInClass = (
  joinedZoom
  || sittingInPerson
  || watchedVideo
);

// Bad:
const age = (
  currentAge +
  elapsedTime
);

// Good:
const age = (
  currentAge
  + elapsedTime
);
```

<Exercise>
  Fix the formatting of the following boolean logic
</Exercise>

```ts
const isStudent = (
  inRoster && (!isTTM ||
    (studentEnrollments +
    observerEnrollments) >
    0
  )
);
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
// Required formatting:
const isStudent = (
  inRoster
  && (
    !isTTM
    || (
      (studentEnrollments + observerEnrollments)
      > 0
    )
  )
);

// It's also okay to put enrollments on their own lines
const isStudent = (
  inRoster
  && (
    !isTTM
    || (
      (
        studentEnrollments
        + observerEnrollments
      )
      > 0
    )
  )
);

// Much better with comments:
const isStudent = (
  // The user must be in the roster
  inRoster
  // ...and cannot be a TTM
  && (
    // The user is not a TTM
    !isTTM
    // ...or the user is a student/auditor
    || (
      (studentEnrollments + observerEnrollments)
      > 0
    )
  )
);
</pre>
</details>
<!-- End Example -->

When retrieving values from objects or tuples (arrays of length 2), you can destructure. We prefer that you do not alias (do not rename destructured values). This helps other programmers follow data around your code and also helps when people use `find` or other searching mechanisms.

<Rule>
  Destructure where possible. Do not alias unless necessary
</Rule>

```ts
const {
  name,
  age,
} = person;
```

## Errors

We always use `try/catch` to handle errors (we don't use `.then` or `.catch` unless absolutely necessary).

Errors must always contain two important ingredients:

1. A human-readable message that explains the issue in plain and simple english without revealing any technical details or inner workings of the app.
1. An error code in the form `ABC123`, where the letters are a code that's specific to the project or section of the project, and the number is a unique number assigned to the error.

<Rule tall>
  All errors must have a human-readable message and a unique error code
</Rule>

To make this possible, we use a custom error called `ErrorWithCode` which can be found in `dce-reactkit`.

## Functions

We never use the `function` keyword. It's been outdated for years.

<Rule>
  Never use the function keyword
</Rule>

```ts
// Banned:
function honk(horn) {
    ...
}
```

Use arrow functions as much as possible: this ensures appropriate context binding and reduces complexity.

<Rule>
  Use arrow functions as much as possible
</Rule>

```ts
// Helper
const honk = (horn: HondaHorn) => {
    ...
};

// Inline
cars.forEach((car) => {
    ...
});
```

To keep our arrow functions uniform, we try not to use shorthand unless it's very helpful. Thus, parentheses around arguments are usually required and curly brackets are usually required surrounding the body, even if the function is very simple. Similarly, most arrow functions should be multiline.

<Rule>
  Arrow functions usually have ( ) and { } and are usually multiline
</Rule>

```ts
// Banned:
(x) => x + 1

// Banned:
name => { print(name); }

// Good:
(x) => {
  return x + 1;
}

// Good:
(name) => {
  print(name);
}
```

<Exercise>
  Fix the function below to make it adhere to our standards
</Exercise>

```ts
// NOTE: created by Chat GPT using this prompt:
// Create a typescript function that takes a string and counts the number of sentences

function countSentences(text: string): number {
  // Define an array of characters that may end a sentence.
  const sentenceEnders = [".", "!", "?"];
  
  // Initialize the sentence count to zero.
  let sentenceCount = 0;
  
  // Loop through each character in the text.
  for (let i = 0; i < text.length; i++) {
    const char = text[i];
    
    // If the character is a sentence ender, increment the sentence count.
    if (sentenceEnders.includes(char)) {
      sentenceCount++;
    }
  }
  
  // Return the sentence count.
  return sentenceCount;
}

// Bonus points for optimizing the code too!
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
<b>// NOTE: moved this outside of function so it isn't initialized over and over</b>
// Define an array of characters that may end a sentence.
const sentenceEnders = [<b>'.', '!', '?'</b>];

const countSentences = (text: string): number => {
  // Initialize the sentence count to zero.
  let sentenceCount = 0;
  
  // Loop through each character in the text.
  for (let i = 0; i < text.length; i++) {
    const char = text[i];
    
    // If the character is a sentence ender, increment the sentence count.
    if (sentenceEnders.includes(char)) {
      sentenceCount <b>+=</b> 1;
    }
  }
  
  // Return the sentence count.
  return sentenceCount;
}
</pre>
</details>
<!-- End Example -->

### Documentation

All named functions absolutely must have JSDoc definitions. Include a description of the purpose of the function, add one or more author tags for people who worked on that function, and describe arguments and return.

<Rule>
  Add JSDoc to all named functions
</Rule>

```ts
/**
 * Prepares a car to race: fills up the tank and tests the engine
 * @author Your Name
 * @param car the car to prepare
 * @param raceType the type of race to prepare for
 * @returns cost of the preparation process in USD
 */
const prepareCar = async (car: Car, raceType: RaceType): number => {
    ...
};
```

Notice that data types are included inline in the typescript function declaration. To minimize documentation update issues, keep data types and sync/async status inline in the typescript. Do not include them in JSDoc. Thus, `{type}` tags and the `@async` keyword are not allowed

<Rule>
  Don't duplicate descriptions with JSDoc
</Rule>

```ts
// Bad:
/**
 * Prepares a car to race: fills up the tank and tests the engine
 * @author Your Name
 * @async
 * @param {Car} car the car to prepare
 * @param {RaceType} raceType the type of race to prepare for
 * @returns cost of the preparation process in USD
 */
const prepareCar = async (car: Car, raceType: RaceType): number => {
  ...
};

// Good:
/**
 * Prepares a car to race: fills up the tank and tests the engine
 * @author Your Name
 * @param car the car to prepare
 * @param raceType the type of race to prepare for
 * @returns cost of the preparation process in USD
 */
const prepareCar = async (car: Car, raceType: RaceType): number => {
  ...
};
```

<Exercise>
  Create JSDoc for the following function
</Exercise>

```ts
const countSentences = (
  opts: {
    text: string,
    sentenceEnders?: string[],
    countEmptyLines?: boolean,
  },
): number {
  ...
};
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
<b>
/**
  * Count the number of sentences in a string
  * @author Gabe Abrams
  * @param opts object containing all arguments
  * @param opts.text the text to analyze
  * @param [opts.sentenceEnders] custom sentence ender punctuation marks
  *   to use when counting sentences
  * @param [opts.countEmptyLines] if true, count empty lines as sentences too
  * @returns the number of sentences in the text
  */
</b>
const countSentences = (
  opts: {
    text: string,
    sentenceEnders?: string[],
    countEmptyLines?: boolean,
  },
): number {
  ...
};
</pre>
</details>
<!-- End Example -->

### Default Argument Values

To include a default value for an argument, do this:

```ts
const helper = (a: string, b: string = 'default value') => {
  // ...
};
```

<Rule>
  All required params must come before default params
</Rule>

```ts
// Bad:
const helper = (text: string, greeting: string = 'hi', id: number) => {
  ...
};

// Good:
const helper = (text: string, id: number, greeting: string = 'hi') => {
  ...
};
```

With types and defaults, arguments can take up a lot of space. As usual, if one item is on another line, all items must be on their own lines. Here's how to do this with arguments:

```ts
const helper = (
  opts: {
    requiredParam1: string,
    requiredParam2: number,
    optionalParam: string = 'default value',
  },
) => {
  // ...
};
```

## Classes

Ask yourself: should this code be a helper function or a class? One rule of thumb is that if code will only be instantiated once, it's probably best as a helper function. Also, if it doesn't have to maintain its own context (it's mostly data, maybe a couple helper functions that do not refer to "this") it could probably just be a type.

All variables in the class must be defined at the top of the class (all `this.xyz` variable).

<Rule>
  Define all instance properties at top of class
</Rule>

```ts
class User {
  private name: string;
  private age: number;
  private pronouns?: string;
  private gender?: string;

  ...
}
```

Every property and methods must be labeled as either `private` or `public`. We require that you make an active decision on privacy. Note: `#` is an acceptable substitute for `private` if you prefer.

<Rule>
  All class properties and methods must either be private or public
</Rule>

```ts
class User {
  // Bad:
  name: string;

  // Good:
  private name: string;

  // Bad:
  getName(): string {
    ...
  }

  // Good:
  public getName(): string {
    ...
  }
}
```

If a method doesn't refer to `this`, then there's no reason it can't be a `static` method. Thus, if a method doesn't refer to `this`, we require that it be `static`. This helps because it's easy for others to figure out if a function depends on class variables.

<Rule>
  Methods that don't reference "this" must be static
</Rule>

```ts
class User {
  // Bad:
  public sayHello() {
    console.log('Hello!');
  }

  // Good:
  public static sayHello() {
    console.log('Hello!');
  }

  // Good:
  public getName(): string {
    return this.name;
  }
}
```

<Exercise>
  Think of your favorite mode of transport as a kid (bike, tricycle, rip stick, scooter) and create a class that represents it (don't implement functions)
</Exercise>

```ts
// Example:
class Kayak {
  // Number of seats in the kayak
  private numSeats: number;
  // Current location
  private location: { x: number, y: number };
  // Current direction
  private direction: number; // degrees

  /**
   * Performs paddle operation, moving the kayak either forward or backward
   * @author Gabe Abrams
   * @param [backward] if true, paddle backward
   */
  public paddle(backward?: boolean) {
    // TODO: implement
  }

  /**
   * Either turns the kayak left (ccw) or right (cw)
   * @author Gabe Abrams
   * @param [opts] object containing all arguments
   * @param [opts.direction=left] the direction to turn
   * @param [opts.angle=45] number of degrees to turn the kayak
   */
  public turn(
    opts: {
      direction?: 'left' | 'right',
      angle?: number,
    } = {},
  ) {
    // TODO: implement
  }
}
```

## Types

We use `Type` to define types (instead of `Interface`) because of some important advanced features that we leverage in React. Note that many people disagree with Gabe on this, so be flexible in interviews, be ready to use `Interface` as well.

<Rule>
  Wherever possible, use Type instead of Interface
</Rule>

```ts
type Car = {
  ...
};
```

We treat types as objects, ending lines with `,` instead of `;`. This isn't because of very important functionality, this is just for consistency. The commas show that each item is part of the whole.

<Rule>
  Delimit types with commas
</Rule>

```ts
type Car = {
  // Company that the car was made by
  make: string,
  // Age
  age: number, // years
};
```

Every property in a type must be accompanied by a full description and units (as usual). Comment above each item.

<Rule>
  Describe all type properties
</Rule>

```ts
// Good:
type Car = {
  // Company that the car was made by
  make: string,
  // Age of the car
  age: number, // years
};

// Bad:
type Car = {
  make: string,
  age: number,
};
```

<Exercise>
  Create a type for your favorite savory entree as if it were a customizable item on an online menu
</Exercise>

```ts
// Example: Samosa Chaat
type SamosaChaat = {
  // Filling inside of the samosa
  filling: string,
  // If true, the chaat will be prepared with more spice
  spicy: boolean,
  // Number of samosas in the chaat
  samosaQuantity: number,
};
```

If a type can have multiple different structures, use `|`:

<Rule>
  If a type has multiple forms, separate by |
</Rule>

```ts
type Vehicle = (
  | {
    // Type of vehicle
    type: 'car',
    // Number of wheels
    numWheels: number,
    // True if car fits in a compact parking spot
    isCompact: boolean,
  }
  | {
    // Type of vehicle
    type: 'truck',
    // Number of wheels
    numWheels: number,
    // True if truck has a trailer hitch
    hasTrailerHitch: boolean,
  }
);
```

In the case where all forms of a type have shared parts, separate that out into a general section of the type:

```ts
type Vehicle = (
  // Common parameters
  {
    // Number of wheels
    numWheels: number,
  }
  // Type-dependent parameters
  & (
    // Car
    | {
      // Type of vehicle
      type: 'car',
      // True if car fits in a compact parking spot
      isCompact: boolean,
    }
    // Truck
    | {
      // Type of vehicle
      type: 'truck',
      // True if truck has a trailer hitch
      hasTrailerHitch: boolean,
    }
  )
);
```

<Exercise>
  Add an optional "side" for your entree. Add a "hasSide" boolean and if it's true, also define your "side" type
</Exercise>

```ts
// Example: Samosa Chaat with Optional Drink
type SamosaChaat = (
  {
    // Filling inside of the samosa
    filling: string,
    // If true, the chaat will be prepared with more spice
    spicy: boolean,
    // Number of samosas in the chaat
    samosaQuantity: number,
  } & (
    // No side drink
    | {
      // If true, a side is included
      hasSide: false,
    }
    // Includes side
    | {
      // If true, a side is included
      hasSide: true,
      // Description of side
      side: {
        // Name of the side
        name: (
          | 'Lassi'
          | 'Water'
          | 'Chai'
        ),
        // Additional cost of the side
        costDollars: number,
      },
    }
  )
);
```

### Types Cheatsheet

For your reference, here's a types cheatsheet with props that I use frequently:

```ts
// Primitives
string // text or character (e.g. 'Hello' or 'h')
number // integer or float (e.g. 4 or 4.73)
boolean // true or false
undefined // Unset value
null // Absence of value

// Operations
(string | number) // Any type in this list
('blue' | 'red' | 'green') // Any value in a list

// Arrays
string[] // Array of strings
number[] // Array of numbers
Car[] // Array containing objects of type Car
(string | Car)[] // Array of strings or objects of type Car

// Enums
EnumName // Enums also function as types

// Common Data Structures
{ [k: string]: number } // Object where keys are strings, values are numbers
Map<string, Car> // Map where keys are strings, values are objects of type Car
Set<Car> // Set of objects of type Car

// Functions
() => undefined // Function with no arguments, no return
(car: Car) => undefined // Function with an argument and no return value
(car: Car, year?: number) => number // Function with optional arg and return type

// Object with specific structure
{
  name: string,
  age?: number,
}

// React types
React.ReactNode // Renderable React content
React.FC<Props> // Functional Component

// Types to avoid
any
unknown
```

Avoid casting at all costs, but if it must be done, use the `as` keyword:

```ts
const user = (await fetchUserFromAPI()) as User;
```

Casting is different from value conversion:

```ts
// Convert to a string:
const str = String(value);

// Convert to a number:
const int = Number.parseInt(value, 10);
const fl = Number.parseFloat(value);

// Convert to a boolean:
const b = !!value;
```

## Enums

If a value can take on many pre-determined values, we use enums. However, we understand that enums are limited: keys are not dynamic and values cannot be complex objects. Use enums where possible.

<Rule>
  Prefer enums, but substitute with objects if not possible
</Rule>

```ts
enum Instrument {
  // An upright piano
  Piano = 'Piano',
  // A violin string instrument
  Violin = 'Violin',
}
```

There are shorthands for numerical enums. To ensure readable database entries and debugging, we prefer string-valued enums where the value is identical to the name.

<Rule>
  Keys and values of enums should be identical strings
</Rule>

```ts
// Bad:
enum Instrument {
  Piano = 'piano',
  Violin = 'violin',
}

// Bad:
enum Instrument {
  Piano,
  Violin,
}

// Bad:
enum Instrument {
  Piano = 1,
  Violin = 2,
}

// Good:
enum Instrument {
  // An upright piano
  Piano = 'Piano',
  // A violin string instrument
  Violin = 'Violin',
}
```

<Exercise>
  Update your entree type to use enums
</Exercise>

```ts
// Type of fillings
enum Filling {
  // Potato and pea filling
  PotatoPea = 'PotatoPea',
  // Cauliflower mash filling
  Cauliflower = 'Cauliflower',
}

// Name of side
enum SideName {
  // Mango or salty lassi
  Lassi = 'Lassi',
  // Iced water
  Water = 'Water',
  // Masala tea
  Chai = 'Chai',
}

// Example: Samosa Chaat with Optional Drink
type SamosaChaat = (
  {
    // Filling inside of the samosa
    filling: Filling,
    // If true, the chaat will be prepared with more spice
    spicy: boolean,
    // Number of samosas in the chaat
    samosaQuantity: number,
  } & (
    // No side drink
    | {
      // If true, a side is included
      hasSide: false,
    }
    // Includes side
    | {
      // If true, a side is included
      hasSide: true,
      // Description of side
      side: {
        // Name of the side
        name: SideName,
        // Additional cost of the side
        costDollars: number,
      },
    }
  )
);
```

It's important to know the type of item, not just the item itself, especially when reading other people's code. Also, some enums may have duplicate keys. This is why we don't destructure enums.

<Rule tall>
  Never destructure enums
</Rule>

## Code Style

To keep code readable and simple, if there are ever more than three of anything (arguments, values, anything), each must be on its own line. Honestly, it's okay to put items on their own lines if there are two or more items.

<Rule>
  If more than three elements, put each element on its own line
</Rule>

```ts
Additionally, whenever there is one item on its own line, all other items must be on their own lines as well.
```

<Rule tall>
  When an item is on its own line, only that item can be on the line (no parentheses, etc.)
</Rule>

Arrays:

```ts
// Bad: first item is not on its own line
const fruits = ['Apple',
  'Orange',
  'Pineapple',
  'Mango',
];

// Bad: last item is not on its own line
const fruits = [
  'Apple',
  'Orange',
  'Pineapple',
  'Mango'];

// Good
const fruits = [
  'Apple',
  'Orange',
  'Pineapple',
  'Mango',
];
```

Function calls:

```ts
// Bad: first item is not on its own line
const firstName = database.initialize()
    .getUser()
    .firstName;

// Bad
const firstName = (
    database.initialize()
        .getUser()
        .firstName
);

// Good
const firstName = (
    database
        .initialize()
        .getUser()
        .firstName
);
```

Arguments:

```ts
// Bad: first item is not on its own line
startCar(Engine.getFourCylinder(),
    WheelKit.manufacture(4),
    Horn.prepare(),
);

// Bad: last item is not on its own line
startCar(Engine.getFourCylinder(),
    WheelKit.manufacture(4),
    Horn.prepare());

// Good
startCar(
    Engine.getFourCylinder(),
    WheelKit.manufacture(4),
    Horn.prepare(),
);
```

<Exercise>
  Fix the following bits of code
</Exercise>

```ts
// Bit 1:
const output = getOutput(text, {
  parse: true,
  delimiter: ',',
});

// Bit 2:
const ageNextYear = (
  ageAtLogin
  + elapsedYears
  + 1);

// Bit 3:
const studentLists = [getDCEStudents(),
  getFASUsers().roster
    .filter((user) => {
      return user.isStudent;
    }).map((user) => {
      return user.userInfo;
    }),
];
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
// Bit 1:
const output = getOutput(
  <b>text, {</b>
    <b>parse: true,</b>
    <b>delimiter: ',',</b>
  <b>},</b>
);

// Bit 2:
const ageNextYear = (
  <b>ageAtLogin</b>
  <b>+ elapsedYears</b>
  <b>+ 1</b>
);

// Bit 3:
const studentLists = [
  <b>getDCEStudents(),</b>
  <b>getFASUsers()</b>
    <b>.roster</b>
    <b>.filter((user) => {</b>
      <b>return user.isStudent;</b>
    <b>})</b>
    <b>.map((user) => {</b>
      <b>return user.userInfo;</b>
    <b>}),</b>
];
</pre>
</details>
<!-- End Example -->

For all arrays, function arguments, object definitions, and other comma-delineated objects, use trailing commas. This helps create clean git diffs and reduces typos.

<Rule>
  Use trailing commas
</Rule>

```
See the examples above. Look for trailing commas.

Note: this is not supported in `.json` files. Thus, when possible, we prefer `.tsx` for data if possible.
```

<Rule>
  Use "guard clauses" if possible
</Rule>

```ts
// Bad:
const showTeacherInfo = () => {
  // Make sure there's at least one enrolled user
  if (enrollments.length > 0) {
    // Print
    console.log('This course has at least one enrolled user');

    // Check if the course has a teacher
    const hasTeacher = enrollments.some((enrollment) => {
      return (enrollment.type === 'TTM');
    });
    if (hasTeacher) {
      // Print
      console.log('This course already has an assigned teacher');

      // Update the UI
      dispatch({
        type: ActionType.ShowTeacherInfo,
      });
    }
  }
};

// Good:
const showTeacherInfo = () => {
  // Make sure there's at least one enrolled user
  if (enrollments.length === 0) {
    return;
  }

  // Print
  console.log('This course has at least one enrolled user');

  // Check if the course has a teacher
  const hasTeacher = enrollments.some((enrollment) => {
    return (enrollment.type === 'TTM');
  });
  if (!hasTeacher) {
    return;
  }
  
  // Print
  console.log('This course already has an assigned teacher');

  // Update the UI
  dispatch({
    type: ActionType.ShowTeacherInfo,
  });
};
```

Guard clauses are `if` statements that terminate execution. Using guard clauses removes the need for nesting.


# Typescript Advanced Stuff

## Array Functions

Array functions are awesome. Replace loops with array functions wherever possible. Unfortunately, array functions do not fully support async/await yet. That's the only time we must use a `for` loop.

<Rule>
  Use array functions whenever possible unless await is used inside
</Rule>

```ts
// Good:
fruits.forEach((fruit: Fruit) => {
  console.log(`I love ${fruit}s`);
});

// Bad:
fruits.forEach(async (fruit: Fruit) => {
  await fruit.waitToRipen();
});

// Good
for (let i = 0; i < fruits.length; i++) {
  await fruits[i].waitToRipen();
}
```

Each array function takes an anonymous "operation function" that is called once for each element in the array. Each time the operation function is called, it receives one of the array elements as an argument. This occurs sequentially such that the operation function is called with the first element, then the second element, then the third, and so on.

### array.forEach – Executes a provided function once for each array element

The operation function holds the code that you want to run for each element.

```ts
const fruits = ['apple', 'orange', 'pineapple'];

fruits.forEach((fruit: string) => {
  console.log(`I love ${fruit}s`);
});

// Output:
// > I love apples
// > I love oranges
// > I love pineapples
```

You can also get the element's index:

```ts
fruits.forEach((fruit, i) => {
  // ...
});
```

<Exercise>
  Create code that greets every other student
</Exercise>

```ts
const studentNames = ['Divardo', 'Calicci', 'Kai', 'Manu', 'Anini', 'Alli'];

// TODO: implement

// Output:
// > Hello, Calicci
// > Hello, Manu
// > Hello, Alli
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
const studentNames = ['Divardo', 'Calicci', 'Kai', 'Manu', 'Anini', 'Alli'];

// Greet every other student
studentNames.forEach((studentName, i) => {
  // Skip even indexed students
  if (i % 2 === 0) {
    return;
  }

  // Greet the student
  console.log(`Hello, ${studentName}`);
});
</pre>
</details>
<!-- End Example -->

### array.map – Creates a new array by applying a function to each element

The operation function takes an element of the original array, does some computation, and then returns the corresponding element for the new array.

```ts
type Car = {
  // The color of the car
  color: string,
  // The year the car was made
  year: number,
};

const cars: Car[] = [
  {
    color: 'red',
    year: 2015,
  },
  {
    color: 'blue',
    year: 2018,
  },
];

const years: number[] = cars.map((car: Car) => {
  return car.year;
});

const olderCars: Car[] = cars.map((car: Car) => {
  return {
    ...car,
    year: car.year - 1,
  };
});
```

<Exercise>
  Create code that prepends each student's name with "Legal Name: "
</Exercise>

```ts
const studentNames = ['Divardo', 'Calicci', 'Kai'];

// TODO: implement

// Output: ['Legal Name: Divardo', 'Legal Name: Calicci', 'Legal Name: Kai']
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
const studentNames = ['Divardo', 'Calicci', 'Kai'];

// Prepend each student's name
const prependedStudentNames = studentNames.map((studentName) => {
  // Add prefix
  return `Legal Name: ${studentName}`;
});
</pre>
</details>
<!-- End Example -->

<Rule tall>
  Prefer .forEach or .map over .reduce
</Rule>

<Rule>
  Never modify function arguments
</Rule>

```ts
// Bad:
const olderCars: Car[] = cars.map((car: Car) => {
  car.year -= 1;

  return car;
});

// Good:
const olderCars: Car[] = cars.map((car: Car) => {
  return {
    ...car,
    year: car.year - 1,
  };
});
```

### array.some – Test whether an element in the array passes the test function

The operation function takes an element in the array and returns true/truthy if this element passes the test. If any element results in the operation function returning true/truthy, `some` immediately returns true. If no elements result in the operation function returning true/truthy, `some` returns false after going through the entire array.

```ts
type Car = {
  // The color of the car
  color: string,
  // The year the car was made
  year: number,
};

const cars: Car[] = [
  {
    color: 'red',
    year: 2015,
  },
  {
    color: 'blue',
    year: 2018,
  },
];

const atLeastOneRed = cars.some((car: Car) => {
  return (car.color === 'red');
});
```

<Exercise>
  Create code that checks if any of the students have a name that ends with a vowel
</Exercise>

```ts
const listA = ['Divardo', 'Calicci', 'Kai'];
const listB = ['Max', 'Clark', 'Ash'];

// TODO: implement

// Output:
// > true
// > false
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
const listA = ['Divardo', 'Calicci', 'Kai'];
const listB = ['Max', 'Clark', 'Ash'];

// Create a list of vowels
const vowels = 'aeiou'.split('');

// Go through each list and check if a student's name ends with a vowel
[listA,listB].forEach((studentNames) => {
  const atLeastOneNameEndsWithVowel = studentNames.some((studentName) => {
    // Get last letter
    const lastLetter = (
      studentName
        .toLowerCase()
        .substring(studentName.length - 1)
    );

    // Check if last letter is a vowel
    return vowels.includes(lastLetter);
  });
});
</pre>
</details>
<!-- End Example -->

### array.every – Test whether all elements in the array pass the test function

The operation function takes an element in the array and returns true/truthy if this element passes the test. If all elements results in the operation function returning true/truthy, `every` returns true after going through the entire array. If at any point, one of the elements result in the operation function returning false/falsy, `every` immediately returns false.

```ts
type Car = {
  // The color of the car
  color: string,
  // The year the car was made
  year: number,
};

const cars: Car[] = [
  {
    color: 'red',
    year: 2015,
  },
  {
    color: 'blue',
    year: 2018,
  },
];

const allCarsAreRed = cars.every((car: Car) => {
  return (car.color === 'red');
});
```

<Exercise>
  Create code that checks if every student is at least 18 years old
</Exercise>

```ts
type Student = {
  // First name
  name: string,
  // Age
  age: number, // years
};

const listA: Student[] = [
  { name: 'Divardo', age: 17 },
  { name: 'Calicci', age: 18 },
  { name: 'Kai', age: 19 },
];
const listB: Student[] = [
  { name: 'Max', age: 20 },
  { name: 'Clark', age: 18 },
  { name: 'Ash', age: 22 },
];

// TODO: implement

// Output:
// > false
// > true
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
const listA = [
  { name: 'Divardo', age: 17 },
  { name: 'Calicci', age: 18 },
  { name: 'Kai', age: 19 },
];
const listB = [
  { name: 'Max', age: 20 },
  { name: 'Clark', age: 18 },
  { name: 'Ash', age: 22 },
];

// Go through each list and check if all students are 18+
[listA,listB].forEach((students) => {
  const allStudentsAtLeast18 = students.every((student) => {
    return (student.age >= 18);
  });
});
</pre>
</details>
<!-- End Example -->

### array.filter – Create an array with elements that pass the test function

The operation function takes an element in the array and returns true/truthy if this element passes the test. At the end, `filter` returns a new array that contains only the elements that pass the test.

```ts
type Car = {
  // The color of the car
  color: string,
  // The year the car was made
  year: number,
};

const cars: Car[] = [
  {
    color: 'red',
    year: 2015,
  },
  {
    color: 'blue',
    year: 2018,
  },
];

const redCars = cars.filter((car: Car) => {
  return (car.color === 'red');
});
```

<Exercise>
  Create code that creates a list of students who are teens
</Exercise>

```ts
type Student = {
  // First name
  name: string,
  // Age
  age: number, // years
};

const students: Student[] = [
  { name: 'Divardo', age: 17 },
  { name: 'Calicci', age: 18 },
  { name: 'Kai', age: 19 },
  { name: 'Max', age: 20 },
  { name: 'Clark', age: 18 },
  { name: 'Ash', age: 22 },
  { name: 'Anna', age: 12 },
];

// TODO: implement

// Output:
// [
//   { name: 'Divardo', age: 17 },
//   { name: 'Calicci', age: 18 },
//   { name: 'Kai', age: 19 },
//   { name: 'Clark', age: 18 },
// ]
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
const students = [
  { name: 'Divardo', age: 17 },
  { name: 'Calicci', age: 18 },
  { name: 'Kai', age: 19 },
  { name: 'Max', age: 20 },
  { name: 'Clark', age: 18 },
  { name: 'Ash', age: 22 },
  { name: 'Anna', age: 12 },
];

// Filter to just teen students
const teens = students.filter((student) => {
  return (
    // Old enough
    student.age >= 13
    // ...and not too old
    && student.age < 20
  );
});
</pre>
</details>
<!-- End Example -->

### array.find - Return the first element that satisfies the test function

The operation function takes an element in the array and returns true/truthy if this element passes the test. At the end, `find` return the first element that passes the test. If no elements pass the test, `find` returns `undefined`.

```ts
type Car = {
  // Color of the body of the car
  color: string,
  // Year that the car was manufactured
  year: number, // e.g. 1995
  // The first name of the owner of the car
  owner: string,
};


const cars: Car[] = [
  {
    color: 'red',
    year: 2015,
    owner: 'Gabe',
  },
  {
    color: 'blue',
    year: 2018,
    owner: 'Ben',
  },
];

const bensCar = cars.find((car: Car) => {
  return (car.owner === 'Ben');
});
```

<Exercise>
  Create code that finds a student who's name starts with 'A'
</Exercise>

```ts
type Student = {
  // First name
  name: string,
  // Age
  age: number, // years
};

const students: Student[] = [
  { name: 'Divardo', age: 17 },
  { name: 'Calicci', age: 18 },
  { name: 'Kai', age: 19 },
  { name: 'Max', age: 20 },
  { name: 'Clark', age: 18 },
  { name: 'Ash', age: 22 },
  { name: 'Anna', age: 12 },
];

// TODO: implement

// Output:
// { name: 'Ash', age: 22 }
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
const students = [
  { name: 'Divardo', age: 17 },
  { name: 'Calicci', age: 18 },
  { name: 'Kai', age: 19 },
  { name: 'Max', age: 20 },
  { name: 'Clark', age: 18 },
  { name: 'Ash', age: 22 },
  { name: 'Anna', age: 12 },
];

// Find a student who's name starts with 'A'
<b>const studentWithNameStartingInA = students.find((student) => {</b>
  <b>return student.name.startsWith('A');</b>
<b>});</b>
</pre>
</details>
<!-- End Example -->

## Object Functions

Object functions are great for iterating through objects. Use them whenever possible. But just like array functions, if using async/await inside the loop, you'll need a for loop.

<Rule tall>
  Use object functions whenever possible unless await is used inside
</Rule>

### Object.keys(...) – get an array that contains each key in the object

```ts
const idToName = {
  12459: 'Divardo',
  50829: 'Calicci',
  50628: 'Keala',
};

const ids = Object.keys(idToName);
```

Note: no matter what type of keys you use, `Object.keys` returns an array of strings. In the example above, `ids` is a string array with values `['12459', '50829', '50628']`.

### Object.values(...) – get an array of values

```ts
const idToName = {
  12459: 'Divardo',
  50829: 'Calicci',
  51628: 'Keala',
};

const names = Object.values(idToName);
```

### Combine with array functions

It's often important to loop through an enum or object's keys or values.

```ts
Object.values(idToName).forEach((name: string) => {
  console.log(`Hello, ${name}!`);
});
```

<Exercise>
  Create an array containing just the first two digits of each student's id number
</Exercise>

```ts
const idToName = {
  12459: 'Divardo',
  50829: 'Calicci',
  51628: 'Keala',
};

// TODO: implement

// Output:
// [12, 50, 50]
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
const idToName = {
  12459: 'Divardo',
  50829: 'Calicci',
  51628: 'Keala',
};

// Extract the first two letters of each id number
const idPrefixes = Object.keys(idToName).map((id) => {
  return id.substring(0, 2);
});
</pre>
</details>
<!-- End Example -->

## Asynchronous Code

Typescript is a single-threaded interpreted language and is _much_ slower than C/C++ and other compiled languages. _But_, asynchronous code runs really fast and is great for servers and good for simple clients like browsers. Thus, Express and React are great choices as long as we use asynchronous code when necessary.

### Asynchronous Functions

This function is non-blocking and executes its function body in the background.

```ts
const funcName = async () => {
  ...
};
```

For asynchronous functions that have return values, simply wrap the return type in `Promise<...>`:

```ts
// For example, here's an async function that returns a number
const funcName = async (): Promise<number> => {
  ...
};
```

Always use the `async` keyword instead of returning `Promise` objects. In fact, refrain from referencing `Promise` except in types and when using `Promise.all`.

<Rule>
  Only reference Promise when using Promise.all or when defining types
</Rule>

```ts
// Bad:
const ready = new Promise((resolve, reject) => {
  ...
});

// Bad:
loadFile.then((contents) => {
  // ...
});
// (where loadFile returns a promise)

// Bad:
const funcName = () => {
  ...
  const p = new Promise((resolve, reject) => {
    ...
  });
  ...
  return p;
};

// Okay:
const funcName = async (): Promise<number> => {
  ...
  await doSomething();
  ...
  return 5;
};

// Okay:
await Promise.all(tasks);
```

<Exercise>
  Create an async function that creates a unique test assignment in a sandbox course
</Exercise>

```ts
// Import caccl-api
import initAPI from 'caccl-api';

// Initialize the API
const api = initAPI({
  // TODO: fill this in
});

// TODO: create a function "createTestAssignment" that creates a unique assignment in the course and returns it
// NOTE: check out the caccl-api docs at bit.ly/caccl-api
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
// Import caccl-api
import initAPI from 'caccl-api';

// Initialize the API
const api = initAPI({
  <b>canvasHost: 'canvas.harvard.edu',</b>
  <b>accessToken: '1895~sdjfoa9me098fjoiasnudo8f7am9sod8ufnoaisdunfkuasdf',</b>
  <b>defaultCourseId: 53450,</b>
});

<b>/**</b>
 <b>* Create a unique test assignment within the sandbox course</b>
 <b>* @author Gabe Abrams</b>
 <b>* @returns assignment object that was created</b>
 <b>*/</b>
<b>const createTestAssignment = async () => {</b>
  <b>// Generate a unique assignment name</b>
  <b>const uniqueAssignmentName = `Test Assignment[${Date.now()}-${Math.random()}]`;</b>

  <b>// Create an assignment</b>
  <b>const assignment = await api.course.assignment.create({</b>
    <b>name: uniqueAssignmentName,</b>
    <b>submissionTypes: ['none'],</b>
    <b>published: true,</b>
  <b>});</b>

  <b>// Return the new assignment</b>
  <b>return assignment;</b>
<b>};</b>
</pre>
</details>
<!-- End Example -->

### Waiting for async tasks

To wait for an async task, always use `await` instead of `.then`.

<Rule>
  Use await instead of .then
</Rule>

```ts
// Bad:
fruit.ripe().then(() => {
  console.log('The fruit is ripe!');
});

// Good:
await fruit.ripe();
```

To catch an error from an awaited task, just surround with `try/catch` instead of `.catch`. This is because if you forget to use `.catch`, errors disappear into the ether.

<Rule>
  Use try/catch instead of .catch
</Rule>

```ts
// Bad:
fruit.ripe().catch((err) => {
  ...
});

// Good:
try {
  await fruit.ripe();
} catch (err) {
  ...
}
```

### Series execution

Use the `await` flag to wait for each function to finish.

```ts
const data1 = await doTask1();
const data2 = await doTask2();
```

<Exercise>
  Create an assignment and then get the full list of assignments
</Exercise>

```ts
// Import caccl-api
import initAPI from 'caccl-api';

// Initialize the API
const api = initAPI({
  // TODO: fill this in
});

// TODO: implement the solution
// NOTE: check out the caccl-api docs at bit.ly/caccl-api
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
// Import caccl-api
import initAPI from 'caccl-api';

// Initialize the API
const api = initAPI({
  <b>canvasHost: 'canvas.harvard.edu',</b>
  <b>accessToken: '1895~sdjfoa9me098fjoiasnudo8f7am9sod8ufnoaisdunfkuasdf',</b>
  <b>defaultCourseId: 53450,</b>
});

<b>/**</b>
 <b>* Create a unique test assignment within the sandbox course</b>
 <b>* @author Gabe Abrams</b>
 <b>* @returns assignment object that was created</b>
 <b>*/</b>
<b>const createTestAssignment = async () => {</b>
  <b>// Generate a unique assignment name</b>
  <b>const uniqueAssignmentName = `Test Assignment [${Date.now()}-${Math.random()}]`;</b>

  <b>// Create an assignment</b>
  <b>const assignment = await api.course.assignment.create({</b>
    <b>name: uniqueAssignmentName,</b>
    <b>submissionTypes: ['none'],</b>
    <b>published: true,</b>
  <b>});</b>

  <b>// Return the new assignment</b>
  <b>return assignment;</b>
<b>};</b>

<b>// First, create an assignment</b>
<b>await createTestAssignment();</b>

<b>// Then, get the full list of assignments</b>
<b>const assignments = await api.course.assignment.list();</b>
</pre>
</details>
<!-- End Example -->

### Parallel execution

Combine `await` with `Promise.all` for parallel execution.

```ts
const [
  data1,
  data2,
] = await Promise.all([
  doTask1(),
  doTask2(),
]);
```

<Exercise>
  In parallel, get the list of pages, assignments, and discussion topics
</Exercise>

```ts
// Import caccl-api
import initAPI from 'caccl-api';

// Initialize the API
const api = initAPI({
  // TODO: fill this in
});

// TODO: implement the solution
// NOTE: check out the caccl-api docs at bit.ly/caccl-api
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
// Import caccl-api
import initAPI from 'caccl-api';

// Initialize the API
const api = initAPI({
  <b>canvasHost: 'canvas.harvard.edu',</b>
  <b>accessToken: '1895~sdjfoa9me098fjoiasnudo8f7am9sod8ufnoaisdunfkuasdf',</b>
  <b>defaultCourseId: 53450,</b>
});

<b>// In parallel, get course content</b>
<b>const [</b>
  <b>pages,</b>
  <b>assignments,</b>
  <b>discussionTopics,</b>
<b>] = await Promise.all([</b>
  <b>// List pages</b>
  <b>api.course.page.list(),</b>
  <b>// List assignments</b>
  <b>api.course.assignment.list(),</b>
  <b>// List discussion topics</b>
  <b>api.course.discussionTopic.list(),</b>
<b>]);</b>
</pre>
</details>
<!-- End Example -->

<Exercise>
  Run two tasks in parallel: 1. create a unique assignment and then get the list of assignments, 2. create a unique page and then get the list of pages
</Exercise>

```ts
// Import caccl-api
import initAPI from 'caccl-api';

// Initialize the API
const api = initAPI({
  // TODO: fill this in
});

// TODO: implement the solution
// NOTE: check out the caccl-api docs at bit.ly/caccl-api
```

<!-- Start Example -->
<details>
<summary>Example Result</summary>
<pre>
// Import caccl-api
import initAPI from 'caccl-api';

// Initialize the API
const api = initAPI({
  <b>canvasHost: 'canvas.harvard.edu',</b>
  <b>accessToken: '1895~sdjfoa9me098fjoiasnudo8f7am9sod8ufnoaisdunfkuasdf',</b>
  <b>defaultCourseId: 53450,</b>
});

<b>/**</b>
 <b>* Create a unique test assignment within the sandbox course</b>
 <b>* @author Gabe Abrams</b>
 <b>* @returns assignment object that was created</b>
 <b>*/</b>
<b>const createTestAssignment = async () => {</b>
  <b>// Generate a unique assignment name</b>
  <b>const uniqueAssignmentName = `Test Assignment [${Date.now()}-${Math.random()}]`;</b>

  <b>// Create an assignment</b>
  <b>const assignment = await api.course.assignment.create({</b>
    <b>name: uniqueAssignmentName,</b>
    <b>submissionTypes: ['none'],</b>
    <b>published: true,</b>
  <b>});</b>

  <b>// Return the new assignment</b>
  <b>return assignment;</b>
<b>};</b>

<b>/**</b>
 <b>* Create a unique test page within the sandbox course</b>
 <b>* @author Gabe Abrams</b>
 <b>* @returns page object that was created</b>
 <b>*/</b>
<b>const createTestPage = async () => {</b>
  <b>// Generate a unique page title</b>
  <b>const uniquePageTitle = `Test Page [${Date.now()}-${Math.random()}]`;</b>

  <b>// Create a page</b>
  <b>const page = await api.course.pages.create({</b>
    <b>title: uniquePageTitle,</b>
    <b>body: 'This is a test page.',</b>
    <b>published: true,</b>
  <b>});</b>

  <b>// Return the new assignment</b>
  <b>return assignment;</b>
<b>};</b>

<b>// Run create + list tasks in parallel</b>
<b>const [</b>
  <b>assignments,</b>
  <b>pages,</b>
<b>] = await Promise.all([</b>
  <b>// Create an assignment and then get the list of assignments</b>
  <b>(async () => {</b>
    <b>// Create an assignment</b>
    <b>await createTestAssignment();</b>

    <b>// Get the list of assignments</b>
    <b>const assignments = await api.course.assignment.list();</b>

    <b>// Return the list of assignments</b>
    <b>return assignments;</b>
  <b>})(),</b>
  <b>// Create a page and then get the list of pages</b>
  <b>(async () => {</b>
    <b>// Create a page</b>
    <b>await createTestPage();</b>

    <b>// Get the list of pages</b>
    <b>const pages = await api.course.page.list();</b>

    <b>// Return the list of pages</b>
    <b>return pages;</b>
  <b>})(),</b>
<b>]);</b>
</pre>
</details>
<!-- End Example -->

### Error Handling

With asynchronous code, error handling is nearly the same: simply wrap your code in a `try/catch` block:

```ts
// Async task that doesn't return anything
try {
  await doAsyncTask();
} catch (err) {
  // Handle error
}

// Async task that returns something
let userEmail: string;
try {
  userEmail = await getUserEmail();
} catch (err) {
  // Handle error
}
```

The most important thing to remember is that asynchronous tasks must be _awaited from inside the try/catch_ otherwise, code execution will continue and leave the `try/catch` block before the error occurs.

When handling errors that occur in `Promise.all` parallel execution, it's important to note that `Promise.all` throws an error immediately as soon as any of the promises passed into it throw an error. If an error occurs, only the first error will be thrown by `Promise.all`. Other tasks will continue to execute, but their results will be ignored.

If you don't want all of the tasks in the `Promise.all` to be ignored if one of the tasks encounters an error, simply group them together and wrap the internal tasks with `try/catch` blocks. The best way to explain this is by example:

Here's what it would look like if we wanted the code to quit if any of the tasks fail:

```ts
try {
  const [
    pages,
    assignments,
    serverList,
  ] = await Promise.all([
    api.course.page.list(),
    api.course.assignment.list(),
    getListOfServers(),
  ]);
} catch (err) {
  // Handle error
}
```

However, let's say that we want it to work such that if one of two first Canvas-based tasks fails, we don't want the `getListOfServers` task to be ignored. We could separate the Canvas-based tasks into a separate asynchronous function and handle the error within that function:

```ts
/**
 * Load pages and assignments. If a failure occurs, instead of failing, we
 *   will return an empty array
 * @author Gabe Abrams
 * @returns pages and assignments
 */
const loadCanvasData = async () => {
  try {
    const [
      pages,
      assignments,
    ] = await Promise.all([
      api.course.page.list(),
      api.course.assignment.list(),
    ]);

    return {
      pages,
      assignments,
    };
  } catch (err) {
    return {
      pages: [],
      assignments: [],
    };
  }
};

try {
  const [
    canvasData,
    serverList,
  ] = await Promise.all([
    loadCanvasData(),
    getListOfServers(),
  ]);

  const {
    pages,
    assignments,
  } = canvasData;
} catch (err) {
  // Handle error
}
```

If the tasks are simple and it's convenient to put the asynchronous task inline, you can skip the step of creating a named function by instead creating an anonymous function and immediately calling it:

```ts
try {
  const [
    canvasData,
    serverList,
  ] = await Promise.all([
    (async () => {
      try {
        const [
          pages,
          assignments,
        ] = await Promise.all([
          api.course.page.list(),
          api.course.assignment.list(),
        ]);

        return {
          pages,
          assignments,
        };
      } catch (err) {
        return {
          pages: [],
          assignments: [],
        };
      }
    })(),
    getListOfServers(),
  ]);

  const {
    pages,
    assignments,
  } = canvasData;
} catch (err) {
  // Handle error
}
```

### Callbacks

Refrain from using callbacks unless absolutely necessary. If it's a lib function that requires a callback, wrap it in a helper and then use the helper.

<Rule>
  Refrain from using callbacks. If a lib requires one, wrap and forget it
</Rule>

```ts
// Bad:
setTimeout(task, 1000);

// Good:
/**
 * Wait for a specific amount of time
 * @author Gabe Abrams
 * @param msToWait the number of ms to wait before continuing
 */
const waitFor = async (msToWait: number) => {
  return new Promise((resolve) => {
    setTimeout(resolve, msToWait);
  });
};

await waitFor(1000);
task();
```

# React

All our front-end development are done within the React framework. We pair our React apps with the following technologies:

- [Bootstrap v5](https://getbootstrap.com/docs) for Styling
- [FontAwesome](https://fontawesome.com) for Glyphs

In favor of built-in React functionality, we do not use:

- Redux

We no longer use any of the following technologies:

- jQuery

Features to use only after a discussion with the team because these features require everyone to be on the same page:

- React Context Providers (useContext hook)

## Organize the Project

We organize our React projects with the following file structure:

```ts
client/src/
  index.tsx // Entry point
  App.tsx // Main component
  Menu.tsx // Non-shared component
  shared/
    styles/
      style.scss // Main shared stylesheet
    constants/
      MY_SHARED_CONSTANT.tsx // A shared constant
    helpers/
      mySharedHelper.tsx // A shared helper
    MySharedComponent.tsx // A shared component
  ...
```

## Create a Component

Each project will either use class-based or functional components, but will not mix and match. New projects will always use functional components. 

<Rule tall>
  Projects do not mix and match functional vs class-based components
</Rule>

<Rule tall>
  New projects use functional components only
</Rule>

All file management rules apply to components as well (naming conventions, file vs folder modules, etc.), so be sure to check out the section earlier in this guide.

All components must follow a shared structure. Sections that are not used may be left out, but any included sections must be formatted appropriately, named properly, and in the same order as below:

<Rule>
  Components must follow our template formatting, order, and naming
</Rule>

```ts
/**
 * Add component description
 * @author Add Your Name
 */

// Import React
import React, { useReducer, useEffect, useRef } from 'react';

// Import FontAwesome
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
import { faCheck } from '@fortawesome/free-solid-svg-icons';

// Import shared helpers
import addHelperName from './addHelperFilename';

// Import shared constants
import ADD_CONSTANT_NAME from './addConstantFilename';

// Import shared types
import AddSharedTypeName from './AddSharedTypeFilename';

// Import shared components
import AddSharedComponentName from './AddSharedComponentFilename';

// Import helpers
import addHelperName from './addHelperFilename';

// Import constants
import ADD_CONSTANT_NAME from './addConstantFilename';

// Import types
import AddTypeName from './AddSharedTypeFilename';

// Import components
import AddComponentName from './AddComponentFilename';

// Import style
import './AddNameOfStylesheet.scss';

/*------------------------------------------------------------------------*/
/* -------------------------------- Types ------------------------------- */
/*------------------------------------------------------------------------*/

// Props definition
type Props = {
  // Add description of required prop
  addPropName: addPropType,
  // Add description of optional prop
  addPropName?: addPropType,
};

// Add description of custom type
type AddCustomTypeName = {
  // Add description of property
  addCustomPropName: addCustomPropType,
};

/*------------------------------------------------------------------------*/
/* ------------------------------ Constants ----------------------------- */
/*------------------------------------------------------------------------*/

// Add description of constant
const ADD_CONSTANT_NAME = 'add constant value';

/*------------------------------------------------------------------------*/
/* -------------------------------- State ------------------------------- */
/*------------------------------------------------------------------------*/

/* -------------- Views ------------- */

enum View {
  // Add description of view
  AddViewName = 'AddViewName',
}

/* -------- State Definition -------- */

type State = (
  | {
    // Current view
    view: View.AddViewName,
    // Add description of require state variable
    addStateVariableName: addStateVariableValue,
    // Add description of optional state variable
    addStateVariableName?: addStateVariableValue,
  }
  | {
    // Current view
    view: View.AddViewName,
    // Add description of require state variable
    addStateVariableName: addStateVariableValue,
    // Add description of optional state variable
    addStateVariableName?: addStateVariableValue,
  }
);

/* ------------- Actions ------------ */

// Types of actions
enum ActionType {
  // Add description of action type
  AddActionTypeName = 'AddActionTypeName',
}

// Action definitions
type Action = (
  | {
    // Action type
    type: ActionType.AddActionTypeName,
    // Add description of required payload property
    addPayloadPropertyName: addPayloadPropertyType,
    // Add description of optional payload property
    addPayloadPropertyName?: addPayloadPropertyType,
  }
  | {
    // Action type
    type: (
      | ActionType.AddActionTypeWithNoPayload
      | ActionType.AddActionTypeWithNoPayload
    ),
  }
);

/**
 * Reducer that executes actions
 * @author Add Your Name
 * @param state current state
 * @param action action to execute
 * @returns updated state
 */
const reducer = (state: State, action: Action): State => {
  switch (action.type) {
    case ActionType.AddActionType: {
      return {
        ...state,
        addStateVariableName: addStateVariableNewValue,
      };
    }
    default: {
      return state;
    }
  }
};

/*------------------------------------------------------------------------*/
/* --------------------------- Static Helpers --------------------------- */
/*------------------------------------------------------------------------*/

/**
 * Add description of helper
 * @author Add Your Name
 * @param addArgName add arg description
 * @param addArgName add arg description
 * @returns add return description
 */
const addHelperName = (
  addRequiredArgName: addRequiredArgType,
  addOptionalArgName?: addOptionalArgType,
  addOptionalArgWithDefaultName?: addOptionalArgType = addArgDefault,
): addReturnType => {
  // TODO: implement
};

/*------------------------------------------------------------------------*/
/* ------------------------------ Component ----------------------------- */
/*------------------------------------------------------------------------*/

const AddComponentName: React.FC<Props> = (props) => {
  /*------------------------------------------------------------------------*/
  /* -------------------------------- Setup ------------------------------- */
  /*------------------------------------------------------------------------*/

  /* -------------- Props ------------- */

  // Destructure all props
  const {
    addRequiredPropName,
    addOptionalPropName = 'add default value of prop',
  } = props;

  /* -------------- State ------------- */

  // Initial state
  const initialState: State = {
    addStateVariableName: 'add state variable initial value',
  };

  // Initialize state
  const [state, dispatch] = useReducer(reducer, initialState);

  // Destructure common state
  const {
    addStateVariableName,
    addStateVariableName,
  } = state;

  /* -------------- Refs -------------- */

  // Initialize refs
  const addRefName = useRef<AddRefType>(null);

  /*------------------------------------------------------------------------*/
  /* ------------------------- Component Functions ------------------------ */
  /*------------------------------------------------------------------------*/

  /**
   * Add component helper function description
   * @author Add Your Name
   * @param addArgName add description of argument
   * @param [addOptionalArgName] add description of optional argument
   * @returns add description of return
   */
  const addComponentHelperFunctionName = (
    addArgName: addArgType,
    addOptionalArgName?: addOptionalArgType,
  ): addReturnType => {
    // TODO: implement
  };

  /*------------------------------------------------------------------------*/
  /* ------------------------- Lifecycle Functions ------------------------ */
  /*------------------------------------------------------------------------*/

  /**
   * Mount
   * @author Add Your Name
   */
  useEffect(
    () => {
      (async () => {
        // TODO: implement
      })();
    },
    [],
  );

  /**
   * Update (also called on mount)
   * @author Add Your Name
   */
  useEffect(
    () => {
      // TODO: implement
    },
    [addTriggerVariable],
  );

  /**
   * Unmount
   * @author Add Your Name
   */
  useEffect(
    () => {
      return () => {
        // TODO: implement
      };
    },
    [],
  );

  /*------------------------------------------------------------------------*/
  /* ------------------------------- Render ------------------------------- */
  /*------------------------------------------------------------------------*/

  /*----------------------------------------*/
  /* ---------------- Modal --------------- */
  /*----------------------------------------*/

  // Modal that may be defined
  let modal: React.ReactNode;

  /* ------- AddFirstTypeOfModal ------ */

  if (addLogicToDetermineIfModalIsVisible) {
    // TODO: implement

    // Create modal
    modal = (
      <Modal
        key="unique-modal-key"
        ...
      />
    );
  }

  /*----------------------------------------*/
  /* ---------------- Views --------------- */
  /*----------------------------------------*/

  // Body that will be filled with the current view
  let body: React.ReactNode;

  /* -------- AddFirstViewName -------- */

  if (view === View.AddViewName) {
    // TODO: implement

    // Create body
    body = (
      <addJSXOfBody />
    );
  }

  /* -------- AddSecondViewName -------- */

  if (view === View.AddViewName) {
    // TODO: implement

    // Create body
    body = (
      <addJSXOfBody />
    );
  }

  /*----------------------------------------*/
  /* --------------- Main UI -------------- */
  /*----------------------------------------*/

  return (
    <addContainersForBody>
      {/* Add Modal */}
      {modal}

      {/* Add Body */}
      {body}
    </addContainersForBody>
  );
};

/*------------------------------------------------------------------------*/
/* ------------------------------- Wrap Up ------------------------------ */
/*------------------------------------------------------------------------*/

// Export component
export default AddComponentName;

```

## Component Development Practices

The template above is highly involved, so let's break it down into pieces. Remember that you can leave any sections out if they are irrelevant. For example, if your component does not have any state, leave out the entire section.

Let's go from top to bottom.

### Documentation

We use JSDoc to document each file and every single function. Add one or more author tags to every single JSDoc entry.

Here's an example for a forgot password button:

<Rule>
  Add JSDoc to the top of every component file, describing the component
</Rule>

```ts
/**
 * Button that shows the "forgot password" panel
 * @author Divardo Calicci
 */
```

<Rule tall>
  Add JSDoc to the top of every named function
</Rule>

### Git Norms

**Commit frequently**. We will squash later, but it's nice to have a detailed history. Plus, this is great for your careers.

### CSS Names

<Rule>
  When naming css classes, always prefix every class with the name of the component
</Rule>

```css
/* For component Favorite Fruits: */

/* Good: */
.FavoriteFruits-container

/* Bad: */
.container
```

### CSS Units

We prefer **rem** for elements that have the same sizing, independent of their context (independent of their parent styling and size).

We prefer **em** for elements that have variable sizing where their sizing depends on their parent or context.

Why? When people customize their browser settings (fonts, font size, viewport settings, etc.) it will mess up your layout and create unexpected layouts. Plus, this makes your tool more accessible (it adapts better to user settings).

<Rule tall>
  Use rem or em units instead of px units
</Rule>

### Imports

We aggressively divide imports by type because components often end up with many imports.

First, we import libraries such as `react`. Then, we import any local files

<Rule>
  Import libraries before importing any local modules
</Rule>

```ts
// Import Lib
import Lib from 'lib';

// Import AnotherLib
import AnotherLib from 'another-lib';

// Import LocalModule
import LocalModule from 'local-module';
```

Additionally, we divide all local modules into categories. Up first are shared imports (items that are also imported by other modules), then we have non-shared imports (items that are not imported by any other module). We divide each of these into sub-categories: helpers, constants, types, and components.

<Rule>
  Group local imports
</Rule>

```ts
// Import shared helpers
import addHelperName from './addHelperFilename';

// Import shared constants
import ADD_CONSTANT_NAME from './addConstantFilename';

// Import shared types
import AddSharedTypeName from './AddSharedTypeFilename';

// Import shared components
import AddSharedComponentName from './AddSharedComponentFilename';

// Import helpers
import addHelperName from './addHelperFilename';

// Import constants
import ADD_CONSTANT_NAME from './addConstantFilename';

// Import types
import AddTypeName from './AddSharedTypeFilename';

// Import components
import AddComponentName from './AddComponentFilename';
```

Finally, always import resources (images, etc.) and stylesheets last. These are the only imports that can include file extensions.

<Rule>
  Import the stylesheet last
</Rule>

```ts
// Import style
import './AddNameOfStylesheet.scss';
```

<Rule tall>
  Only stylesheet and resource imports can include file extensions
</Rule>

### Types

The first type in your types section must always be your `Props` (if your component has any).

<Rule tall>
  Props must be at the top of the "Types" section
</Rule>

Remember that optional props must be marked with the `?` symbol. We put default props in the "Set Up" section inside of the component itself, so leave out the defaults here.

Example:

```ts
// Props definition
type Props = {
  // User's first name
  userFirstName: string,
  // User's last name
  userLastName: string,
  // True if the user is a teacher
  isTeacher?: boolean,
  // Handler for when the user wants to log in
  onLogInClicked?: () => void,
};
```

### Constants

All constants are named with all caps, words separated by underscores. We do this because the `const` keyword is ubiquitous throughout our code, so `const` does not always indicate that something is a module constant.

<Rule>
  Constants use ALL_CAPS_NAMING
</Rule>

```ts
// Duration of fade out animation
const FADE_OUT_DURATION = 1500; // ms
```

Remember that all numbers must include their units.

<Exercise tall>
  Create a simple button component that takes a label, onClick function, variant, and ariaLabel as props
</Exercise>

### State

You may be familiar with the React `useState` hook. We take a more rigorous approach to component state, always requiring that state be managed by reducers. This forces us to keep our views and controllers separate. Thus, we achieve a fully separate MVC design.

<Rule tall>
  Use reducers to manage state
</Rule>

For components that have different views, define a `View` enum and base state definitions on the view. In our example, the component is a checkout panel.

<Rule>
  Create a View enum for components that have more than one view
</Rule>

```ts
enum View {
  // View the cart
  Cart = 'Cart',
  // Add shipping and billing information
  ShippingAndBillingForm = 'ShippingAndBillingForm',
  // Review order details and confirm
  Review = 'Review',
}
```

Then, base the sate off of views. Each view should have a separate state definition.

```ts
type State = (
  | {
    // Current view
    view: View.Cart,
    // List of items that are in the cart
    cart: Items[],
  }
  | {
    // Current view
    view: View.ShippingAndBillingForm,
    // List of items that are being purchased
    cart: Items[],
    // Shipping information
    shippingInformation: {
      // Shipping address
      address: Address,
      // Delivery instructions
      deliveryInstructions: string,
      // Phone number
      phone: PhoneNumber,
    },
    // Billing information
    billingInformation: (
      | {
        // True if same as shipping information
        sameAsShippingInformation: true,
      }
      | {
        // True if same as shipping information
        sameAsShippingInformation: false,
        // Billing address
        address: Address,
        // Phone number
        phone: PhoneNumber,
      }
    ),
  }
  | {
    // Current view
    view: View.Review
    // Identifier of the pending transaction
    transactionId: string,
    // True if the user has accepted the terms
    termsAccepted: boolean,
  }
);
```

If the component only has one view, leave out the `View` enum and create a state that has only one form:

```ts
type State = {
  // List of email recipients
  recipients: EmailAddress[],
  // List of CC recipients
  ccRecipients?: EmailAddress[],
  // Text typed into the email subject line
  subject: string,
  // Text typed into the body of the email
  body: string,
  // True if the "sending" indicator is visible
  sending: boolean,
};
```

We use reducers to manage state. That means that all state updates are handled through actions. This helps us to abstract away state updates, and helps state updates to be more reusable.

First, we create an `ActionType` enum that defines all of the types of actions that can be dispatched.

<Rule>
  All actions must have a separate ActionType
</Rule>

```ts
// Types of actions
enum ActionType {
  // Add a recipient to the email
  AddRecipient = 'AddRecipient',
  // Update the subject of the email
  UpdateSubject = 'UpdateSubject',
  // Reset the entire email form
  ResetForm = 'ResetForm',
  // Show the "email is being sent" indicator
  ShowSendingIndicator = 'ShowSendingIndicator',
}
```

Then, define the type of each action object. If the action has any payload properties, give it a separate Action type definition. Then, group all actions that have no payload at the bottom into one shared type definition.

<Rule>
  Define every action type with payload separately, group payload-less actions
</Rule>

```ts
// Action definitions
type Action = (
  | {
    // Action type
    type: ActionType.AddRecipient,
    // Email address of the recipient
    recipient: EmailAddress,
  }
  | {
    // Action type
    type: ActionType.UpdateSubject,
    // New text in the subject line
    subject: string,
  }
  | {
    // Action type
    type: (
      | ActionType.ResetForm
      | ActionType.ShowSendingIndicator
    ),
  }
);
```

Finally, create a reducer that executes the state updates. This function can get quite involved, so remember to keep it very organized. If using the spread operator (`...`) to merge state, always put `...state` as the first element in the list so properties are overwritten.

```ts
/**
 * Reducer that executes actions
 * @author Divardo Calicci
 * @param state current state
 * @param action action to execute
 * @returns updated state
 */
const reducer = (state: State, action: Action): State => {
  switch (action.type) {
    case ActionType.AddRecipient: {
      return {
        ...state,
        recipients: [...state.recipients, action.recipient],
      };
    }
    case ActionType.UpdateSubject: {
      return {
        ...state,
        subject: action.subject,
      };
    }
    case ActionType.ResetForm: {
      return {
        recipients: [],
        ccRecipients: [],
        subject: '',
        body: '',
        sending: false,
      };
    }
    case ActionType.ShowSendingIndicator: {
      return {
        ...state,
        sending: true,
      };
    }
    default: {
      return state;
    }
  }
};
```

Switch statements in Typescript (and Javascript) share a block scope, so it can get very confusing to reason about logic. Thus, we wrap each case in a closure.

<Rule>
  Switch cases must be wrapped in curly brace closures
</Rule>

```ts
// Bad:
switch (expression) {
  case value1:
    ...
  case value2:
    ...
  default:
    ...
}

// Good:
switch (expression) {
  case value1: {
    ...
  }
  case value2: {
    ...
  }
  default: {
    ...
  }
}
```

If some of your actions can only be dispatched from within specific views, break your reducer into multiple sections surrounded with `if` statements:

```ts
/**
 * Reducer that executes actions
 * @author Divardo Calicci
 * @param state current state
 * @param action action to execute
 * @returns updated state
 */
const reducer = (state: State, action: Action): State => {
  /* --------- Assignment List -------- */
  
  if (state.view === View.AssignmentList) {
    switch (action.type) {
      case ActionType.FilterAssignments: {
        ...
      }
      default: {
        return state;
      }
    }
  }

  /* ------------ Page List ----------- */

  if (state.view === View.PageList) {
    switch (action.type) {
      case ActionType.FilterPages: {
        ...
      }
      default: {
        return state;
      }
    }
  }

  /* ------------- Default ------------ */

  return state;
};
```

<Exercise tall>
  Create a closeable alert that becomes invisible after being closed
</Exercise>

### Static Helpers

If logic can be removed from the component because it does not depend on state or props, either create a small static helper or move the logic to another file and import it under "Import Helpers".

<Rule tall>
  Static helpers and imported helpers should not heavily rely on state or props
</Rule>

Otherwise, static helpers follow usual rules: add JSDoc, types, etc.

```ts
/**
 * Get time of day
 * @author Divardo Calicci
 * @param timezone timezone of the current user
 * @returns text describing the time of day
 */
const getTimeOfDay = (timezone: Timezone): string => {
  ...
};
```

### Component Setup

The first thing that happens inside the component function is labeled "Setup" and it contains initialization for the props and state.

First, destructure props and include default props directly inline.

```ts
// Destructure all props
const {
  name,
  email,
  age,
  isTeacher = false,
  profileColor = Color.Blue,
} = props;
```

Then, define the initial state. In this way, default props and state are right next to each other and easy to find.

```ts
// Initial state
const initialState: State = {
  isOnline: false,
};
```

Then, initialize the state and destructure all state variables that are shared amongst all forms of the state.

```ts
// Initialize state
const [state, dispatch] = useReducer(reducer, initialState);

// Destructure common state
const {
  isOnline,
} = state;
```

Finally, initialize refs (if you have any).

```ts
// Initialize refs
const inputElem = useRef<HTMLInputElement>(null);

...

<input ref={inputElem} ...
```

To get the element attached to a ref, use `inputElem.current`.

### Lifecycle Functions

React programmers often speak about the "lifecycle" of a component. When a component first is included in the UI, we say that the component is "Mounted". Then, when the props or state change, we say that the component "Updated". Note that when the component first receives its props and state (during the mount step), we also consider this as an update. Finally, when the component leaves the UI, we say that the component is "Unmounted". We use three different types of lifecycle functions if we want to trigger code when one of these lifecycle states occurs.

#### Mount

To trigger code when the component mounts, we add a `useEffect(handler, [])` hook.

```ts
/**
 * Mount
 * @author Divardo Calicci
 */
useEffect(
  () => {
    // TODO: implement
  },
  [],
);
```

The "Mount" lifecycle function is great for running any asynchronous loading code (example: API request). If your code is asynchronous, wrap it in an anonymous async function. This trick works for any other lifecycle function, but we will only show it used here.

```ts
/**
 * Mount
 * @author Divardo Calicci
 */
useEffect(
  () => {
    (async () => {
      // Check if the user is online
      const { isOnline } = await getUserState();

      // Update the sate
      dispatch({
        type: ActionType.CHANGE_USER_STATUS,
        isOnline,
      });
    })();
  },
  [],
);
```

#### Update

To trigger code when a prop or state variable changes, we use a `useEffect(handler, [trigger])` hook. The trigger array can be one or more props and/or state variables that will cause the handler to be called. We recommend keeping your trigger array as concise as possible.

```ts
/**
 * Update (also called on mount)
 * @author Divardo Calicci
 */
useEffect(
  () => {
    // Play a "message received" sound
    audioPlayer.play(Sound.MessageReceived);
  },
  [messages],
);
```

If you need multiple different "Update" lifecycle functions with different triggers, add multiple "Update" functions, each with a different trigger array.

You may hear about another usage for the `useEffect` hook where the trigger array is left out completely: `useEffect(handler)`, which corresponds to a trigger that happens whenever _anything_ changes. Refrain from using this hook unless it's absolutely necessary. Usually, if you want to use this hook, that means that either you are doing logic that will need to happen every render (so it might as well be part of the render function), or your logic doesn't need to be run that frequently (so you should be more careful with when your logic runs, which you do by adding a trigger array).

<Rule tall>
  Always include a trigger array with the useEffect hook
</Rule>

#### Unmount

To trigger code when a component leaves the UI, we return a handler function within a `useEffect(handler, [])` hook. This is a great lifecycle function for cleanup.

```ts
/**
 * Unmount
 * @author Divardo Calicci
 */
useEffect(
  () => {
    return () => {
      // Save the user's changes
      saveChanges();
    };
  },
  [],
);
```

<Exercise tall>
  Create an app that lists the assignments in the course and allows the user to delete an assignment
</Exercise>

#### useEffect Hook

In each of the lifecycle functions we learned above, you'll see effective usage of the `useEffect` hook, which is one of the more complex hooks. It's not necessary that you fully understand this hook in order to do software development at DCE, but it's a good hook to understand. Thus, we'll go over it in some detail just for fun. This is a slightly simplified and modified description, see the docs for full detail.

The `useEffect` hook is used to watch for changes to prop variables (so we can make updates when prop variables change) and also to watch for destruction of such variables (we we can do cleanup). Here's how it works:

`useEffect` takes two arguments. The first argument is the effect function that is called when the changes are detected. The second argument is the list of prop variables to watch.

When any of the prop variables in the list change, the effect function is called. Also, on mount, those prop variables go from not existing to having values (that counts as a change), so the effect function is called on mount. The effect function contains the code that React should run when the changes are detected, and that is quite straightforward. But, the effect function also does something a little tricky: it's allowed to return another function (a cleanup function) that will be called when the component unmounts (this is a simplification).

Let's go through a few examples to make sense of this:

```ts
useEffect(
  () => {
    console.log('Hello!');
  },
  [],
);
```

In the example above, the array of prop variables to watch is empty. Thus, the effect function will be called on mount (because it's always called on mount) but will not be triggered at any point afterward. The effect function contains just a console.log and does not return a cleanup function, so there is no code here that will be called upon unmount. That's why we consider this `useEffect` usage to be a "Mount" function.

```ts
useEffect(
  () => {
    console.log('Hello!');
  },
  [users],
);
```

In the example above, the array of prop variables contains the "users" prop. Thus, the effect function will be called on mount and will also be called whenever the "users" prop changes value. The effect function contains just a console.log and does not return a cleanup function, so there is no code here that will be called upon unmount. That's why we consider this `useEffect` usage to be an "Update" function.

```ts
useEffect(
  () => {
    return () => {
      console.log('Hello!');
    };
  },
  [],
);
```

In the example above, the array of prop variables to watch is empty. Thus, the effect function will be called on mount (because it's always called on mount) but will not be triggered at any point afterward. The effect function only contains a return statement and does not run any other code, so in effect, there is no code to run on mount but there is code to run on unmount (the returned function will be called on unmount). That's why we consider this `useEffect` usage to be an "Unmount" function.

At DCE, these are the only three usages that we'll allow for `useEffect`, but at other organizations they may allow much more complex `useEffect` implementations. We keep things simple and clear for understandability and readability.

<Rule tall>
  Only use the "useEffect" hook statements that are listed in the template
</Rule>

### Render

You may have noticed that we separate sections of our code with comment blocks. Aside from the usual very large and wide comment block delimiting sections of the code, we use two smaller types of comment blocks to organize our render functions.

Medium blocks to separate parts of the UI:

```ts
/*----------------------------------------*/
/* ---------------- Modal --------------- */
/*----------------------------------------*/
```

And line comments to organize different types of that part of the UI:

```ts
/* ----------- Error Modal ---------- */
```

```ts
/* ------- Confirmation Modal ------- */
```

<Rule tall>
  Use comment blocks and lines to organize render code
</Rule>

When rendering views, it is okay to use `if` statements along with the `view` state variable (instead of `if` `else if` logic) because this keeps our code separate and readable.

At the end of the component's render code, there should be just one return statement that returns the main UI.

<Rule>
  Components can have only one return statement
</Rule>

```tsx
/*----------------------------------------*/
/* --------------- Main UI -------------- */
/*----------------------------------------*/

return (
  <div className="EmailForm-outer-container">
    {/* Add Modal */}
    {modal}

    {/* Add Body */}
    {body}
  </div>
);
```

### Wrap Up

This final section is usually very short. Put any final export logic here.

```ts
// Export component
export default EmailForm;
```

<Rule tall>
  Default export must happen at the end of the file on one line
</Rule>

<Rule>
  Default export cannot directly export a value
</Rule>

```ts
// Bad:
export default 50;

// Bad:
export default {
  ...
};

// Good:
export default myVariableName;

// Good:
export default MyClass;
```

## Writing JSX

Writing JSX code takes some getting used to. In many cases, it looks and feels just like HTML, but on certain cases, it differs in very small ways. Let's go through JSX by reviewing some of my favorite tips.

### Injecting Typescript

JSX is a combination of HTML and Typescript. The most important thing you'll learn about JSX is how to inject typescript into html. Typescript is always surrounded by `{...}` within our JSX blocks. Let's learn through examples:

Add a dynamically generated template string for the button aria-label:

```jsx
<button
  type="button"
  className="btn btn-warning"
  aria-label={`log out ${currentUserName}`}
>
  Log Out
</button>
```

Add a variable as the value for an onClick function:

```jsx
<button
  type="button"
  className="btn btn-warning"
  onClick={logOut}
>
  Log Out
</button>
```

Add an inline function that's called when the user clicks a button:

```jsx
<button
  type="button"
  className="btn btn-warning"
  onClick={() => {
    console.log('Logging out now!');
  }}
>
  Log Out
</button>
```

This works for props and also normal html contents:

```jsx
<button
  type="button"
  className="btn btn-warning"
>
  Log Out
  {' '}
  {numActiveUsers}
  {' '}
  Users
</button>
```

Any typescript can be placed inside the `{...}`, for example, math:

```jsx
<button
  type="button"
  className="btn btn-warning"
>
  Log Out
  {' '}
  {numActiveUsers + 1}
  {' '}
  Users
</button>
```

We can also use conditional logic, just like usual in typescript:

```jsx
<button
  type="button"
  className="btn btn-warning"
>
  {
    numActiveUsers === 1
      ? 'Log Out Current User'
      : `Log Out ${numActiveUsers} Users`
  }
</button>
```

### Classes

Instead of using `class="..."`, we use `className="..."` in JSX.

### Events

In HTML, event handlers are named in all lowercase like `onmousedown` but in JSX, we use camel case like `onMouseDown`.

### Spaces in JSX

To add a normal breaking space, use `{' '}` on its own line.

To add a non-breaking space, use `&nbsp;`.

### Quotes and Other Symbols

To keep our JSX clean and to help with rendering, we always encode symbols.

<Rule tall>
  Always encode symbols in JSX
</Rule>

Here are a few for reference:

- `&` becomes `&amp;`
- `<` becomes `&lt;`
- `>` becomes `&gt;`
- `"` becomes `&quot;`
- `'` becomes `&apos;`
- `¢` becomes `&cent;`
- `©` becomes `&copy;`
- `®` becomes `&reg;`

### Modals

All modals should be `dce-reactkit` modals with unique keys.

<Rule>
  All modals must have unique keys
</Rule>

```ts
<Modal
  key="unique-modal-key"
  ...
/>
```

### FontAwesome Icons

To add a FontAwesome icon, make sure the icon is imported. For example, if we want a checkmark, we will import the `faCheck` icon:

```ts
// Import FontAwesome
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
import { faCheck } from '@fortawesome/free-solid-svg-icons';
```

Usually, icon names are just the camelCase versions of the icon name, but autocomplete should help you here.

Then, when you want to use the icon, include it like this:

```html
<FontAwesomeIcon icon={faCheck} />
```

You can also add a `className` prop to `FontAwesomeIcon` for bootstrap styles:

```html
<FontAwesomeIcon
  icon={faCheck}
  className="m-2"
/>
```

### Self-closing Tags

In HTML, you may see a tag that has no contents:

```html
<div id="LoginButton-container"></div>
```

...but in JSX, we use self-closing tags:

```tsx
<div id="LoginButton-container" />
```

<Rule tall>
  Use self-closing tags for elements with no children
</Rule>

## Dispatching Actions

We spent a lot of time defining the state and reducer, but how do you dispatch an action to the reducer?

Simple: call the `dispatch` function and pass an object with a `type` property and any other payload properties that are defined for that action type.

```ts
dispatch({
  type: ActionType.UpdateSubject,
  subject: inputField.value,
});
```

## Design Principles

### Prefer Multiline Representations

Unless something in JSX has just one item, put it on multiple lines. This keeps our UI code very clean and readable.

<Rule>
  Prefer multiline JSX
</Rule>

```tsx
{/* Good */}
<div id="LoginButton-container" />

{/* Equally Good */}
<div
  id="LoginButton-container"
/>

{/* Bad */}
<div id="LoginButton-container" className="row" />

{/* Good */}
<div
  id="LoginButton-container"
  className="row"
/>
```

### One Language Per Line

In JSX file, we mix and match typescript and html code.

Unless you're embedding a single variable:

```tsx
<button
  onClick={handleClick}
  ...
```

...or you're embedding a single value:

```tsx
<button
  type="button"
  ...
```

...don't mix and match typescript and html code on the same line.

<Rule>
  Don't mix typescript and JSX
</Rule>

```tsx
{/* Bad: */}
<button
  onClick={() => { handleClick(); }}
  ...
/>

{/* Good: */}
<button
  onClick={() => {
    handleClick();
  }}
  ...
/>

{/* Bad: */}
<div className="Role-description">
  You are a {user.role} in the course.
</div>

{/* Good: */}
<div className="Role-description">
  You are a
  {' '}
  {user.role}
  {' '}
  in the course
</div>
```

### Shared State

If state must be shared between multiple components, put those state variables in the lowest common ancestor and pass state down to children via props.

This can cause what is called "prop drilling", where state is passed through multiple layers of children via their props. If this becomes particularly cumbersome, it might be one of the cases where we use a React Context Provider to create a shared state, but this needs to be a full team decision.

<Rule tall>
  Never create a React Context Provider without discussing with the rest of the team
</Rule>

### No Images

Unless absolutely necessary, never use images. Great alternatives are glyphs via `FontAwesome` or svg vector graphics. If you think that an image is required, discuss the situation with the team. We do this to aggressively keep our apps small in size. We have students all over the world, many with very slow internet connections, so load time is very important.

<Rule tall>
  Never use an image without discussing with the rest of the team
</Rule>

### "Fat" Reducers

You'll often hear the term "fat" vs "thin" reducers, which refers to whether logic is concentrated inside the reducer or outside the reducer, respectively. We love "fat" reducers. As much as possible, move logic into the reducer. In my opinion, "thin" reducers defeat the entire purpose of reducers. When writing "thin" reducers, you often create an entire action that just passes through state updates. In this case, you lose all of the benefits of abstraction that `useReducer` offers and you might as well just replace it with `useState`.

## Constant Modules

If you have shared constants, put them in a `constants/` folder either in `client/src/shared/` if they're shared across the whole app or put them directly in the folder for the current component if they're shared across a component and its children.

Constant modules are simple:

```tsx
// MAX_STUDENTS_PER_TABLE.tsx

/**
 * Maximum number of students allowed at a table
 * @author Divardo Calicci
 */
const MAX_STUDENTS_PER_TABLE = 500; // people

export default MAX_STUDENTS_PER_TABLE;
```

## Enum or Types Modules

If you have shared enums or types, put them in a `types/` folder either in `client/src/shared/` if they're shared across the whole app or put them directly in the folder for the current component if they're shared across a component and its children.

Type modules are simple:

```tsx
// Car.tsx

/**
 * Car type
 * @author Divardo Calicci
 */
type Car {
  // Company that made the car
  make: string,
  // Year that the car was manufactured
  year: number,
  // Color of the car
  color: AllowedColors,
}

export default Car;
```

Enum modules are simple:

```tsx
// AllowedColors.tsx

/**
 * Allowed paint colors for new cars
 * @author Divardo Calicci
 */
enum AllowedColors {
  Red = 'Red',
  Green = 'Green',
  Blue = 'Blue',
}

export default AllowedColors;
```

It seems like a lot of word to re-type the name of enum values in lowercase, but we do that for a good reason: it helps with readable serialization and database entries that are more debuggable and readable. Because this is so valuable, we require it.

<Rule>
  Enums must have string value unless the value's natural type is a number
</Rule>

```ts
// Bad:
enum AllowedColors {
  Red,
  Green,
  Blue,
}

// Good:
enum AllowedColors {
  Red = 'Red',
  Green = 'Green',
  Blue = 'Blue',
}

// Bad (allowed colors are not numbers)
enum AllowedColors {
  Red = 1,
  Green = 2,
  Blue = 3,
}

// Good (number of wheels is a number naturally)
enum VehicleWheelConfig {
  Bike = 2,
  Tricycle = 3,
  Car = 4,
  FlatbedTruck = 16,
}
```

## Helper Modules

If you have shared helpers, put them in a `helpers/` folder either in `client/src/shared/` if they're shared across the whole app or put them directly in the folder for the current component if they're shared across a component and its children.

Simply define the function and then export it.

```ts
// roundToTwoDecimals.tsx

/**
 * Round a number to two decimals
 * @author Divardo Calicci
 * @param num the number to round
 * @returns the rounded number
 */
const roundToTwoDecimals = (num: number) => {
  return (
    Math.round(
      num * 100
    )
    / 100
  );
};

export default roundToTwoDecimals;
```

### Use Bootstrap As Much As Possible

If Bootstrap has a class for the style or layout that you want to use, take advantage of Bootstrap. Check out the [Bootstrap docs](https://getbootstrap.com/docs/). They're great.

But if you must create a new style, put it in an associated `.scss` file. If that style is shared, see the next section on "Shared Styles"

## Shared Styles

If you have shared styles, put them in a `styles/` folder either in `client/src/shared/` if they're shared across the whole app or put them directly in the folder for the current component if they're shared across a component and its children.

Great candidates for these styles are:

- Shared classes like `btn-nostyle`
- Shared custom color variables
- Shared custom number variables

Generally, we try to limit the number of shared style because we use Bootstrap so much. But, as a team, we may put some shared styles into a `client/src/shared/styles/style.scss` file.

To import a stylesheet that includes variables that you'd like to use, do it with the `@use` command:

```scss
@use '../shared/styles/style.scss';
```

When defining variables, do so at the top of your scss file:

```scss
$border-width: 0.5rem;
```

# Logging

To improve our tools, inform teaching practices, and provide analytics to faculty and staff, we log user errors and actions. Because logging is done so commonly, we use a common logging service from `dce-reactkit`.

## Preparation

### Connect to DB

In your app, make sure you've followed [instructions on setting up connections to the database](#mongodocdb). Then, add another "Log" collection to your `/server/src/shared/helpers/mongo.ts` file:

Import `dce-reactkit` dependencies at the top of the file:

```ts
// Import dce-reactkit
import { initLogCollection, Log } from 'dce-reactkit';
```

Initialize the log collection near the bottom of the file:

```ts
// Logs
export const logCollection = initLogCollection(Collection) as Collection<Log>;
```

And as always, whenever you make a change to this file, increment the `schemaVersion` variable.

Then, in the server index of your app, initialize `dce-reactkit` by importing the appropriate dependencies near the top:

```ts
// Import CACCL
import initCACCL, { getLaunchInfo } from 'caccl/server';

// Import dce-reactkit
import { initServer } from 'dce-reactkit';

// Import log collection
import { logCollection } from './shared/helpers/mongo';
```

Then, within the `initCACCL`, at the top of the `express.postprocessor` function, add code to initialize `dce-reactkit` with logging:

```ts
const main = async () => {
  // Initialize CACCL
  await initCACCL({
    ...
    express: {
      postprocessor: (app) => {
        // Initialize dce-reactkit
        initServer({
          app,
          getLaunchInfo,
          logCollection,
        });

        ...
      },
    },
  });
};
...
```

### Log Organization

Now that you've set up support for logging, take some time to think through how you want to organize the logs. We'll always divide logs into `error` and `action` logs, where `action` logs contain user actions such as opening panels, clicking buttons, interacting with elements, etc. It's up to you how you want to organize your action logs.

We'll be curating a `/server/src/shared/types/LogMetadata.ts` file (that should be synched to the client as well) that will hold all of the reusable log organization metadata (which you will learn about in later sections). Add an empty file to get started:

```ts
/**
 * Log contexts, tags, and other metadata
 * @author Your Name
 */
const LogMetadata = {
  // TODO: add metadata
};

export default LogMetadata;
```

There are two ways you will organize your logs:

#### Context and Subcontext

Each action log entry must be tied to a "context" and can optionally be tied to a "subcontext" as well. You may choose for contexts to represent features in your app, where subcontexts represent subfeatures. Or perhaps contexts represent pages/panels in your app. Or perhaps contexts represent different parts of a toolbox.

Once you've determined how you want to structure your contexts and subcontexts, add a section to the `LogMetadata.ts` file. Add each context to the `LogMetadata.Context` object as a string key where the value of each key matches the key itself:

```ts
/**
 * Log contexts, tags, and other metadata
 * @author Your Name
 */
const LogMetadata = {
  // Contexts
  Context: {
    AttendancePanel: 'AttendancePanel',
    AnalyticsDashboard: 'AnalyticsDashboard',
    Roster: 'Roster',
  },
};

export default LogMetadata;
```

If your app will make use of subcontexts, simply nest the context object and move the string value to an inner key called `_` that is placed at the top of the list of children. In the following example, we have subcategories within "AnalyticsDashboard" that represent different views inside of the analytics dashboard: "StudentView", "ClassView", and "ProgramView".

```ts
/**
 * Log contexts, tags, and other metadata
 * @author Your Name
 */
const LogMetadata = {
  // Contexts
  Context: {
    AttendancePanel: 'AttendancePanel',
    AnalyticsDashboard: {
      _: 'AnalyticsDashboard',
      StudentView: 'StudentView',
      ClassView: 'ClassView',
      ProgramView: 'ProgramView',
    },
    Roster: 'Roster',
  },
};

export default LogMetadata;
```

However you choose to organize your logs, make sure you future-proof your structure so that it can grow as your app changes. It's not fun to have to go back through old log entries and perform migrations. Instead, it's best to create future-proofed contexts and subcontexts that can be augmented and expanded. To better understand future-proofing, let's discuss an example: you are working on an app called "Math Toolbox" and you anticipate that it'll eventually have lots of sub-tools with different purposes. Currently, you've only created the "Calculator" subtool.

Here's an example of poor organization where contexts are not future-proofed:

```ts
/**
 * Log contexts, tags, and other metadata
 * @author Your Name
 */
const LogMetadata = {
  // Contexts
  Context: {
    Algebra: 'Algebra',
    Calculus: 'Calculus',
    Graphing: 'Graphing',
  },
};

export default LogMetadata;
```

Each context (Algebra, Calculus, Graphing) represents one part of the current calculator app. This will become really confusing and cluttered as more tools get added to our Math Toolbox tool. Perhaps the next tool will be a data science tool or a visualization tool. When more tools get added to our Math Toolbox, our context space will get more cluttered and it'll be hard to tell which context belongs to each tool. Plus, if other tools in our Math Toolbox have similar functions (perhaps the data science tool also has a graphing function), then we would have to add another context for that other tool and we'd have to give it a confusing name like `GraphingForDataScience`.

Here's a slightly improved way to organize contexts, but even this is not good enough:

```ts
/**
 * Log contexts, tags, and other metadata
 * @author Your Name
 */
const LogMetadata = {
  // Contexts
  Context: {
    CalculatorAlgebra: 'CalculatorAlgebra',
    CalculatorCalculus: 'CalculatorCalculus',
    CalculatorGraphing: 'CalculatorGraphing',
  },
};

export default LogMetadata;
```

In the example above, at least it's clear which tool each context belongs to, but it'll still be too cluttered as we further develop the tool.

Here's an example of good future-proofing:

```ts
/**
 * Log contexts, tags, and other metadata
 * @author Your Name
 */
const LogMetadata = {
  // Contexts
  Context: {
    Calculator: {
      _: 'Calculator',
      Algebra: 'Algebra',
      Calculus: 'Calculus',
      Graphing: 'Graphing',
    },
  },
};

export default LogMetadata;
```

### Tags

Another way you can organize logs is through tags. These tags are flexible, optional, and very simple. You decide which tags to use for your app. The main thing to think about is clutter-reduction. In particular, it's easy to create an endless list of tags that are confusing and sometimes indistinguishable from each other.

If you choose to use tags, once you've decided on a list of tags, add them to your `LogMetadata.ts` file:

```ts
// Import dce-reactkit
import { LogMetadataType } from 'dce-reactkit';

/**
 * Log contexts, tags, and other metadata
 * @author Your Name
 */
const LogMetadata = {
  // Contexts
  ...
  // Tags
  Tag: {
    StudentFeature: 'StudentFeature',
    TeacherFeature: 'TeacherFeature',
    AdminFeature: 'AdminFeature',
    PilotFeature: 'PilotFeature',
    RequiresLogin: 'RequiresLogin',
    RequiresRegistration: 'RequiresRegistration',
  },
};

export default LogMetadata;
```

### Log Levels

Each log entry is assigned a "log level" which determines the type of information the log contains. For example, "warn" level logs contain critical information, "info" level logs contain normal user story information, and "debug" level logs contain highly detailed information that might be necessary for fine-grained tracking or debugging.

By default, log entries are assigned the "info" log level. If you want to use another log level, simply pass it in while logging as `level`:

```ts
logServerEvent({
  ...
  level: LogLevel.Warn,
});
```

Where `LogLevel` can be imported from `dce-reactkit`:

```ts
// Import dce-reactkit
import { LogLevel } from 'dce-reactkit';
```

### Metadata

If context, subcontext, and tags aren't enough, you can add custom metadata individually to each log entry. The intent of the metadata field is to allow complicated actions or errors to provide additional information about the event. The metadata field should be an object with string keys and simple values (strings, numbers, booleans, etc.) but the metadata field is not intended for large amounts of data (images, etc.)

To add metadata to a log entry, simply pass it in while logging as `metadata`:

```ts
logServerEvent({
  ...
  metadata: {
    my: 28,
    custom: 'metadata',
    can: 'have',
    any: {
      format: 'I want',
    },
  },
});
```

Where `metadata` can be any JSON object, however, we do prefer shallow metadata for easier querying.

### Automatically Added Organization

Whenever you log using `dce-reactkit`, a whole bunch of useful data is added to each log entry:

#### User Information

Every log entry will automatically include the following user information taken directly from the user's Canvas info:

```ts
{
  // First name of the user
  userFirstName: string,
  // Last name of the user
  userLastName: string,
  // User email
  userEmail: string,
  // User Canvas Id
  userId: number,
  // If true, the user is a learner
  isLearner: boolean,
  // If true, the user is an admin
  isAdmin: boolean,
  // If true, the user is a ttm
  isTTM: boolean,
}
```

#### Course Information

Every log entry will automatically include the following course information taken directly from the current Canvas course:

```ts
{
  // The id of the Canvas course that the user launched from
  courseId: number,
  // The name of the Canvas course
  courseName: string,
}
```

#### Device and Browser Information

Every log entry will automatically include the following course information taken from the user's session information:

```ts
{
  // Browser info
  browser: {
    // Name of the browser
    name: string,
    // Version of the browser
    version: string,
  },
  // Device info
  device: {
    // Name of the operating system
    os: string,
    // If true, device is a mobile device
    isMobile: boolean,
  },
}
```

#### Date and Time

Every log entry will automatically include the following date and time information, recorded in ET where applicable:

```ts
{
  // Calendar year that the event is from
  year: number,
  // Month that the event is from (1 = Jan, 12 = Dec)
  month: number,
  // Day of the month that the event is from
  day: number,
  // Hour of the day (24hr) when the event occurred
  hour: number,
  // Minute of the day when the event occurred
  minute: number,
  // Timestamp of event (ms since epoch)
  timestamp: number,
}
```

#### Error Source

If the log entry was created on the client, the entry will automatically include the following source flag:

```ts
{
  // Source of the event
  source: LogSource.Client,
}
```

Where `LogSource` can be found in `dce-reactkit`.

If the log entry was created on the server, the entry will automatically include the following source flag:

```ts
{
  // Source of the event
  source: LogSource.Server,
  // Route path (e.g. /api/admin/courses/53450/blocks)
  routePath: string,
  // Route template (e.g. /api/admin/courses/:courseId/blocks)
  routeTemplate: string,
}
```

Where route information is taken from express.

## Writing Logs

First, let's go over all the cases where logs are already automatically written. Whenever the `renderErrorPage` function is called from within an endpoint, that will automatically be logged. Also, whenever an error is thrown on the server from within an endpoint, that error will also automatically be logged.

To write your own logs, all you need to do is call the appropriate logging function. On the client, simply import the `logClientEvent` function from `dce-reactkit` and call it:

```ts
// Import dce-reactkit
import { logClientEvent } from 'dce-reactkit';

...

logClientEvent({
  ...
});
```

If you're on the server, from within an endpoint that is using the `genEndpointHandler` function, destructure the `logServerEvent` function from the handler's arguments and call it:

```ts
app.post(
  '/api/my/endpoint/path',
  genRouteHandler({
    ...
    handler: async ({ logServerEvent }) => {
      ...
      logServerEvent({
        ...
      });
```

Both the `logServerEvent` and `logClientEvent` functions take the same arguments. Thus, the process of logging on the server is identical to the process of logging on the client. See the section below depending on which type of log you’re making (error or action):

### Logging Errors

To log errors, call `logServerEvent` or `logClientEvent` with an "error" argument which is an Error instance:

```ts
logClientEvent({
  context: LogMetadata.Context.AnalyticsDashboard,
  error: myError,
});
```

You can also add any or all of the following: subcontext, tags, level (log level), and/or metadata:

```ts
logClientEvent({
  context: LogMetadata.Context.AnalyticsDashboard,
  error: myError,
  subcontext: LogMetadata.Context.AnalyticsDashboard.StudentView,
  tags: [LogMetadata.Tag.RequiresLogin],
  level: LogLevel.Debug,
  metadata: {
    userHasPopupBlocker: true,
  },
});
```

Where `LogLevel` can be imported from `dce-reactkit`: `import { LogLevel } from 'dce-reactkit';`.

We automatically record `error.message`, `error.code`, and `error.stack`. If you want to manually determine those, try creating a `new ErrorWithCode`:

```ts
// Import dce-reactkit
import { ErrorWithCode } from 'dce-reactkit';

...

const error = new ErrorWithCode(
  'Add a message here',
  ErrorCode.MyErrorCode,
);
```

When querying logs, note that error information is spread out across three variables for simplicity:

```ts
{
  // The error message
  errorMessage: string,
  // The error code
  errorCode: string,
  // Error stack trace
  errorStack: string,
}
```

### Logging Actions

An action is any event that is either triggered by a user or is encountered by a user. To log actions, call `logServerEvent` or `logClientEvent` with an `action` and an optional `target` argument. If the action is being performed on the context itself (for example, the user is opening the AnalyticsDashboard), then the target should be left blank. Otherwise, the target should be included and should be a target taken directly from `LogMetadata.Target`. For a full list of available types of actions, see the list of [dce-reactkit log actions](https://github.com/harvard-edtech/dce-reactkit/blob/main/src/types/LogAction.ts).

Example of opening the context:

```ts
// Import dce-reactkit
import { LogAction } from 'dce-reactkit';

...

logServerEvent({
  context: LogMetadata.Context.AnalyticsDashboard,
  action: LogAction.Open,
});
```

Example of doing an action within a context:

```ts
// Import dce-reactkit
import { LogAction } from 'dce-reactkit';

...

logServerEvent({
  context: LogMetadata.Context.AnalyticsDashboard,
  action: LogAction.Remove,
  target: LogMetadata.Target.WatchSpeedWidget,
});
```

As with errors, you can add more information to your action log entry by adding a subcontext, tags, level (log level), and/or metadata:

```ts
logClientEvent({
  context: LogMetadata.Context.AnalyticsDashboard,
  subcontext: LogMetadata.Context.AnalyticsDashboard.StudentView,
  action: LogAction.Remove,
  target: LogMetadata.Target.WatchSpeedWidget,
  tags: [
    LogMetadata.Tag.PilotFeature,
    LogMetadata.Tag.AdminFeature,
  ],
  level: LogLevel.Warn,
  metadata: {
    analyticsInHighContrastMode: false,
  },
});
```

Where `LogLevel` can be imported from `dce-reactkit`: `import { LogLevel } from 'dce-reactkit';`.

## Querying Logs

There are many ways to query the logs, but here are some tips:

### Filter by Type

Take a look at the included [dce-reactkit log types](https://github.com/harvard-edtech/dce-reactkit/blob/main/src/types/LogType.ts) and filter by one of those. For example, if querying for just actions, use this query:

```ts
{ type: 'action' }
```

### Filter by User, Course, or Role

Use `userId`, `userEmail`, `userFirstName`, and/or `userLastName` to filter to a specific user.

Use `courseId` and/or `courseName` to filter to a specific course.

Use `isLearner`, `isAdmin`, or `isTTM` to filter to specific user roles.

### Filter by Source

You can filter by where the error occurred (on the server, on the client, etc.) by taking a look at the included [dce-reactkit sources](https://github.com/harvard-edtech/dce-reactkit/blob/main/src/types/LogSource.ts). For example, if querying for server-side errors, use this query:

```ts
{ source: 'server' }
```

### Filter by Date and/or Time

You can use the `year`, `month`, `day`, `hour`, `minute`, etc. fields to query. For example, if we know that the issue occurred in January or February of 2023:

```ts
{
  year: 2023,
  month: { $in: [1, 2] },
}
```

### Filter by Action Type

If searching through action logs, you can take a look at the included [dce-reactkit action types](https://github.com/harvard-edtech/dce-reactkit/blob/main/src/types/LogAction.ts). For example, if you just want to find Open/Close/Cancel actions:

```ts
{
  action: {
    $in: ['open', 'close', 'cancel'],
  },
}
```

### Combining Filters

As usual, you can combine any of the example filters above while also adding your own custom filters to your query. For example, here's a query to find all client-side errors that students experienced in 2022:

```ts
{
  year: 2022,
  isLearner: true,
  source: 'client',
  type: 'error',
}j
```

# Express Server

## Why Express?

All of our React apps are served with an Express backend. This is a very intentional decision because it allows us to fluidly move items between the front-end and the back-end. This is possible because Express runs typescript in the same way as our React clients, plus all our dependencies can be added to either the server or the client. Finally, it allows us to share types across our server and client, instead of having to re-define them and manage two sets of types. None of this would be possible if we use a non-express, non-typescript backend (django, java, etc.).

If your app requires a server, it _must_ use Express.

## Dependencies

Make sure `caccl`, `dotenv`, and `dce-reactkit` are added to your project dependencies.

## Setting up Server

In the top-level `/server/src/index.ts` file, make sure you have the following key components of initialization:

```
// Import CACCL
import initCACCL, { getLaunchInfo } from 'caccl/server';

// Import dce-reactkit
import { initServer } from 'dce-reactkit';

// Import environment
import 'dotenv/config';

// Import route adders
import addRoutes from './addRoutes';

/**
 * Initialize app server
 * @author Your Name
 */
const init = async () => {
  // Initialize CACCL
  await initCACCL({
    express: {
      postprocessor: (app) => {
        // Initialize dce-reactkit
        initServer({
          getLaunchInfo,
        });

        // Call route adders
        addRoutes(app);
      },
    },
  });
};

// Init server and display errors
init();
```

## Server Folder Structure

All servers should generally follow this structure from within the `/server/src/` folder:

```
/index.ts – the main server file, described above
/addRoutes/index.ts – a script that calls all route adders
/addRoutes/addSomeTypeOfRoutes.ts – adds one type of routes (e.g. student API routes)
/addRoutes/addAnotherTypeOfRoutes.ts – adds one type of routes (e.g. teacher API routes)
```

Shared files go into the `/server/src/shared/` folder:

```
/constants/
/helpers/
/types/
/classes/
/interfaces/
```

<Rule tall>
  Use the server folder structure above
</Rule>

## Adding API Endpoints and Other Routes

In each server, there should be a `/server/src/addRoutes` module that contains all routes. Divide routes into sensible categories, ideally separated by feature, and put them in a nested tree structure such that the top-level `index.ts` file only needs to call one route adder: `/server/src/addRoutes/index.ts`.

For example, let's say you have an app where there are really three key features: an app store, a training locator, and a meeting scheduler. In that example, it would make sense to have three route adders: `addAppStoreRoutes`, `addTrainingLocatorRoutes` and `addMeetingSchedulerRoutes`. If those key features themselves contain subfeatures, add subfeature route adders and make the parent route adders into folders. Here's an example in action:

```
/addRoutes/index.ts – a route adder function that calls all route adder subfolders
/addRoutes/addAppStoreRoutes.ts – adds all app store routes
/addRoutes/addTrainingLocatorRoutes/index.ts – calls all training locator route adder functions
/addRoutes/addTrainingLocatorRoutes/addTrainingManagerRoutes.ts – adds routes for the training manager subfeature
/addRoutes/addTrainingLocatorRoutes/addTrainingLauncherRoutes.ts – adds routes for the training launcher subfeature
/addRoutes/addTTMAPIRoutes/addMeetingSchedulerRoutes.ts – adds all teacher routes
```

### Standard Route Path Naming

We use REST API standards with additional constraints. When defining a route, always use the following rules to create your paths:

<Rule tall>
  All API endpoint paths must start with `/api`
</Rule>

Additionally, if only certain types of users can access the route, add another prefix for the type of user. Currently, we support `admin` and `ttm`:

<Rule tall>
  TTM API routes must start with `/api/ttm`, admin API routes must start with `/api/admin`
</Rule>

Why do we do this? `dce-reactkit` automatically applies security and authorization rules to endpoints based on the prefix in the path.

For the endpoint method, follow these rules:

- Get data = GET
- Create or add something = POST
- Multipurpose create *or* modify something = POST
- Single-purpose modify something = PUT
- Delete or remove something = DELETE

We use a folder-like pluralized path structure for endpoints. All placeholders must be prefixed by a description of the value.

<Rule tall>
  All placeholders must have a description prefix
</Rule>

For example, if you want to have a course id and a user id in the path, you must add prefixes:

```
Good:
/api/admin/courses/:courseId/users/:userId

Bad:
/api/admin/course/:courseId/user/:userId – not pluralized
/api/admin/courses/:courseId/:userId – userId has no prefix
/api/admin/:courseId/:userId – neither course nor user ids have prefixes
```

Add routes directly to the express app (for consistency across projects):

```ts
app.get(
  '/api/ttm/videos/:videoId/transcripts/:transcriptId',
  [handler here],
);
```

<Rule tall>
  Every endpoint must be documented using JSDoc
</Rule>

Add a JSDoc block above each endpoint, making sure to describe as `@param` statements any parameters that are _not_ included in the URL. For example, if we have an endpoint with two parameters in the url (`videoId` and `transcriptId`) and two parameters included in the request (`format` and `language`), the JSDoc would look like this:

```ts
/**
 * Get the transcript for a video
 * @author Gabe Abrams
 * @param {string} format the format of the transcript to return
 * @param {string} [language=en] the language to use for the transcript
 * @returns {string} full video transcript
 */
app.get(
  '/api/ttm/videos/:videoId/transcripts/:transcriptId',
  [handler here],
);
```

All API routes should use the `dce-reactkit` function for generating a route handler: `genRouteHandler`, which handles auth, session management, security and privacy, parameter parsing, automatic error handling, crash prevention, and so much more.

<Rule tall>
  API route handlers should use "genRouteHandler" from dce-reactkit if possible
</Rule>

The second argument of the express `app.get`, `app.post`, `app.put`, `app.delete`, or `app.all` function is a route handler. Use `genRouteHandler` to create such a handler.

`genRouteHandler` takes one argument, which is an object that must contain a `handler` function, may optionally contain a `paramTypes` map defining the types of parameters, and may optionally contain a flag that turns off the session check. Each property is defined below:

#### genRouteHandler: paramTypes

Define all params that the user can include in the request, including params in the URL and params in the request body. For example, if we have an endpoint with two parameters in the url (`videoId` and `transcriptId`) and two parameters included in the request (`format` and `language`), the `paramTypes` object should look like this:

```ts
app.get(
  '/api/ttm/videos/:videoId/transcripts/:transcriptId',
  genRouteHandler({
    paramTypes: {
      videoId: ParamType.Int,
      transcriptId: ParamType.Int,
      format: ParamType.String,
      language: ParamType.StringOptional,
    },
    ...
  }),
);
```

We use the `dce-reactkit` special param type enum called `ParamType`, which supports the following types:

```ts
Boolean – required boolean
BooleanOptional – optional boolean
Float –  required float
FloatOptional – optional float
Int – required int
IntOptional – optional int
JSON – required JSON object that has been stringified
JSONOptional – optional JSON object that has been stringified
String – required string
StringOptional – optional string
```

Note that it doesn't make sense to make a URL parameter be an optional param because they must always be included by construction.

#### genRouteHandler: handler function

The handler function is key because it handles the request. The handler function is an `async` function that is tasked with either returning the value that should be sent in the response to the client, or the handler function should throw an error which would also be sent to the client.

To send an error code to the client, use the `dce-reactkit` custom error called `ErrorWithCode`.

To send a response to the client, simply return the value that you want to send to the client. If you don't want to return anything, simply `return undefined;`.

Handler functions can take any of the following requirements, depending on what's required for the functionality you need to implement:

- `params`: a map containing all params defined in `paramTypes` plus a whole host of other automatically included user information. See the list below for more information
- `req`: the express request object
- `next`: a function to call to call the next express handler in the stack `next()`
- `send`: send a raw text response to the client `send(text: string, [status: number])`
- `renderErrorPage`: render a pretty html page that displays a server-side error (should not be used for API endpoints), takes an object that contain any of the following strings: `title`, `description`, `code`, `pageTitle`, as well as an optional `status` number
- `renderInfoPage`: render a pretty html page that displays server-side info (should not be used for API endpoints), takes an object that contains the following strings: `title`, `body`.

Additional params added to the `params` object in addition to params defined by `paramTypes`:

```ts
/**
 * Additional auto-included params:
 * @param {number} userId the user's CanvasId
 * @param {string} userFirstName the user's first name from Canvas
 * @param {string} userLastName the user's last name from Canvas
 * @param {string} userEmail the user's primary email from Canvas
 * @param {string} userAvatarURL a link to the user's profile image
 * @param {boolean} isLearner true if the user is a learner (student) in the Canvas course
 * @param {boolean} isTTM true if the user is a teacher, TA, or other teaching team member in the Canvas course
 * @param {boolean} isAdmin true if the user is a Canvas admin
 * @param {number} courseId the id of the Canvas course that the user launched from
 * @param {string} courseName the name of the Canvas course
 */
```

Further, all variables from the user's express session will be added to the params object if those variables are of type `string` or `boolean` or `number`.

Here's an example:

```ts
app.get(
  '/api/ttm/videos/:videoId/transcripts/:transcriptId',
  genRouteHandler({
    ...
    handler: async ({ params, next }) => {
      ...

      if (somethingBadHappened) {
        throw new ErrorWithCode(
          'Error message with full description here',
          'AX34', // Error code
        );
      }

      ...

      if (needToCallNextHandler) {
        return next();
      }

      ...

      // Process params and get transcript
      const {
        // Get request info
        videoId,
        transcriptId,
        format,
        language,
        // Get more info
        userId,
        userFirstName,
      } = params;

      // Get the transcript
      const transcript = getTranscript({
        videoId,
        transcriptId,
        format,
        language,
      });

      // Add user info to the transcript
      const transcriptWithUserInfo = augmentWithUserInfo(transcript, userId, userFirstName);

      // Send the response to the client
      return transcriptWithUserInfo;
    },
    ...
  }),
);
```

#### genRouteHandler: skipSessionCheck

If `skipSessionCheck` is true, `dce-reactkit` will skip its usual session checks (user must have launched via LTI and must have a valid session).

### Cross-Server Requests

To send requests between caccl-based servers that use dce-reactkit, you'll need to create cross-server endpoints on the receiving server and you'll need to use a special function to send the cross-server request.

#### Set Up Receiving Server

Create a `Scope.ts` enum for the project, in `/server/src/shared/types` that contains an enum that lists all cross-server API scopes.

For example:

```ts
/**
 * Cross-server API scopes
 * @author Your Name
 */
enum Scope {
  // Add a student to the course
  AddStudent = 'AddStudent',
  // Remove a student from the course
  RemoveStudent = 'RemoveStudent',
  // List all students in the course
  ListStudents = 'ListStudents',
}

export default Scope;
```

Next, create a cross-server credential collection that will hold the encoded credentials for servers that are allowed to make requests to the current server:

Update to `mongo.ts`:

```ts
// Import dce-reactkit
import {
  initCrossServerCredentialCollection,
  CrossServerCredential,
} from 'dce-reactkit';

...

// Cross server credentials
export const crossServerCredentialCollection = (
  initCrossServerCredentialCollection(Collection) as Collection<CrossServerCredential>
);
```

Finally, add `REACTKIT_CRED_ENCODING_SALT` environment variable to the receiving server. Fill it with random characters (no whitespace).

#### Set Up Sending Server

From any project that uses `dce-reactkit`, run the following command:

```bash
npm run gen-reactkit-cross-server-secret --description="Name of Sending Server" --key=short-name --host=receiving-server.dcex.harvard.edu --salt="receiving server credential encoding salt"
```

Where `--description` is a human-readable description of the server that will _send_ the requests, `--key` is a short unique key for the server that will _send_ the requests, and `--host` is the hostname for the server that will _receive_ the requests.

Example (requests will  be sent from Hello Harvard Prod to Immersive Classroom):

```bash
npm run gen-reactkit-cross-server-secret --description="Hello Harvard Prod" --key=hello-prod --host=immersive.dcex.harvard.edu
```

Once the credential has been generated, you'll see instructions on what to do next:

First, you'll need to _append_ a string to the `REACTKIT_CROSS_SERVER_CREDENTIALS` environment variable on the server that will _send_ the requests. To append, copy down the value into a text editor, make the changes, then paste the changes into the dev wizard (don't accidentally _replace_ the contents instead of appending). If the environment variable does not exist, add it. The format of the appended text should be: `|host:key:secret|`.

Second, you'll need to add the credential to the CrossServerCredential collection on the server that will _receive_ the requests. You'll be given a JSON object to insert into the database. Insert it, then append scopes to the `scopes` array for all of the scopes that the server should have access to.

A server may send requests to any number of other servers. This is why the `REACTKIT_CROSS_SERVER_CREDENTIALS` value can contain many credentials concatenated together: `|host1:key1:secret1||host2:key2:secret2|...`. Also, a server may both send cross-server requests and receive cross-server requests. In that case, you'll need to follow the instructions above in both directions.

#### How to Add a Cross-server Endpoint to the Receiving Server

Use the `genRouteHandler` function as with other endpoints, but add one important `crossServerScope` parameter, and remember that `params` will not automatically populate session-based info like `userFirstName` or `isAdmin`. Instead, authorization will be based on whether the server that makes the request has approval to use that scope and information like `userFirstName` _must_ be passed through with the request.

Example:

```ts
// Import shared types
import Scope from '../shared/types/Scope';

...

/**
 * Add a student to the course
 * @author Gabe Abrams
 * @param userFirstName the first name of the student to add to the course
 * @param userLastName the last name of the student to add to the course
 * @returns id of the new user
 */
app.post(
  '/api/cross-server/students',
  genRouteHandler({
    crossServerScope: Scope.AddStudent,
    paramTypes: {
      userFirstName: ParamType.String,
      userLastName: ParamType.String,
    },
    handler: async ({ params }) => {
      // Destructure params
      const {
        userFirstName,
        userLastName,
      } = params;

      // TODO: implement

      return userId;
    },
  }),
);
```

#### How to Send Cross-Server Requests

On the server that will _send_ the cross-server request, use the `visitEndpointOnAnotherServer` function that is exported from `dce-reactkit`:

```ts
// Import dce-reactkit
import { visitEndpointOnAnotherServer } from 'dce-reactkit';

...

const userId = await visitEndpointOnAnotherServer({
  method: 'POST',
  host: 'immersive.dcex.harvard.edu',
  path: '/api/cross-server/students',
  params: {
    userFirstName: 'Kino',
    userLastName: 'Greene',
  },
});
```

Remember that the `host` field _must_ match a credential in the sending server's `REACTKIT_CROSS_SERVER_CREDENTIALS` environment variable.

If the request is deemed inauthentic (credentials invalid, scope not added, etc.), you will get a `401` error.

## Mongo/DocDB

### When to Add a Database

We use databases intentionally. Thus, it's important to understand when to use a database, and when not to.

Comparing memory vs database storage:

| Factor | In Memory | In Database |
| --- | --- | --- |
| Speed | Quick to access | Slow to access |
| Permanence | Deleted upon instance restart | Stored indefinitely |
| Distribution | Data must only be relevant to one user during their session | Data can be shared across multiple sessions, across multiple users, or across multiple server instances |
| Migration | Automatically deleted when app is upgraded | Must be migrated when app is updated |
| Backups | Never backed up | Automatically backed up on regular intervals |
| Cleanup | If managed well, garbage collector takes care of this | Database will continue to grow if not managed carefully |

From this chart, it may seem like everything should go in a database, which is not necessarily true. Especially with user-specific information that is specific to the user's current session, it is extremely advantageous to store that information directly to the user's session (`req.session` via express) instead of storing items in the database. This minimizes the number of I/O lookups that have to occur on every server request.

Here are a few scenarios to consider:

- A piece of user-specific data needs to be quickly accessible by the user and is not needed after the user's session expires. We'll put this in the user's session because it'll be fast to access and will be automatically cleaned up after the user ends their session.
- A piece of data needs to be extremely quick to access because it must be used by server-side algorithms, but this data is also required outside the user's session. We'll store this in a database but cache it in memory, so we get the best of both worlds...but we'll be careful to think through the impact of caching and potentially out-of-date data.
- A piece of data needs to be stored indefinitely and we'll continue to add to it over time. We'll store this in the database because that'll ensure the data is persistent and backed up.
- A piece of data needs to be accessed by multiple users. We'll store this in the database.
- A piece of data is very large. We'll store this in the database because we simply cannot leave it in memory without risk of running out of memory once multiple users use this feature.

Once you've decided what data should be in the database and what data should not be in the database, you can continue to the following section to integrate with mongo/docdb.

### Integrating with Mongo/DocDB

Because our projects are designed to go back and forth seamlessly between MongoDB and Amazon DocDB, we use a library called `dce-mango` which provides the seamless interface that ensures operations are successfully executed and queries are consistently executed independent of the database type.

We _only_ use non-relational database because these types of databases work extremely fluently with the rest of our javascript-based stack. In particular, mongo and docdb allow us to store javascript objects directly to the database, with a couple constraints. Thus, wherever possible, try to create javascript objects that adhere to the following constraints so we can move those objects to a database if needed:

1. No circular objects (an object cannot contain cycles)
1. Only simple data in objects (strings, numbers, booleans, arrays, objects) instead of complex objects (classes, interfaces, class instances, etc.)

If integrating with a database, create a shared helper called `/server/src/shared/helpers/mongo.ts` that contains all of the code defining each collection in the database. For each collection, define the typescript type for an entry that will be stored in said collection and put that type in `/server/src/shared/types/stored`.

I'll explain `dce-mango` through example. It is important that you follow the structure of this template. This includes formatting and headings.

First, import dependencies and the shared types associated with each collection:

```ts
// Import db
import { initMango, Collection } from 'dce-mango';

// Import shared types
import ActivitySubmission from '../types/stored/ActivitySubmission';
import ShareoutPost from '../types/stored/ShareoutPost';
import LiveMessage from '../types/stored/LiveMessage';
import LiveViewer from '../types/stored/LiveViewer';
import Migration from '../types/stored/Migration';
import WatchTrace from '../types/stored/WatchTrace';
```

Then, initialize `dce-mango`, giving it a schemaVersion (start at 1 and increment every time you make changes to this file):

```ts
/*------------------------------------------------------------------------*/
/* ----------------------------- Initialize ----------------------------- */
/*------------------------------------------------------------------------*/

initMango({
  schemaVersion: 12,
  dbName: 'immersive-player-store',
});
```

Finally, define and export each collection. Define each collection by creating a new instance of the `Collection` class. Add in the type of the entries in the collection, using the associated type that you imported: `new Collection<MyEntryType>(...)`. The `Collection` constructor takes two arguments: the first argument is the name of the collection, which should be named the same as the entry type: `new Collection<MyEntryType>('MyEntryType', ...`. The second argument defines indexes, and takes the following parameters:

`uniqueIndexKey` – a string that represents the key for the property to use as a unique index. If defined, each entry must have a unique value for this property. When inserting into a collection with a unique index, if an existing entry has a matching value for this key, the existing entry will be overwritten.

`indexKeys` – a list of secondary non-unique keys that should be used to create other indexes. Here, simply provide a list of keys that will commonly be used for searching and querying. Don't get too carried away: for every key you add to this list, the database must maintain an index and must update the index when entries are added/modified/removed.

`expireAfterSeconds` – a number of seconds that represents the minimum lifespan of entries in this collection. If not included, entries will not be automatically deleted. There is no guarantee that entries will be deleted immediately after they expire. Instead, regular cleanups occur and expired entries are deleted. 

<Rule tall>
  If entries have an id, always simply name it "id"
</Rule>

Remember to export each collection, as you see in the example:

```ts
/*------------------------------------------------------------------------*/
/* ----------------------------- Collections ---------------------------- */
/*------------------------------------------------------------------------*/

// Activity Submissions
export const activitySubmissionCollection = new Collection<ActivitySubmission>(
  'ActivitySubmission',
  {
    uniqueIndexKey: 'id',
    indexKeys: [
      'courseId',
      'videoId',
      'isLearner',
      'isAdmin',
    ],
  },
);

// Shareout Post
export const shareoutPostCollection = new Collection<ShareoutPost>(
  'ShareoutPost',
  {
    uniqueIndexKey: 'id',
    indexKeys: [
      'courseId',
      'videoId',
      'isLearner',
      'isAdmin',
    ],
  },
);

// Migrations
export const migrationCollection = new Collection<Migration>(
  'Migration',
  {
    uniqueIndexKey: 'id',
    indexKeys: [
      'oldVideoId',
      'newVideoId',
      'migrationStatus',
    ],
  },
);

// Live messages
export const liveMessageCollection = new Collection<LiveMessage>(
  'LiveMessage',
  {
    uniqueIndexKey: 'id',
    indexKeys: [
      'courseId',
      'videoId',
      'timestamp',
      'isLearner',
      'isAdmin',
    ],
  },
);

// Live viewers
export const liveViewerCollection = new Collection<LiveViewer>(
  'LiveViewer',
  {
    uniqueIndexKey: 'id',
    indexKeys: [
      'courseId',
      'videoId',
      'timestamp',
      'isLearner',
      'isAdmin',
    ],
    expireAfterSeconds: 90,
  },
);

// Watch traces
export const watchTraceCollection = new Collection<WatchTrace>(
  'WatchTrace',
  {
    uniqueIndexKey: 'id',
    indexKeys: [
      'courseId',
      'videoId',
      'isLearner',
      'isAdmin',
    ],
  },
);
```

### Local Development

Once deployed to AWS, `dce-mango` will automatically connect to an auto-provisioned database, as long as the app is configured to have a dabase.

However, while developing your app and testing in a local dev environment, you'll need to have a test database. Ultimately, you'll need to "MONGO_URL" which you'll put in your `/server/.env` file:

```bash
MONGO_URL=mongodb://some/mongo-database-url-here
```

There are two recommended ways of provisioning your test database:

#### Get a free cloud-based mongodb instance

This option is best if you want a simple, flexible database that has a UI, and is easy to share across multiple systems. Gabe recommends this for all EdTech Software Engineers that report to them because it'll be easier for Gabe to jump in and run your code with your current database state.

1. Visit `cloud.mongodb.com`
1. Log in with your `g.harvard.edu` email
1. Create a new project
1. Get a free "Shared" tier database and place it in AWS N. Virginia
1. Create a Username and Password for your app
1. Allow access from anywhere by adding an IP to your IP Access List: IP Address = 0.0.0.0/0 and Description = Anywhere
1. Find the cluster (probably called "Cluster0") and click "Connect"
1. Click "Connect your application"
1. Copy down the "connection string" and replace "<username>" with the username, replace "<password>" with the password
1. Paste the url into your `/server/.env` file as "MONGO_URL"

#### Create a local mongodb cluster

This option is best if you're a pro and want complete control over your cluster. Also consider this option if you're storing sensitive data.

Find a tutorial online on how to provision a local mongodb cluster. Create a database within that cluster. For the sake of this example, let's call the database "my-app". Then, a url to your local cluster in your `/server/.env` file. It might look something like this:

```bash
MONGO_URL=mongodb://0.0.0.0:27017/my-app
```

### Accessing and Modifying Data

Now that you've integrated with the database, you'll need to create, edit, delete, and query collections in the database. We'll walk through some asynchronous operations you can perform. Full documentation can be found via the typescript JSDoc embedded in the `dce-mango` library. We'll show a few examples.

In each example, we will pretend that we're integrating with a "Users" collection that contains objects that look like this:

```ts
// Type (saved to /server/src/shared/types/stored/User.ts)
type User = {
  // The user's unique id
  id: string,
  // The user's first name
  userFirstName: string,
  // The user's last name
  userLastName: string,
  // The user's email
  userEmail: string,
  // The user's current age
  age: number,
  // List of user's current addresses
  addresses: {
    type: ('home' | 'work' | 'other'),
    streetAddress: number,
    streetName: string,
    streetSuffix: ('st' | 'dr' | 'av' | 'pl' | 'rd'),
    cityName: string,
    zipCode: number,
    country: string,
  }[],
};

// Example user:
const user: User = {
  id: '1022',
  userFirstName: 'Gabe',
  userLastName: 'Abrams',
  userEmail: 'gabe_abrams@harvard.edu',
  age: 10,
  addresses: [
    {
      type: 'home',
      streetAddress: 13,
      streetName: 'Axis',
      streetSuffix: 'dr',
      cityName: 'Cambridge',
      zipCode: 02155,
      country: 'US',
    },
  ],
};
```

Before continuing, we need to describe a "query" object. This is used for searching the collection. You can think of a query as a partial object that is compared with every item in the collection. Any items that match the query will be returned/modified/deleted/etc. depending on the current operation. I'll explain with a few examples:

```ts
// Query that matches all users with a certain first name:
const query = {
  userFirstName: 'Kino',
};
```

```ts
// Query that matches all users with a certain age:
const query = {
  age: 14,
};
```

We support complex queries. You can google these, but generally, the way you use these is by putting an object in place of a value. Here are a few examples:

```ts
// Query that matches all users who are younger than 18
const query = {
  age: { $lt: 18 },
};
```

```ts
// Query that matches all users who are 10 or 20
const query = {
  age: { $in: [10, 20] },
};
```

To interact with the collection, simply import it at the top of your file:

```ts
import { userCollection } from '../../shared/helpers/mongo';
```

#### Find - Query/Search a Collection

Each find command searches a collection for _all_ matches to a query. If the returned array is empty, there are no matches to the query.

```ts
// Find all teenagers
const matches = await userCollection.find({
  age: { $gte: 13, $lt: 20 },
});
```

#### Increment - increment an integer propery of an object

To use this function, the collection must be uniquely indexed by a string "id" field. Simply pass in the id of the object and the property to increment.

```ts
// Increment a user's age by 1 year
await userCollection.increment('1022', 'age');
```

#### Update Prop Values - add or update values in an entry in the collection

For this to work, the object must already exist in the collection. Instead of overwriting the object, you can use this operation to perform a partial update, only modifying certain parts of the object. Pass in a query that will be used to find the object to update, then pass in an object containing the updates to apply.

```ts
// Set the addresses of all users with the last name "Abrams"
await userCollection.updatePropValues(
  {
    userLastName: 'Abrams',
  },
  {
    addresses: [
      {
        type: 'home',
        streetAddress: 13,
        streetName: 'Axis',
        streetSuffix: 'dr',
        cityName: 'Cambridge',
        zipCode: 02155,
        country: 'US',
      },
    ],
  },
);
```

#### Push - add an object to an array in an object

If there's an existing array in an object, you can use this function to add one more item to that array. To use this function, the collection must be uniquely indexed by a string "id" field. Simply pass in the id of the object, the property that points to the array, and the object to insert.

```ts
// Add an address to a specific user's addresses array
await userCollection.push(
  '1022',
  'addresses',
  {
    type: 'home',
    streetAddress: 13,
    streetName: 'Axis',
    streetSuffix: 'dr',
    cityName: 'Cambridge',
    zipCode: 02155,
    country: 'US',
  },
);
```

#### Filter Out - modify an array by filtering out all objects that don't match a comparison

If there's an existing array in an object, you can use this function to filter items out of an array. To use this function, the collection must be uniquely indexed by a string "id" field. Pass an object that contains the id, arrayProp, and a compareProp (the property inside of each array object to compare) and the compareValue (the value to filter out).

```ts
// Remove all US addresses from a user's addresses array
await userCollection.filterOut({
  id: '1022',
  arrayProp: 'addresses',
  compareProp: 'country',
  compareValue: 'US',
});
```

#### Insert - add an item to the collection

This one's simple: it'll insert an item into the collection. If the collection is uniquely indexed and an object already exists, the insert will be converted to an "upsert" which replaces the existing object automatically.

```ts
// Add a user to the db
await userCollection.insert({
  id: '1022',
  userFirstName: 'Gabe',
  userLastName: 'Abrams',
  userEmail: 'gabe_abrams@harvard.edu',
  age: 10,
  addresses: [
    {
      type: 'home',
      streetAddress: 13,
      streetName: 'Axis',
      streetSuffix: 'dr',
      cityName: 'Cambridge',
      zipCode: 02155,
      country: 'US',
    },
  ],
});
```

#### Delete - remove an item from the collection

This one's simple: it'll delete the first object that matches the query.

```ts
// Delete a user
await userCollection.delete({
  id: '1022',
});
```

# React Component Unit Tests

## Guiding Principles

We aim for high test coverage, but time is always limited, so we write tests in order of priority.

Here's our order of priority:

1. Main interactive components + key features
1. Edge cases
1. Features that have a higher chance of breaking later on
1. Everything else

There are some things that we do not test:

1. Implementation details: these will change
1. Specific look and feel (colors, etc.): these will change with themes

When writing tests, first write each assertion with the opposite type of test (if a button should be enabled, test if it's disabled) and make sure the test will fail. Writing tests that succeed is easy. Writing tests that fail when appropriate is very hard.

One way to identify all the tests that you need to write is to start with each prop and state variable:

1. How does each prop or state variable impact the functionality/rendering/interactivity of the component?
1. What kinds of special cases might arise for props/state variables? For example, negative numbers, empty strings, empty arrays, etc.
1. How should the props/state react to errors?
1. How does the component render, what content should it create based on each type of prop passed in?

## Create a Test File

Name your test the same as your component with a `.test.tsx` filename:

<Rule>
  Tests use same name as component with .test.tsx extension
</Rule>

```ts
MyComponent.tsx // Component
MyComponent.test.tsx // Test
```

## Write a Test

First, import our testing library and the component to test:

```ts
// Import testing lib
import Raixa from 'raixa';

// Import component to test
import MyComponent from './MyComponent';
```

We use a custom-built wrapper for [React Testing Library (RTL)](https://testing-library.com/docs/react-testing-library/intro/) that we call [Raixa](https://bit.ly/dce-raixa). Although we do not directly interact with RTL, for your own professional development, we recommend that you take some time to learn it. But for our purposes, if a testing functionality is not available in [Raixa](https://bit.ly/dce-raixa), we will add the functionality to [Raixa](https://bit.ly/dce-raixa) instead of using RTL.

Create a test:

```ts
test(
  'description of test',
  async () => {
    ...
  },
);
```

Describe your test. Here are some examples for an email form component:

- "Updates as user types into subject field"
- "Validates recipient address properly"
- "Sends the correct request to the server when user clicks 'send'"

Inside the test, render the component of interest, including appropriate props (note this is rendered to a hidden headless browser, there is no way to see this):

```ts
Raixa.render(
  <MyComponent
    prop1={value}
    prop2="value"
  />,
);
```

Once you've rendered your component, use [Raixa functions](https://bit.ly/dce-raixa) to test the component.

```ts
// Click the "start email button"
Raixa.click('.MyComponent-start-email-button');

// Type into the subject field
Raixa.typeInto('#MyComponent-email-subject-field', 'Test Email Subject');

// Test to make sure that the submit button is available
Raixa.assertExists('.MyComponent-submit-button');
```

If your interactable elements do not have classNames or ids, add them! Remember that if your component will ever be used in more than one place at once, use classNames. Otherwise, ids are fine.

If a test will take longer to execute, extend its timeout with a third argument:

```ts
test(
  'description of test',
  async () => {
    ...
  },
  10000, // Timeout in ms
});
```

If your component sends requests to the server, then you'll need to first stub requests (do this before `Raixa.render`). For each request that your component will send, stub that request with `stubServerEndpoint` from `dce-reactkit`:

```ts
import { stubServerEndpoint } from 'dce-reactkit';

...

test(
  'description of test',
  async () => {
    // Stub email form submission endpoint
    stubServerEndpoint({
      method: 'POST',
      path: '/api/ttm/threads/102398/emails',
      body: true,
    });

    // Render email form
    Raixa.render(...
  },
);
```

To stub a successful response from the server, use:

```ts
stubServerEndpoint({
  method: <http method that the component will use>,
  path: <path of the endpoint the component will send to>,
  body: <fake response to simulate coming back from the server>,
});
```

To stub a failed response from the server, use:

```ts
stubServerEndpoint({
  method: <http method that the component will use>,
  path: <path of the endpoint the component will send to>,
  errorMessage: <string error message that would come from the server>,
  errorCode: <string error code that would come from the server>,
});
```

Example of a full test:

```tsx
// Import testing lib
import Raixa from 'raixa';

// Import component to test
import EmailForm from './EmailForm';

test(
  'Shows notice when recipient email is invalid',
  async () => {
    // Render the component
    Raixa.render(
      <EmailForm
        sender="test@harvard.edu"
        onSent={() => {}}
      />,
    );

    // Type an invalid recipient
    Raixa.typeInfo('.EmailForm-recipient-email-input-field', 'invalid.email@@.com');

    // Make sure validation text shows up
    Raixa.assertExists('.EmailForm-recipient-email-invalid-notice');
  },
);

test(
  'Allows email send when recipient email is valid',
  async () => {
    // Stub email form submission endpoint with a successful response
    stubServerEndpoint({
      method: 'POST',
      path: '/api/ttm/threads/102398/emails',
      body: true,
    });

    // Render the component
    Raixa.render(
      <EmailForm
        sender="test@harvard.edu"
        onSent={() => {}}
      />,
    );

    // Type a valid recipient
    Raixa.typeInfo('.EmailForm-recipient-email-input-field', 'valid.email@gmail.com');

    // Make sure validation text is not visible
    Raixa.assertAbsent('.EmailForm-recipient-email-invalid-notice');

    // Click the "send" button
    Raixa.click('.EmailForm-send-button');

    // Make sure a success message shows up after some time
    Raixa.waitForElementPresent('.EmailForm-send-successful-message');
  },
);

test(
  'Shows an error message when the server fails',
  async () => {
    // Stub email form submission endpoint with a successful response
    stubServerEndpoint({
      method: 'POST',
      path: '/api/ttm/threads/102398/emails',
      errorMessage: 'The message could not be sent',
      errorCode: 'EM29',
    });

    // Render the component
    Raixa.render(
      <EmailForm
        sender="test@harvard.edu"
        onSent={() => {}}
      />,
    );

    // Type a valid recipient
    Raixa.typeInfo('.EmailForm-recipient-email-input-field', 'valid.email@gmail.com');

    // Make sure validation text is not visible
    Raixa.assertAbsent('.EmailForm-recipient-email-invalid-notice');

    // Click the "send" button
    Raixa.click('.EmailForm-send-button');

    // Make sure the server's error is visible
    Raixa.waitForElementPresent('.EmailForm-error-occurred');
  },
);
```

You can stub multiple requests and Raixa will automatically know which to stub based on the method and path. If your component sends multiple requests to the _same_ method and path combo, then intersperse `stubServerEndpoint` throughout your test code, only stubbing right before your component sends the request.

## Running Tests

Use `npm run test:client` to start the jest test runner.

If `test:client` is not set up yet, here's how you add that script:

1. In the top-level `package.json` file, add a new script: `"test:client": "cd client && npm run test"`
2. Then, in `client/package.json`, modify the "test" script to include the --runInBand flag: `"test": "react-scripts test --runInBand"`

# Helper Unit Tests

## Guiding Principles

For each helper function that we test, we aim for high test coverage, but time is always limited, so we write tests in order of priority.

Here's our order of priority:

1. Usual inputs and outputs or side-effects
1. Edge cases (unusual inputs or environment variables, for example)
1. Features that have a higher chance of breaking later on
1. Everything else

There are some things that we do not test:

1. Implementation details: these will change
1. Dependencies and libs: these are unit tests, so we do not focus on dependencies and libs

## Create a Test File

Name your test the same as your component with a `.test.ts` filename:

<Rule>
  Tests use same name as the helper with .test.ts extension
</Rule>

```ts
myHelper.ts // Helper
myHelper.test.ts // Test
```

## Write a Test

First, import the helper that you're going to test:

```ts
// Import helper to test
import myHelper from './myHelper';
```

All of our helper unit tests are built using vanilla [Jest](https://jestjs.io/docs/getting-started) tests. We create our list of tests and each one becomes a call to the `test` function:

Create a test:

```ts
test(
  'description of test',
  async () => {
    ...
  },
);
```

Describe your test. Here are some examples for a helper function that divides two numbers:

- "Divides two positive, nonzero numbers"
- "Throws an error when one or both of the arguments are not numbers"
- "Throws an error if the denominator is zero"
- etc.

If a test will take longer to execute, extend its timeout with a third argument:

```ts
test(
  'description of test',
  async () => {
    ...
  },
  10000, // Timeout in ms
});
```

## Running Tests

Simply use `npm test` to run tests. If that doesn't work, ask Gabe to help set your project up with jest test running.

# Automated UI Testing

We use Katalon for all our end-to-end automated cross browser testing.

## Set Up Katalon

### 1. Install Katalon:

Visit [Katalon](https://katalon.com/download-studio-free), create an account, and then install the free version of the tool.

### 2. Modify Katalon Preferences:

In Katalon's preferences panel, make the following changes:

`Katalon > Git > Enable Git Integration` – Turn this off (uncheck the box)

`Katalon > Test Case > Default Open View` – Set to "Script View"

`General > Editors > Text Editors > Displayed Tab Width` – Set this to "2"

Also, edit your default text editor profile:

`General > Editors > Text Editors > New...`

Create a new profile called "DCE Automated Testing" and click "OK"

Under the "Indentation" section, change "Tab policy" to "Spaces Only" and change both "Indentation size" and "Tab size" to "2"

Click "Apply", "OK", make sure "DCE Automated Testing" is your active profile, then click "Apply" and then "Apply and Close"

## Keep Katalon Up-to-date

Regularly update your web drivers:

1. Launch Katalon
1. Under `Tools > Update WebDrivers`, one by one, click each browser and update it

## Project and File Management

All of our tests will be organized in a GitHub repo that's separate from the code. Ask your project manager about cloning that repo.

Our test case files follow a strict folder structure: there should only be one top-level folder called "All Tests" inside of the "Test Cases" folder. Then, inside "All Tests", we create one folder for each feature of the project. Name your test cases in a descriptive manner. Example: "User can log in after password is reset"

## Write a Test

Our tests are written in the `Groovy` language, which looks like `Java`.

Check out the [Kaixa Docs](https://harvard-edtech.github.io/create-kaixa/) for guides on how to write end-to-end tests, but it should feel just like writing tests with [Raixa](https://bit.ly/dce-raixa).

### Where to Find Docs

For general commands (clicking, typing, waiting, etc.) use the [Kaixa Docs](https://harvard-edtech.github.io/create-kaixa/). For project-specific docs, open Katalon, in the file browser go to "Keywords" and find the keyword file that is _not_ `Kaixa.groovy`. For example, the Immersive Classroom keyword is called `IC.groovy` and the Gather keyword is called `Gather.groovy`. Within that file, there are many custom functions that represent automation tasks that we expect to perform quite frequently for that project. Each function contains inline JSDoc that outlines the functions use and each argument you might pass in.

### How to Choose CSS Selectors

When clicking, typing, asserting, waiting for, or doing any other task that requires specifying an element on the page, you'll need a CSS selector.

Open the app in your browser and poke around until you see the element that you want to target, then right click it and select "Inspect". In your element inspector, you'll see the code for the html. The element may have an `id` or `class`. You're welcome to use either. The main mission is to select something that's unique and descriptive. It _must_ start with the name of the component (e.g. `BookmarkDashboard-something-else`) and cannot be one of the all lowercase formatting classes (e.g. `text-center` or `pb-2`).

If there isn't an obvious class name or id that you can use, _do not_ get creative. Instead, we'll go into the code of the app and add unique class names and ids.

## Running a Test

1. Make sure the app you're testing is running and ready to be tested
1. Open the test case
1. Choose a profile
1. Next to the play button, click the dropdown and choose a browser

# Commonly Used Dependencies

If you're looking for a module that does one of the operations below, use these libs. Thus, when bundling, we can save space by using common libs.

`fast-clone` – for fast deep clones

`papaparse` – for CSV parsing and generation

`object-hash` – for hashing objects

<Rule tall>
  Use dependencies listed above instead of seeking out alternatives
</Rule>

# Creating React Projects

In almost every case, let Gabe create React projects. That said, it's good to know the process:

## Create a new npm project:

1. Create a git repo and clone it
1. Initialize the project: `npm init`
1. Add a `.gitignore`
1. Initialize caccl app using `npm init caccl@latest`
1. Add eslint rules in each sub-project separately (client and server, for example): `npm init dce-eslint@latest`, remove react lines in `/server/.eslintrc.js`
1. Add `private: true` flag in `package.json`

## Set up the server:

1. Create a `server/` folder
1. Inside the `server/` folder, initialize the project: `npm init`
1. Add a `.gitignore`
1. Add `private: true` flag in `package.json`
1. If you have custom server env vars, add `**/.env` to your gitignore, install `dotenv` on the server as a dev dependency, add `import 'dotenv/config';` to the top of your server index, and add a `/server/.env` file where environment variables are listed one per line: `NAME=value`

## Set up the client

1. From the top-level directory, initialize react: `npx create-react-app --template typescript client`
1. Install bootstrap: `npm i --save bootstrap`
1. Import bootstrap in `index.tsx`:
    ```ts
    // Import bootstrap stylesheet
    import 'bootstrap/dist/css/bootstrap.min.css';
    import 'bootstrap/dist/js/bootstrap.min';
    ```
1. Install FontAwesome libs: `npm i --save @fortawesome/fontawesome-svg-core @fortawesome/free-regular-svg-icons @fortawesome/free-solid-svg-icons @fortawesome/react-fontawesome`
1. Install SCSS with `npm i --save-dev sass`
1. Remove eslint rules from `package.json` (they're included via `dce-eslint`)

Add a script for copying types from the server to the client:

This script copies types from the server (`/server/src/shared/types`) and puts them on the client (`/client/src/shared/types`). This is extremely useful if types are shared between the server and the client, or if a database is used.

```json
  "scripts": {
		"copy-server-types": "rm -rf ./client/src/shared/types/from-server; cp -r ./server/src/shared/types ./client/src/shared/types/from-server"
	},
```

## Set up the project for deployment:

Install `dce-dev-wizard` into the project: `npm i --save-dev dce-dev-wizard`.

Add a `dceConfig.json` file with deployment information. The `name` is a human-readable deployment name, `app` is the aws name of the deployment, and `profile` is the aws profile. Example:

```json
{
  "deployments": [
    {
      "name": "Stage",
      "app": "my-app-stage",
      "profile": "stage"
    },
    {
      "name": "Prod",
      "app": "my-app-prod",
      "profile": "prod"
    }
  ]
}
```

## Add a `dev-wizard` script that is used for managing and performing deployment:

```json
  "scripts": {
		"dev-wizard": "./node_modules/.bin/dce-dev-wizard"
  }
```

## Adding Typescript Support to a Project

Once you've created the project, you need to separately add typescript support.

First, move all code into a `src/` folder and make sure your project has no top-level `lib/` folder.

Add typescript to the project:

1. Install typescript with `npm i --save-dev typescript`
1. In `package.json`, update `main` to `./lib/index.js`
1. In `package.json`, update `types` to `./lib/index.d.ts`
1. Add a build script: `tsc --project ./tsconfig.json`

Add a `tsconfig.json` file to the top-level directory of the project:

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "esModuleInterop": true,
    "noImplicitAny": true,
    "noEmitOnError": true,
    "removeComments": false,
    "declaration": true,
    "sourceMap": true,
    "target": "es5",
    "lib": ["DOM", "ES2015"],
    "outDir": "./lib"
  },
  "include": [
    "./src"
  ],
  "ts-node": {
    "files": true
  }
}
```

You can customize the `tsconfig.json`. This config is designed to target es5 while supporting modern standards.

If your project has non-typescript files that are required in the project, update your build script:

1. Install new dependencies `npm i --save-dev rimraf copyfiles`
1. Update your build script: `rimraf lib/ && tsc --project ./tsconfig.json && copyfiles -u 1 src/**/*.ejs src/**/*.jpg lib/`

# Creating Component Libraries

Component libraries are npm modules that contain React components that are intended for reuse. If you find yourself reusing a component across multiple projects, you might want to consider putting that component into a shared component library.

Creating a component library can be really complex and finnicky, so we've simplified our process and made some compromises. Please follow this guide, including all simplifications and compromises.

When naming your component library, include `dce` or `harvard` in the project name _unless_ it is a project that will be used across multiple universities. We don't want to be part of the npm clutter problem, so don't reserve generic names for our internal libs if you don't need to. For example, if we're creating a support library that is used for managing dates and times with respect to Cambridge, MA, don't snag the `date-manager` project name. Instead, call your library `dce-date-manager` or something.

## 1. Prepare Your Components

Before components can be added to a component library, we require that style be translated into vanilla css (not scss) and copied inline into a new section at the top of the component `.tsx` file:

```tsx
/*----------------------------------------*/
/* ---------------- Style --------------- */
/*----------------------------------------*/

const style = `
  .MyComponent-container {
    ...
  }
`;
```

Then, in the final `return` in the render function, add the style inline:

```tsx
  return (
    <div className="MyComponent-container">
      {/* Inline Style */}
      <style>
        {style}
      </style>

      ...
    </div>
  );
```

## 2. Create a Component Package

Now, we'll create an npm package that we will be publishing as open source to npm. For consistency and maintenance, Gabe will be the one who publishes and maintains these packages on npm.

First, create a new repo on GitHub, set it up using the `Node` gitignore template, write a short description of the project (and copy that description to the clipboard), and add the `MIT` license. Then, clone that repo to your computer.

Next, initialize the npm project using `npm init`. When prompted for a description, paste the description from your clipboard. When prompted for an author, use `Gabe Abrams <gabeabrams@gmail.com>`, and when prompted for a license, use "MIT".

Also, add eslint rules to the project:

```bash
npm init dce-eslint@latest
```

## 3. Set Up Build Process

Install dev dependencies:

`npm i --save-dev rollup rollup-plugin-dts rollup-plugin-sourcemaps typescript @rollup/plugin-commonjs @rollup/plugin-json @rollup/plugin-node-resolve @rollup/plugin-typescript @types/react`

Install peer dependencies, modifying for the proper versions:

```json
  // Add to package.json:
  "peerDependencies": {
    "@fortawesome/free-regular-svg-icons": "^6.x.x",
    "@fortawesome/free-solid-svg-icons": "^6.x.x",
    "@fortawesome/react-fontawesome": "^0.x.x",
    "bootstrap": "^5.x.x",
    "react": "^x.x.x"
  },
```

Then run `npm i` to install the appropriate dependencies.

Add a build script to your `package.json`:

```json
  "scripts": {
    ...
    "build": "rm -rf dist && rollup -c"
  },
```

Modify/add the following lines to your `package.json`:

```json
  "main": "dist/cjs/index.js",
  "module": "dist/esm/index.js",
  "types": "dist/index.d.ts",
```

Add a `rollup.config.js` file to the root project directory:

```js
import resolve from '@rollup/plugin-node-resolve';
import commonjs from '@rollup/plugin-commonjs';
import typescript from '@rollup/plugin-typescript';
import dts from 'rollup-plugin-dts';
import sourcemaps from 'rollup-plugin-sourcemaps';

const packageJson = require('./package.json');

export default [
  {
    input: 'src/index.ts',
    output: [
      {
        file: packageJson.main,
        format: 'cjs',
        sourcemap: true,
      },
      {
        file: packageJson.module,
        format: 'esm',
        sourcemap: true,
      },
    ],
    plugins: [
      resolve(),
      commonjs(),
      typescript({ tsconfig: './tsconfig.json' }),
      sourcemaps(),
    ],
    external: [
      ...Object.keys(packageJson.dependencies || {}),
      ...Object.keys(packageJson.peerDependencies || {}),
    ],
  },
  {
    input: 'dist/esm/index.d.ts',
    output: [{ file: 'dist/index.d.ts', format: 'esm' }],
    plugins: [dts()],
    external: [
      ...Object.keys(packageJson.dependencies || {}),
      ...Object.keys(packageJson.peerDependencies || {}),
    ],
  },
];
```

Add a `tsconfig.json` file to the root project directory:

```json
{
  "compilerOptions": {
    "target": "es2016",
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "strict": true,
    "skipLibCheck": true,

    "jsx": "react",
    "module": "ESNext",
    "declaration": true,
    "declarationDir": "types",
    "sourceMap": true,
    "outDir": "dist",
    "moduleResolution": "node",
    "allowSyntheticDefaultImports": true,
    "emitDeclarationOnly": true,
    "rootDir": "src"
  },

  "include": [
    "./src/**/*"
  ]
}
```

## 4. Add Components

Create a `/src` folder and a `/src/index.ts` file that will serve as the entrypoint.

Add all components to a `/src/components` folder and follow all other normal rules for file and folder structure (naming conventions, shared folders, etc.).

In the `/src/index.ts` file, import all components, helpers, types, etc. that you want to be available to users of your package and then export them in one object:

```ts
// Components
import MyFirstComponent from './components/MyFirstComponent';
import MySecondComponent from './components/MyFirstComponent';

// Helpers
import myHelperFunction from './helpers/myHelperFunction';

// Types
import MyFirstType from './shared/types/MyFirstType';
import MySecondType from './shared/types/MySecondType';

// Export
export {
  // Components
  MyFirstComponent,
  MySecondComponent
  // Helpers
  myHelperFunction,
  // Types
  MyFirstType,
  MySecondType,
};
```

## 5. Test

One of the easiest ways to test is to create a test React app, copy your components into the app and try to use them. This is a good place to start, but won't get you all the way there, so check out `npm link` functionality and ask Gabe for specific testing strategies that will work for you.

## 6. Build and Publish

Build your component lib by running `npm run build`. If no errors occur, check the `/dist` folder for built contents.

Commit and push your code and ask Gabe to publish the library.

<Rule tall>
  Only Gabe publishes packages to npm
</Rule>

# Creating Support Libraries

Support libraries contain helpful, reusable code that is used across multiple projects. These support libraries cannot contain React code. If they do, consider a Component Library (see the previous section).

Creating a support library is extremely complicated and complex, so we've created this guide and need you to stick to it. What might seem to be compromises are probably careful decisions that were made to improve the build process or robustness of the library in other ways.

When naming your support library, include `dce` or `harvard` in the project name _unless_ it is a project that will be used across multiple universities. We don't want to be part of the npm clutter problem, so don't reserve generic names for our internal libs if you don't need to. For example, if we're creating a support library that is used for managing dates and times with respect to Cambridge, MA, don't snag the `date-manager` project name. Instead, call your library `dce-date-manager` or something.

## 1. Prepare Your Code

Any code that you want to place into a shared library must be 100% typescript files (`.ts`). We do not currently support assets or other types of files.

## 2. Create a Support Package

Now, we'll create an npm package that we will be publishing as open source to npm. For consistency and maintenance, Gabe will be the one who publishes and maintains these packages on npm.

First, create a new repo on GitHub, set it up using the `Node` gitignore template, write a short description of the project (and copy that description to the clipboard), and add the `MIT` license. Then, clone that repo to your computer.

Next, initialize the npm project using `npm init`. When prompted for a description, paste the description from your clipboard. When prompted for an author, use `Gabe Abrams <gabeabrams@gmail.com>`, and when prompted for a license, use "MIT".

Also, add eslint rules to the project:

```bash
npm init dce-eslint@latest
```

## 3. Set Up Build Process

Install dev dependencies:

`npm i --save-dev @types/node typescript`

Add a build script to your `package.json`:

```json
  "scripts": {
    ...
    "build": "tsc --project ./tsconfig.json"
  },
```

Add/modify the following `package.json` lines:

```json
  "main": "./lib/index.js",
  "types": "./lib/index.d.ts",
```

Add the following `tsconfig.json` file to the top-level of your project:

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "esModuleInterop": true,
    "noImplicitAny": true,
    "noEmitOnError": true,
    "removeComments": false,
    "declaration": true,
    "sourceMap": true,
    "target": "es5",
    "outDir": "./lib"
  },
  "include": [
    "./src"
  ],
  "ts-node": {
    "files": true
  }
}
```

## 4. Add Code

Add all code to a `/src` folder and follow all other normal rules for file and folder structure (naming conventions, shared folders, etc.).

In the `/src/index.ts` file, import all functions, types, etc. that you want to be available to users of your package and then export them in one object:

```ts
// Functions
import myFirstFunction from './helpers/myFirstFunction';
import mySecondFunction from './helpers/mySecondFunction';

// Types
import MyFirstType from './shared/types/MyFirstType';
import MySecondType from './shared/types/MySecondType';

// Export
export {
  // Functions
  myFirstFunction,
  mySecondFunction,
  // Types
  MyFirstType,
  MySecondType,
};
```

## 5. Test

To test your project, create a test npm project somewhere else on your machine, then follow these instructions for testing via `npm link`:

First, build your support library using `npm run build`.

Then, link your support library using `npm link`.

Finally, in your test project, run `npm link <package-name>` where `<package-name>` is the name of your support library.

Repeat these steps as necessary.

## 6. Build and Publish

Build your component lib by running `npm run build`. If no errors occur, check the `/dist` folder for built contents.

Commit and push your code and ask Gabe to publish the library.

<Rule tall>
  Only Gabe publishes packages to npm
</Rule>
