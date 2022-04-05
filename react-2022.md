# Comprehensive Software Development Guide

Created by Gabe Abrams in 2022. This will probably be out of date within minutes of this guide being published. Be alert and be flexible.

<style>
  Rule {
    display: block;
    font-weight: bold;
    color: #FFC107;

    border: 1px solid #FFC107;
    border-radius: 5px;

    padding-top: 3px;
    padding-bottom: 3px;
    padding-left: 8px;
    padding-right: 8px;
  }
  Rule::before {
    content: 'Rule: ';
    font-weight: normal;
  }
  Rule[tall] {
    margin-bottom: 10px;
  }
</style>

# Set Up Your Workspace

_Note:_ if using windows, start by installing a terminal replacement like Git Bash. It must function like a Mac OS or Linux machine. Otherwise, virtualize Linux.

## Typescript

Javascript environment:

1. Install Node.js LTS
1. Install NVM

NPM setup

1. Install npx using `npm i -g npx`

## Code Editor

Install required VSCode extensions:

1. `Code Spell Checker` by Street Side Software - flags spelling errors in your code
1. `ESLint` by Microsoft - required for eslint enforcement
1. `npm` by Microsoft - required for code highlighting
1. `TODO Highlight` by Wayou Liu (alternative is okay) - highlights TODOs

Remove banned extensions or disable them on all our projects:

1. `GitHub Copilot` - this removes opportunity for learning
1. `Prettier` - formats in ways that do not necessarily follow our rules

If you want, install optional VSCode extensions:

1. `Path Intellisense` by Christian Kohler - helps auto-complete local imports
1. `npm Intellisense` by Christian Kohler - helps auto-complete lib imports
1. `Auto Close Tag` by Jun Han - automatically closes html tags
1. `gitignore` by michelemelluso - right click and add to gitignore
1. `Thunder Client` by Ranga Vadhineni - lets you easily send api requests for testing

If you want, update these VSCode settings:

1. Use two spaces instead of tabs
1. Emmet: Show Expanded Abbreviation = inMarkupAndStylesheetFilesOnly
1. Turn on "Bracket Pair Colorization"
1. Typescript Preferences > Quote Style = "single"

Troubleshooting ESLint:

If eslint isn't working on the project, first try reinstalling it: Shift + CMD/Ctrl + P > Reinstall Extension > ESLint.

If that doesn't fix it, try the solutions in this [ESLint Troubleshooting Checklist](https://dev.to/tillsanders/eslint-not-working-in-vscode-help-build-a-troubleshooting-checklist-fdc).

# Create a Project

Create a new npm project:

1. Create a git repo and clone it
1. Initialize the project: `npm init`
1. Add a `.gitignore`
1. Add eslint rules in each sub-project separately (client and server, for example): `npm init dce-eslint`
1. Add `private: true` flag in `package.json`

Set up the server:

1. Create a `server/` folder
1. Inside the `server/` folder, initialize the project: `npm init`
1. Add a `.gitignore`
1. Add `private: true` flag in `package.json`

Set up the client

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

# Project and File Management

## Assigned Tasks

We use GitHub Projects as our task management system. To see what you're assigned, visit the repo, click `Projects`, click our project, and take a look at the `Assigned` column. Cards with your picture on them are yours to do this week.

When you start working on a task, drag the card to `In Progress`. 

When you finish a task, drag the card to `In Review`.

We'll peer-review each-other's work before moving cards to `Done`.

As you work, keep track of everything you work on and update your Google Sheet with things you've done and minutes you've spent.

## GitHub

The main branch of the project is managed by Gabe. Anything that makes it to `main` is Gabe's responsibility, so please do not merge into `main`.

<Rule tall>
    Never commit, merge, or push to main
</Rule>

For each task you work on, check the title and label of the card in GitHub Projects. That label may be "enhancement" or "new-feature" etc.

Before starting to work on that task, create a new branch labeled `<label>/<lowercase-dashed-title>`.

<Rule>
    One branch per task, named appropriately
</Rule>

