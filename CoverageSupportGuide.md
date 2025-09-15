# Coverage Support Guide

This guide is intended as a resource to review in preparatioinfor Gabe taking time off or in the event of sickness or emergency.

## Prepare

### Read the EdTech Guide

All apps that Gabe works on follow the same structure and style as outlined in the [EdTech Guide](https://harvard-edtech.github.io/edtech-guide/).

See the Table of Contents in the [EdTech Guide](https://harvard-edtech.github.io/edtech-guide/) for a full breakdown of all documentation. It covers everything from folder structures (so you know where to look for each type of file), typescript rules and processes (so you know how to read and write code), React design and development (so you can quickly understand front-end code), logging practices (so you can trace errors backward through code to debug issues), server and API norms (so you can debug understand how to support server-side issues), database libs and processes (so you can access, reason through, and debug database issues), unit and end-to-end testing (so you can understand, run, and add to tests), processes for updating and patching instances, and so much more.

The best way to become intimately familiar with the contents of the guide is to attend one of Gabe's full ~8 week training courses that's offered when Gabe onboards a new team member.

### Familiarize Yourself with Integration Libs

Gabe's apps centralize the integration with common platforms and tools. This is critical to be able to maintain, update, and keep these integrations secure.

- [CACCL](https://harvard-edtech.github.io/caccl/): Canvas LTI + API Integration
- [CACCL API](https://harvard-edtech.github.io/caccl-api/): The API portion of Canvas Integration
- [ZACCL](https://harvard-edtech.github.io/zaccl/): Zoom API Integration
- [ReactKit](https://github.com/harvard-edtech/dce-reactkit): Reusable React components, helper functions, constants, and more
- [ExpressKit](https://github.com/harvard-edtech/dce-expresskit): Reusable Express endpoint structure, security, helper functions, and more
- [Mango](https://github.com/harvard-edtech/dce-mango/blob/main/src/classes/Collection.ts): Mongo/AWS DocDB operations
- [AI](https://github.com/harvard-edtech/dce-ai): GenAI integration that automatically tracks cost, allows for strongly typed responses, and makes it easy to switch secure models
- [Kaixa](https://harvard-edtech.github.io/create-kaixa/): Katalon end-to-end testing framework
- [Dev Wizard](https://github.com/harvard-edtech/dce-dev-wizard): deployment manager, security checker, environment variable modifier, db connector, log tailer, and much more
- [Identity API](https://github.com/harvard-edtech/harvard-identity-api): Harvard IAM API library
- [Send Email](https://github.com/harvard-edtech/dce-send-email): email sender via AWS services
- [iCommons](https://github.com/harvard-edtech/dce-icommons): iCommons API library
- [Raixa](https://github.com/harvard-edtech/raixa): React component unit testing library

### Checkout the Code

This part is simple, but should be repeated in preparation for each time you prepare for coverage because you'll want to have the most up-to-date code:

1. Clone the repos of the apps you're covering
1. Find the branch (probably "main") for the instance you're covering (if not sure which target branch, use the dev wizard)
1. Fetch/pull to get the most up-to-date code
1. Run `npm install` and make sure it completes successfully

All apps that Gabe works on follow the same code structure, file and variable naming, code documentation process, and so much more.

All code can be found in the [Harvard EdTech](https://github.com/harvard-edtech) GitHub organization, but here are some critical app repos:

- [Gather](https://github.com/harvard-edtech/gather)
- [Immersive Classroom](https://github.com/harvard-edtech/immersive-player)
- [Hello Harvard](https://github.com/harvard-edtech/harvard-hello)

Branch names follow the standard set by the "GitHub" section of the [EdTech Guide](https://harvard-edtech.github.io/edtech-guide/). Generally, for support purposes, you'll be mostly interested in the "main" branch, which is the branch that is deployed to the prod instance.

Throughout this guide, when asked to run commands in the terminal, those commands should always be run after updating the code, running `npm install`, and making sure you're in the top-level folder of the project.

### Familiarize Yourself with Server Code

The [Server Folder Structure](https://harvard-edtech.github.io/edtech-guide/#server-folder-structure) and surrounding sections of the [EdTech Guide](https://harvard-edtech.github.io/edtech-guide/) break down server design. Each project will have a `/server` folder with all helper functions, constants, types, and endpoints.

### Learn to Use the Dev Wizard

The dev wizard is installed into each of Gabe's apps and handles debugging, deployments, environment variables, connecting to the database, reading recent logs, and much more.

To launch the dev wizard, use `npm run dev:wizard`. We'll assume your AWS CLI is configured. If it isn't, you'll need to work with Jay to get your credentials set up.

First, you'll need to choose an instance (Prod, Stage, etc.)

Then, an interface will appear to guide you through each of the processes. Checking environment variables, the target that was deployed to the instance, performing new deployments, tail the logs, and more should all be rather straightforward.

To start a connection with the database, choose to connect to the database, and a new wizard will appear that will walk you through connecting via a Mongo client like Robo 3T.

### Familiarize Yourself with Client Code

The [React](https://harvard-edtech.github.io/edtech-guide/#react) section in the [EdTech Guide](https://harvard-edtech.github.io/edtech-guide/) outlines the entire development process for client-side code, which is broken down into React Components, helper functions, constants, and types.

The documentation in the [React](https://harvard-edtech.github.io/edtech-guide/#react) section outlines the structure for all components. This is critical for support and debugging because you'll be able to navigate the code much faster if you know the formatting and documentation style. For example, every component puts its props near the top of the file in the `Types` section, and every single prop has full documentation and types.

### Gain Contextual Understanding

Watch the app tutorials, try it out, see how users launch the app and navigate around the app, and learn about other relevant and surrounding systems so you can begin to understand the boundaries between systems and how each system impacts other systems.

## Support Incoming Questions and Issues

There are two types of support processes that you'll be part of: answering/triaging technical questions about the app and supporting issues with the app.

In either case, it's important to be able to perform educated actions:

1. Do we have all the information? Ask the reporter for complete information including who brought this up, the exact time it happened, which course, impacted users and their ids, the precise error message and error code they encountered, browser and operating system settings, internet quality, and any other relevant details and current state of things (perhaps Zoom or HarvardKey was experiencing issues at the time, for example)
1. Is the question/issue about this app? It could be user error, training/communication issues, bugs in other systems, AWS deployment/memory/networking issue, problem logging in, wrong permissions/access, or many other issues. It's important to rule these out first before opening a can of worms and assuming there's a coding problem
1. Who should be involved? Bring in the appropriate stakeholders on the Dev and Teaching and Learning teams, or other groups from around Harvard
1. What process am I following? Document the process you followed, what worked, what did not work. It's easy to get caught up in debugging and not keep good notes of exactly what you checked/did
1. Is this truly urgent? Know when to table an issue and save it for when Gabe returns. Most errors have workarounds, stopgaps, or human-based solutions (training, manual processes, etc.) that can sufficiently solve or postpone the problem until the end of Gabe's time away
1. Do we need to bring in Gabe? Throughout the process, send Gabe updates but don't mark them as urgent. If it's life or death and you were not able to resolve the issue without them, then send an urgent message to Gabe. It is not in any way guaranteed that Gabe will have the network connectivitiy, time, resources, equipment, etc. to respond, so continue working on a stopgap solution in the meantime

### Attempt to Reproduce the Issue

1. **Research:** Gather as much information as you can about the issue: who encountered it, when did they notice the issue, what were they doing at the time, which course, which error messages/error codes, steps they took, etc.
1. **Reproduce in Sandbox:** attempt to reproduce the issue with test resources, in a test environment/sandbox, and with test users. Watch logs, open the network and console tabs of the developer tools in your browser. See if you can reproduce the issue while also gaining extra information about any clientside console/network monitor or serverside logs that might help you pinpoint the issue in the app.
1. **Reproduce in Prod:** if you cannot reproduce the issue, ask yourself if the action is destructive, dangerous, or modifies data that will impact student experience in a way that cannot be undone or cleaned up. If it's safe, perform the steps to reproduce the issue in prod. If possible, act as the user of interest, perform the same steps, use the same operating system and browser, and so on. Again, watch logs.

### Tail Container Logs

During preparation, you would have become familiar with the process of opening the dev wizard. You can tail server container logs very easily from within the dev wizard.

### Query the App Log Collection

During preparation, you would have made sure you have access to the app database. Check out the Log collection (see [Log type](https://github.com/harvard-edtech/dce-reactkit/tree/main/src/types/Log) for documentation) and query to find relevant logs.

### Bottom Up: Trace from the Error

Search the code for the error code. It should appear in either the `ClientErrorCode.ts` or `ServerErrorCode.ts` file if it's an error originating from the app itself. If it's an error from one of the other libs, the error code will be found in those libs instead. Error codes always start with the initials of the app or library, which provides a helpful clue as to where to look for the error code.

Once you find the error code in on ef the error code enum type files, you'll see the longer name it was given. For example, if the error code is `ICC25`, we would find it in the Immersive Classroom Client (ICC) in the `ClientErrorCode.ts` file on a line that looks like this:

```ts
ShareoutBoardsNotFound = 'ICC25',
```

The name of the error code (ShareoutBoardsNotFound) serves as a very short description of the error. You can then begin tracing the error code upward through the code. Search the code for that error code name by searching for the name inside the type: `ClientErrorCode.ShareoutBoardsNotFound`. You will probably find it just once, but you may find it a few times if it's a general error that could occur many types of ways. With this example, perhaps we found the error in the code like this:

```ts
throw new ErrorWithCode(
  `Failed to load Shareout boards for video ${videoId} in course ${courseId}.`,
  ClientErrorCode.ShareoutBoardsNotFound,
);
```

From there, I can look at surrounding code to see what might have gone wrong, and trace bottom up from the error.

### Top Down: Trace from the Endpoint

Discover the feature that's encountering an issue and figure out which endpoint is triggering the error. If this is a client-side error, this method is irrelevant. Some tactics for figuring out the endpoint is to open the network tab in a browser inspector, then reproduce the error and figure out which endpoint had an error.

Once you find the error, create a template version of the endpoint and find it in the server code. For example:

```ts
// Endpoint:
/api/ttm/courses/12345/users/67890/analytics
```

There are two template placeholders that we see in the URL:

```ts
// Template:
/api/ttm/courses/:courseId/users/:userId/analytics

// Where the following params are defined:
courseId = 12345
userId = 67890
```

Once you find the endpoint, you can trace downward through the code, following the logic path and see if you can discover the issue.

### Debug in AWS

Sometimes, the error has to do with the server restarting, running out of memory or other resources, disconnecting from the db, or other infrastructure issues.

If you suspect an issue in AWS, work with Jay or his LHT to figure out how to approach the problem. There are also some tactics you can employ on your own:

Find the ECS cluster, figure out how old the tasks are. If they're younger than expected, or if their age indicates that there was a restart around when the user encountered the error, it might be expected that the user got a "Session Expired" error while the server restarted. But, if the age doesn't line up with an expected release, perhaps the cluster restarted due to a terminal error. Look back in the AWS logs for stopped instances to see if you can find any clues.

Also, check memory and CPU usage and look back to the time where the error was encountered. Perhaps there's a spike in resource utilization and that might indicate the source of the issue.

### Simulate Slow Network

Many of our users have very slow internet. Use your browser's debugging tools to simulate a very slow internet speed and see if that helps you reproduce the error. This is particularly useful for timeouts, certain portions of the page not loading, images loading after content, and other network issues.