```bash
# For an "enhancement" task called "Add Simplification Algorithm"
git checkout stage
git pull
git checkout -b enhancement/add-simplification-algorithm
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

# Typescript Basics

## Types

### Primitives

- `number` - all number types (int, float, etc.)
- `string` - text of any length
- `boolean` - either true or false
- `undefined` - unset
- `null` - no value
- `void` - either `undefined` or `null` - but we refrain from using it

### Important Data Structures

- `Array` - array of elements
- `Map` - dictionary with keys and values
- `Set` - set where items can only exist once in the list
- `Object` - unordered map where keys must be strings

### Types and Enums

- `Type/Interface` - a data type/interface
- `Enum` - an enum (does not support dynamic keys or values that are objects)

## Creating Variables

Use `const` when defining variables. Only use `let` if absolutely necessary (a variable's value changes). It is unforgivable to use `var`.

<Rule>
    Use const to define vars. Only use let if necessary
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

Object property modification do **not** count as re-assigning:

```js
// Still use const
const user = {
    name: 'Divardo',
    age: 10,
};

// These do not modify user
user.name = 'Jane';
user.age += 1;
```

We favor longer variable names that are descriptive: `mouseX` is better than `x`.

<Rule>
    Use appropriate naming conventions
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
  When naming css classes, always prefix every class with the name of the component
</Rule>

```css
/* For component Favorite Fruits: */

/* Good: */
.FavoriteFruits-container

/* Bad: */
.container
```

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

We reserve single quotes for typescript and double quotes for JSX. This makes our code differentiable and nestable.

<Rule>
    Only use single quotes in typescript
</Rule>

```ts
import toggleButton from 'toggle-button';

const name = 'Divardo';
```

Arrays that start off empty must have a declared type.

<Rule>
    Arrays must have declared types
</Rule>

```ts
const names: string[] = [];
// or
const names = new Array<string>();
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
    Always use ===  or !== for equality comparisons
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
    Only use ++ or -- in for loop declaration
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

## Classes

Ask yourself: should this code be a helper function or a class? One rule of thumb is that if code will only be instantiated once, it's probably best as a helper function.

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
    Methods that don't use this must be static
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

## Types

We use `Type` to define types (instead of `Interface`) because of some important advanced features that we leverage in React.

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

### Types Cheatsheet

For your reference, here's a types cheatsheet with props that I use frequently:

```ts
// Primitives
string // String
number // Number
boolean // Boolean
undefined // Unset value
null // Absence of value

// Operations
(string | number) // Any type in this list
('blue' | 'red' | 'green') // Any value in a list

// Arrays
string[] // Array of strings
number[] // Array of numbers
Car[] // Array containing objects of type Car
Array<(string | Car)> // Array of strings or objects of type Car

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

## Enums

If a value can take on many pre-determined values, we use enums. However, we understand that enums are limited: keys are not dynamic and values cannot be complex objects. Use enums where possible.

<Rule>
  Prefer enums, but substitute with objects if not possible
</Rule>

```ts
enum Instrument {
  Piano = 'piano',
  Violin = 'violin',
}
```

There are shorthands for numerical enums. To ensure readable database entries and debugging, we prefer string-valued enums, even if those values are just a lowercase version of the key.

## Code Style

To keep code readable and simple, if there are ever more than three of anything (arguments, values, anything), each must be on its own line.

<Rule>
  If more than three elements, put each element on its own line
</Rule>

```ts
Additionally, whenever there is one item on its own line, all other items must be on their own lines as well.
```

Arrays:

```js
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

For all arrays, function arguments, object definitions, and other comma-delineated objects, use trailing commas. This helps create clean git diffs and reduces typos.

<Rule>
  Use trailing commas
</Rule>

```
See the examples above. Look for trailing commas.

Note: this is not supported in `.json` files. Thus, when possible, we prefer `.tsx` for data if possible.
```

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

### Array.forEach – loop

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

### Array.map – create new value based on each item

```ts
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

### Array.some – returns true if at least one passes the test

```ts
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

### Array.every – returns true if all pass the test

```ts
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

### Array.filter – filters an array, keeping only items that pass the test

```ts
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

## Object Functions

Object functions are great for iterating through objects. Use them whenever possible. But just like array functions, if using async/await inside the loop, you'll need a for loop.

<Rule>
    Use object functions whenever possible unless await is used inside
</Rule>

### Object.keys(...) – get an array of keys

```js
const idToName = {
  12459: 'Divardo',
  50829: 'Calicci',
  50628: 'Keala',
};

const ids = Object.keys(idToName);
```

### Object.values(...) – get an array of values

```js
const idToName = {
  12459: 'Divardo',
  50829: 'Calicci',
  50628: 'Keala',
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

## Default Params

To include a default value for a param, do this:

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
const helper = (a: string, b: string = 'hi', c: number) => {
  ...
};
```

With types and defaults, arguments can take up a lot of space. As usual, if one item is on another line, all items must be on their own lines. Here's how to do this with arguments:

```ts
const helper = (
  requiredParam1: string,
  requiredParam2: number,
  optionalParam: string = 'default value',
) => {
  // ...
};
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
    When importing, leave off extension if `.tsx`
</Rule>

```ts
import MyComponent from '../shared/MyComponent';
```

If a module is a folder, leave off `index.tsx` when importing.

<Rule>
    Leave off `index.tsx` when importing file modules
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

## Asynchronous Code

Typescript is a single-threaded interpreted language and is _much_ slower than C/C++ and other compiled languages. _But_, asynchronous code runs really fast and is great for servers and good for simple clients like browsers. Thus, Express and React are great choices as long as we use asynchronous code when necessary.

### Asynchronous Functions

This function is non-blocking and executes its function body in the background.

```ts
const funcName = async () => {
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
/*                                  Types                                 */
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
/*                                Constants                               */
/*------------------------------------------------------------------------*/

// Add description of constant
const ADD_CONSTANT_NAME = 'add constant value';

/*------------------------------------------------------------------------*/
/*                                  State                                 */
/*------------------------------------------------------------------------*/

/* -------------- Views ------------- */

enum View {
  // Add description of view
  AddViewName = 'add-view-name',
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
  AddActionTypeName = 'add-action-type-name',
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
/*                             Static Helpers                             */
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
/*                                Component                               */
/*------------------------------------------------------------------------*/

const AddComponentName: React.FC<Props> = (props) => {
  /*------------------------------------------------------------------------*/
  /*                                  Setup                                 */
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
  const addRefName = useRef(null);

  /*------------------------------------------------------------------------*/
  /*                           Component Functions                          */
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
  /*                           Lifecycle Functions                          */
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
  /*                                 Render                                 */
  /*------------------------------------------------------------------------*/

  /*----------------------------------------*/
  /*                  Modal                 */
  /*----------------------------------------*/

  // Modal that may be defined
  let modal: React.ReactNode;

  /* ------- AddFirstTypeOfModal ------ */

  if (addLogicToDetermineIfModalIsVisible) {
    // TODO: implement

    // Create modal
    modal = (
      <addJSXOfModal />
    );
  }

  /*----------------------------------------*/
  /*                 Views                  */
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
  /*                 Main UI                */
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
/*                                 Wrap Up                                */
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

```ts
/**
 * Button that shows the "forgot password" panel
 * @author Divardo Calicci
 */
```

### Git Norms

**Commit frequently**. We will squash later, but it's nice to have a detailed history. Plus, this is great for your careers.

### CSS Units

We prefer **rem** for elements that have the same sizing, independent of their context (independent of their parent styling and size).

We prefer **em** for elements that have variable sizing where their sizing depends on their parent or context.

For very small details that are not required in order to understand the functionality or content of a tool (example: a very fine border), you can use **px**. If this part of the UI is important for functionality or content, then setting it as a specific number of pixels will mean that people with visual impairments will not be able to zoom in and see it in certain settings.

Why? When people customize their browser settings (fonts, font size, viewport settings, etc.) it will mess up your layout and create unexpected layouts. Plus, this makes your tool more accessible (it adapts better to user settings).

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
  Cart = 'cart',
  // Add shipping and billing information
  ShippingAndBillingForm = 'shipping-and-billing-form',
  // Review order details and confirm
  Review = 'review',
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
  AddRecipient = 'add-recipient',
  // Update the subject of the email
  UpdateSubject = 'update-subject',
  // Reset the entire email form
  ResetForm = 'reset-form',
  // Show the "email is being sent" indicator
  ShowSendingIndicator = 'show-sending-indicator',
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
      ActionType.ResetForm
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

### Render

You may have noticed that we separate sections of our code with comment blocks. Aside from the usual very large and wide comment block delimiting sections of the code, we use two smaller types of comment blocks to organize our render functions.

Medium blocks to separate parts of the UI:

```ts
/*----------------------------------------*/
/*                  Modal                 */
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
/*                 Main UI                */
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
  Never create a React Context Provider without a discussion with your manager and the rest of the team
</Rule>

### No Images

Unless absolutely necessary, never use images. Great alternatives are glyphs via `FontAwesome` or svg vector graphics. If you think that an image is required, ask your manager before continuing. We do this to aggressively keep our apps small in size. We have students all over the world, many with very slow internet connections, so load time is very important.

<Rule tall>
  Never use an image without permission from your manager
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
enum Car {
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
  RED = 'red',
  GREEN = 'green',
  BLUE = 'blue',
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
  RED,
  GREEN,
  BLUE,
}

// Good:
enum AllowedColors {
  RED = 'red',
  GREEN = 'green',
  BLUE = 'blue',
}

// Bad (allowed colors are not numbers)
enum AllowedColors {
  RED = 1,
  GREEN = 2,
  BLUE = 3,
}

// Good (number of wheels is a number naturally)
enum VehicleWheelConfig {
  BIKE = 2,
  TRICYCLE = 3,
  CAR = 4,
  FLATBED_TRUCK = 16,
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
$border-width: 5px;
```

# Express

// TODO: write

# Mongo/DocDB

// TODO: write

## Concepts

### Schema

A schema is a description of what documents in a collection should look like.

Example: description of what a User looks like.

### Model

A model is an instance of an object from the database.

Example: a specific User instance that you can interact with.

### Query

A lookup in the database. Basically, like a search.

# Unit Tests

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

We use a custom-built wrapper for [React Testing Library (RTL)](https://testing-library.com/docs/react-testing-library/intro/) that we call [Raixa](bit.ly/dce-raixa). Although we do not directly interact with RTL, for your own professional development, we recommend that you take some time to learn it. But for our purposes, if a testing functionality is not available in [Raixa](bit.ly/dce-raixa), we will add the functionality to [Raixa](bit.ly/dce-raixa) instead of using RTL.

Create a test:

```ts
test(
    'description of test',
    async () => {
        ...
    },
);
```

Inside the test, render the component of interest, including appropriate props:

```ts
Raixa.render(
    <MyComponent
        prop1={value}
        prop2="value"
    />
);
```

All testable items must have either an `id` or a `className` for reference. We then use `container.querySelector` to find elements, even though this is not recommended. We do this so identifiers can be shared across our unit and our end-to-end tests.

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

Use `npm test` to start the jest test runner.

# Automated UI Testing

We use Katalon for all our end-to-end automated cross browser testing.

## Set Up Katalon

### 1. Install Katalon:

Visit [Katalon.com](https://www.katalon.com/katalon-studio/), create an account, and then install the free version of the tool.

### 2. Modify Katalon Preferences:

In Katalon's preferences panel, make the following changes:

`Katalon > Git > Enable Git Integration` – Turn this off (uncheck the box)

`Katalon > Test Case > Default Open View` – Set to "Script View"

`General > Editors > Text Editors > Displayed Tab Width` – Set this to "2"

`General > Editors > Text Editors > Insert Spaces for Tabs` – Turn this on (check the box)

## Keep Katalon Up-to-date

Regularly update your web drivers:

1. Launch Katalon
1. Under `Tools > Update WebDrivers`, one by one, click each browser and update it

## Project and File Management

All of our tests will be organized in a GitHub repo that's separate from the code. Ask your project manager about cloning that repo.

Our test case files follow a strict folder structure: there should only be one top-level folder called "All Tests" inside of the "Test Cases" folder. Then, inside "All Tests", we create one folder for each feature of the project. Name your test cases in a descriptive manner. Example: "User can log in after password is reset"

## Write a Test

Our tests are written in the `Groovy` language, which looks like `Java`.

Check out the [Kaixa Docs](https://harvard-edtech.github.io/create-kaixa/) for guides on how to write end-to-end tests, but it should feel just like writing tests with [Raixa](bit.ly/dce-raixa).

## Running a Test

1. Start a development copy of the app (server and/or client)
1. Open the test case
1. Next to the play button, click the dropdown and choose a browser
