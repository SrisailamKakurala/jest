# jest
jest notes and practice

---

> [Roadmap](./Roadmap.md)

---

## ✅ What is Testing?

### 💡 Simple Definition:

> **Testing is the process of checking whether your code behaves as expected.**

You write some code → You write a test → The test checks:
“Is this code doing what it’s supposed to?”

---

### 🎯 Why Do We Test?

| Reason                       | Explanation                                                     |
| ---------------------------- | --------------------------------------------------------------- |
| 🔒 Prevent bugs              | You catch problems before users see them.                       |
| 🧹 Refactor with confidence  | Tests make sure changes don’t break things.                     |
| 🧪 Document behavior         | Tests describe what your code is supposed to do.                |
| 🤝 Easier team collaboration | Other devs can trust your code doesn’t break existing features. |
| 🚦 Automate quality checks   | Part of CI/CD pipelines—tests run before deployment.            |

---

## ✅ Types of Tests

You’ll commonly hear about **3 levels** of testing. Here's what they mean:

### 1. 🧩 Unit Testing

* **What:** Test a single function or component in isolation.
* **Goal:** Ensure it behaves correctly on its own.
* **Tools:** `Jest`, `Mocha`, `Vitest`

📦 Example:

```js
function add(a, b) {
  return a + b;
}

test("adds two numbers", () => {
  expect(add(2, 3)).toBe(5);
});
```

---

### 2. 🔗 Integration Testing

* **What:** Test how multiple parts work **together**.
* **Goal:** Validate data flows, e.g., function → database → response
* **Tools:** `Jest`, `Supertest`, `React Testing Library`

📦 Example:

* Test a route handler that saves data in a DB and returns a response.

---

### 3. 🌐 End-to-End (E2E) Testing

* **What:** Simulates a user using your app (real browser).
* **Goal:** Validate real user workflows like signing in or posting a comment.
* **Tools:** `Cypress`, `Playwright`, `Puppeteer`

📦 Example:

* Open the browser → Fill login form → Click “Login” → See Dashboard

| Level       | Scope             | Speed     | Stability | Tools               |
| ----------- | ----------------- | --------- | --------- | ------------------- |
| Unit        | Individual pieces | 🔥 Fast   | ✅ Stable  | Jest                |
| Integration | Multiple modules  | ⚡ Medium  | ✅ Stable  | Jest + Supertest    |
| E2E         | Full user journey | 🐢 Slower | ❌ Brittle | Cypress, Playwright |

---

## ✅ Why Jest?

Jest is the **most popular testing framework** for JavaScript and TypeScript.

### 🔥 Benefits of Jest:

| Feature               | Why it matters                                          |
| --------------------- | ------------------------------------------------------- |
| ✅ Zero config         | Just install and write tests — it works out of the box. |
| ⚡ Fast                | Parallel testing, snapshot support                      |
| 🧪 All-in-one         | Includes test runner, assertion library, mocking        |
| ❤️ Works with React   | React projects often use Jest + React Testing Library   |
| 🛠 Rich ecosystem     | Plugins, reporters, TypeScript support                  |
| 📦 Maintained by Meta | Actively maintained, used by large companies            |

---

### 📦 Installing Jest

```bash
npm install --save-dev jest
```

Then, in `package.json`, add:

```json
"scripts": {
  "test": "jest"
}
```

And create a file:

```js
// math.test.js
test("adds 1 + 2 = 3", () => {
  expect(1 + 2).toBe(3);
});
```

Run tests:

```bash
npm test
```

---

### 🧠 Visual Analogy:

Imagine your app is a **car**.

* **Unit test:** Does the engine start?
* **Integration test:** Does the engine + transmission together make the wheels move?
* **E2E test:** Can the car drive from point A to B?

All testing levels are important to ensure **reliability, safety, and performance**.

---

## ✅ Summary for Phase 1

| Concept         | Key Points                                              |
| --------------- | ------------------------------------------------------- |
| What is testing | Ensuring code works as expected                         |
| Types           | Unit, Integration, E2E — each testing a different scope |
| Why Jest        | Fast, reliable, rich features, React-friendly           |
| Setup           | `npm install jest` + `npm test`                         |

---

## 🧪 PHASE 2: Jest Fundamentals (Backend-Focused)

---

#### ✅ Installing Jest

```bash
npm install --save-dev jest
```

In `package.json`:

```json
"scripts": {
  "test": "jest"
}
```

Run tests:

```bash
npm test
```

---

#### ✅ Your First Test

```js
// math.test.js
test("adds 1 + 2 to equal 3", () => {
  expect(1 + 2).toBe(3);
});
```

---

#### ✅ test(), expect(), toBe()

* `test(description, function)` – Defines a test case.
* `expect(actual)` – Wraps a value to apply a matcher.
* `toBe(expected)` – Checks for **strict equality** (`===`).

---

#### ✅ Matchers (Core for backend logic)

| Matcher          | Use Case Example                            |
| ---------------- | ------------------------------------------- |
| `toBe()`         | Exact value (`===`)                         |
| `toEqual()`      | Deep equality for objects/arrays            |
| `toBeTruthy()`   | Checks if value is truthy                   |
| `toBeFalsy()`    | Checks if value is falsy                    |
| `toContain()`    | Checks if an array or string contains value |
| `toHaveLength()` | Checks `.length` of array/string            |
| `toMatch()`      | Regex match in strings                      |
| `toThrow()`      | Checks if a function throws an error        |

---

#### ✅ Examples (Backend Context)

**1. Pure function**

```js
function isAdult(age) {
  return age >= 18;
}

test("returns true if age >= 18", () => {
  expect(isAdult(20)).toBeTruthy();
});
```

**2. Object comparison**

```js
function getUser() {
  return { name: "Sri", role: "admin" };
}

test("returns correct user object", () => {
  expect(getUser()).toEqual({ name: "Sri", role: "admin" });
});
```

**3. String validation**

```js
test("email contains @ symbol", () => {
  expect("hello@example.com").toMatch(/@/);
});
```

**4. Error testing**

```js
function throwError() {
  throw new Error("fail");
}

test("throws error", () => {
  expect(() => throwError()).toThrow("fail");
});
```

---

#### ✅ Running Tests

```bash
npx jest          // runs all test files
npx jest math     // runs math.test.js
npx jest --watch  // watch mode (great for dev)
```

---

Next: Phase 3 – Testing Functions and Modules (Backend Services)

---

## 🧩 PHASE 3: Testing Functions, Modules, & Async Code (Backend-Focused)

---

#### ✅ **Testing Pure Functions (Utilities)**

**Concept:**
Pure functions are deterministic — given the same input, they always return the same output and don't cause side effects (like modifying global state, making network requests, etc.).

**Why it matters:**
These are easiest to test and form the building blocks of logic-heavy backend code (e.g., validations, transformations, business rules).

**Example:**

```js
// utils/calc.js
function multiply(a, b) {
  return a * b;
}

module.exports = multiply;

// tests/calc.test.js
const multiply = require('../utils/calc');

test("multiplies 3 * 2 to equal 6", () => {
  expect(multiply(3, 2)).toBe(6);
});
```

---

#### ✅ **Importing Modules into Test Files**

**Concept:**
You separate concerns in backend by using utility modules and services. To test them, you import the actual module you're testing.

**Example:**

```js
const myService = require('../services/myService');

test("does something with service", () => {
  const result = myService.doWork();
  expect(result).toBe("done");
});
```

---

#### ✅ **Testing Async Code (`async/await`, `done`, Promises)**

**Concept:**
Backend code often uses async patterns — fetching from DBs, calling APIs, etc. You must wait for those to resolve before making assertions.

There are **3 ways** to test async code:

---

1. **Using `async/await` (most common)**

```js
async function fetchData() {
  return "data";
}

test("returns correct data", async () => {
  const data = await fetchData();
  expect(data).toBe("data");
});
```

---

2. **Returning a Promise**

```js
function fetchData() {
  return Promise.resolve("data");
}

test("returns data via promise", () => {
  return fetchData().then(data => {
    expect(data).toBe("data");
  });
});
```

---

3. **Using `done()` callback** (less common)

```js
function fetchWithDelay(cb) {
  setTimeout(() => cb("delayed"), 100);
}

test("uses done callback", (done) => {
  fetchWithDelay((msg) => {
    expect(msg).toBe("delayed");
    done(); // tell Jest the test is complete
  });
});
```

---

#### ✅ **Setup and Teardown (`beforeEach`, `afterAll`, etc.)**

**Concept:**
When testing backend modules like DB access, services, or APIs, you need to prepare before tests and clean up after.

**Lifecycle Hooks:**

| Hook         | Description                   |
| ------------ | ----------------------------- |
| `beforeAll`  | Run once before **all** tests |
| `afterAll`   | Run once after **all** tests  |
| `beforeEach` | Run before **every** test     |
| `afterEach`  | Run after **every** test      |

**Example:**

```js
let db = [];

beforeEach(() => {
  db = ["Sri"];
});

afterEach(() => {
  db = [];
});

test("db has initial user", () => {
  expect(db).toContain("Sri");
});
```

---

**Real World Use Case Example:**

```js
const { connectDB, disconnectDB } = require('../db');
const { getUser } = require('../services/userService');

beforeAll(async () => {
  await connectDB();
});

afterAll(async () => {
  await disconnectDB();
});

test("gets user by email", async () => {
  const user = await getUser("sri@mail.com");
  expect(user.name).toBe("Sri");
});
```

---

Up next: Phase 4 – Mocking Dependencies and External APIs

---

## 🎭 PHASE 4: Mocks and Spies (Backend-Focused)

---

### ✅ `jest.fn()` — Mock Functions

**Concept:**
`jest.fn()` creates a fake function you can inspect: whether it was called, how many times, with what arguments, and what it returned. This is useful when you're testing code that depends on other code (e.g., a controller calling a service).

**Example:**

```js
const myMock = jest.fn();

myMock("hello");

expect(myMock).toHaveBeenCalled(); // ✅
expect(myMock).toHaveBeenCalledWith("hello");
```

You can also give it a custom implementation:

```js
const add = jest.fn((a, b) => a + b);
expect(add(2, 3)).toBe(5);
```

---

### ✅ Mocking Modules

**Concept:**
When testing backend code that depends on modules like DBs, services, or libraries, you don’t want to use real ones. Instead, you mock them.

**Example:**

```js
// services/userService.js
module.exports.getUser = () => {
  return { name: "Real Sri" };
};

// __mocks__/userService.js
module.exports.getUser = () => {
  return { name: "Mock Sri" };
};

// test
jest.mock("../services/userService"); // use __mocks__/userService.js
const { getUser } = require("../services/userService");

test("gets mocked user", () => {
  const user = getUser();
  expect(user.name).toBe("Mock Sri");
});
```

---

### ✅ Spying on Function Calls (`jest.spyOn()`)

**Concept:**
Use `jest.spyOn()` to watch real functions without replacing them entirely. It lets you verify calls, or temporarily override their behavior.

**Example:**

```js
const utils = {
  greet: (name) => `Hello, ${name}`,
};

test("spy on greet", () => {
  const spy = jest.spyOn(utils, "greet");
  const msg = utils.greet("Sri");

  expect(spy).toHaveBeenCalledWith("Sri");
  expect(msg).toBe("Hello, Sri");
});
```

You can also mock implementation:

```js
spy.mockImplementation(() => "Mocked Hello");
```

---

### ✅ Mocking API Calls (`fetch`, `axios`)

**Concept:**
Your backend may make external HTTP calls (to 3rd-party APIs or microservices). You don't want those to run during tests — mock them.

#### Axios Example:

```js
const axios = require("axios");
jest.mock("axios"); // auto-mock all its exports

const fetchData = async () => {
  const res = await axios.get("https://api.com");
  return res.data;
};

test("mocks axios GET", async () => {
  axios.get.mockResolvedValue({ data: "mocked!" });

  const data = await fetchData();
  expect(data).toBe("mocked!");
});
```

---

### ✅ Clearing Mocks (`mockClear`, `mockReset`, `mockRestore`)

| Function        | Description                                              |
| --------------- | -------------------------------------------------------- |
| `mockClear()`   | Clears call history and usage data.                      |
| `mockReset()`   | Like `clear()` but also removes custom implementations.  |
| `mockRestore()` | Restores original function (only works on `jest.spyOn`). |

**Example:**

```js
const mock = jest.fn().mockImplementation(() => "yo");

mock();
mock();

expect(mock).toHaveBeenCalledTimes(2);

mock.mockClear();

expect(mock).toHaveBeenCalledTimes(0); // ✅
```

---

**Summary:**

* Use `jest.fn()` to create fake functions.
* Use `jest.mock()` to replace real modules.
* Use `jest.spyOn()` to monitor real functions.
* Use `mockResolvedValue()` / `mockRejectedValue()` for async mocking.
* Clean mocks with `mockClear`, `mockReset`, or `mockRestore`.

---

Next: **Phase 5 – Testing Express APIs**

---

## ⚙️ PHASE 5: Testing React (with Jest + Testing Library)

---

### ✅ Setup with `@testing-library/react`

Install required packages:

```bash
npm install --save-dev @testing-library/react @testing-library/jest-dom
```

In your test setup (like `setupTests.js`), add:

```js
import '@testing-library/jest-dom';
```

This extends Jest with extra DOM assertions like `toBeInTheDocument`.

---

### ✅ Rendering Components

Use `render()` to render React components in a virtual DOM for testing:

```js
import { render } from '@testing-library/react';
import MyComponent from './MyComponent';

test("renders MyComponent", () => {
  const { getByText } = render(<MyComponent />);
  expect(getByText("Hello")).toBeInTheDocument();
});
```

---

### ✅ Firing Events

Simulate user interactions using `fireEvent` or `userEvent`:

```js
import { render, fireEvent } from '@testing-library/react';

test("button click triggers callback", () => {
  const mockFn = jest.fn();
  const { getByText } = render(<button onClick={mockFn}>Click</button>);
  fireEvent.click(getByText("Click"));
  expect(mockFn).toHaveBeenCalled();
});
```

For more realistic interactions, you can use `@testing-library/user-event`:

```bash
npm install --save-dev @testing-library/user-event
```

```js
import userEvent from '@testing-library/user-event';

await userEvent.type(inputElement, 'Sri');
await userEvent.click(buttonElement);
```

---

### ✅ Assertions on DOM

You can check if elements are present, visible, disabled, etc.:

```js
const { getByText, queryByTestId } = render(<Component />);

expect(getByText("Welcome")).toBeInTheDocument();
expect(queryByTestId("my-element")).toBeVisible();
expect(queryByTestId("submit-btn")).toBeDisabled();
```

These are powered by `@testing-library/jest-dom`.

---

### ✅ Mocking Props, State, APIs

**Mocking Props:**

```js
render(<Greeting name="Sri" />);
expect(screen.getByText("Hello, Sri")).toBeInTheDocument();
```

**Mocking API calls (e.g., axios):**

```js
jest.mock('axios');
axios.get.mockResolvedValue({ data: { message: "Success" } });
```

**Mocking state with hooks:**

If you use `useState`, `useEffect`, etc., no special mocking is needed unless you're mocking the hook itself (advanced).

---

### 🛠 Example: Full Test Case

```js
import { render, fireEvent, screen } from '@testing-library/react';
import Button from './Button';

test("calls onClick when clicked", () => {
  const mockFn = jest.fn();
  render(<Button onClick={mockFn}>Click</Button>);

  fireEvent.click(screen.getByText("Click"));
  expect(mockFn).toHaveBeenCalledTimes(1);
});
```

---

**Summary:**

* Use `render()` to mount components.
* Interact with `fireEvent` or `userEvent`.
* Assert presence/behavior using `@testing-library/jest-dom`.
* Mock props, API calls, or context where necessary.

---

Next: **Phase 6 – Testing Express APIs** (backend-focused)

---

## 🚦 PHASE 6: Coverage, Best Practices, and Advanced Features

---

### ✅ Code Coverage (`--coverage`)

* Run tests with coverage info:

```bash
npx jest --coverage
```

* You'll get a breakdown of how much of your code is covered:

  * **Statements**: total executed lines
  * **Branches**: if/else, switch cases, etc.
  * **Functions**: how many functions are invoked
  * **Lines**: actual number of lines run

🧠 Aim for **80%+ coverage**, but don't blindly chase 100%. Focus on critical paths.

---

### ✅ Snapshot Testing

* Useful for testing UI output consistency:

```js
import { render } from '@testing-library/react';
import Component from './Component';

test("renders correctly", () => {
  const { asFragment } = render(<Component />);
  expect(asFragment()).toMatchSnapshot();
});
```

* Jest saves the output as a `.snap` file.
* If the UI changes intentionally, update the snapshot:

```bash
npx jest -u
```

---

### ✅ Testing Edge Cases and Error Boundaries

* Always test for invalid inputs, empty states, and thrown errors:

```js
test("throws on bad input", () => {
  expect(() => myFunction(null)).toThrow("Invalid input");
});
```

* For React, test error boundaries with `ErrorBoundary` components.
* For APIs, simulate 400/500 errors and test how the UI or logic handles them.

---

### ✅ Test Folders & Naming Conventions

**Structure:**

```
src/
  components/
    Button/
      Button.jsx
      Button.test.jsx
  utils/
    formatDate.js
    formatDate.test.js
```

**Alternatives:**

* Place tests in `__tests__` folders
* Use `.spec.js` or `.test.js`

✅ Consistency > convention

---

### ✅ Organizing Test Suites (`describe`, `it`)

* Use `describe()` to group related tests
* Use `it()` or `test()` for individual cases

```js
describe("formatDate", () => {
  it("formats correctly", () => {
    expect(formatDate("2025-05-05")).toBe("May 5, 2025");
  });

  it("handles invalid date", () => {
    expect(() => formatDate(null)).toThrow();
  });
});
```

This improves readability, especially in long test files.

---

### ✅ Custom Matchers

Install `jest-extended`:

```bash
npm install --save-dev jest-extended
```

Then in `setupTests.js`:

```js
import 'jest-extended';
```

Example:

```js
expect([1, 2, 3]).toIncludeAnyMembers([3, 4, 5]);
expect('  ').toBeEmpty();
```

Also helpful:

* `toBeNumber()`
* `toStartWith()`
* `toBeOneOf()`

---

### 📚 Tools

* `jest-extended`: for powerful, readable matchers
* `jest-mock-axios`: to simulate axios calls in isolation

```bash
npm install --save-dev jest-mock-axios
```

Example:

```js
import mockAxios from 'jest-mock-axios';

afterEach(() => {
  mockAxios.reset();
});
```

---

**Conclusion:**

* Use coverage to guide—not dictate—your testing.
* Snapshots for UI, custom matchers for clarity.
* Organize tests cleanly, cover edge/error cases well.

---

Next: **Phase 7 – Testing Express APIs and Middleware (Backend Focus)**?

---

## 🚢 PHASE 7: CI/CD Integration and Production Readiness

### 🎯 Goal: Use Jest in real-world and team-based codebases

---

### ✅ Run Jest in GitHub Actions

**What is GitHub Actions?**
GitHub Actions is a CI/CD tool that runs scripts automatically when events happen in your repo (like pushing code).

**Why use it with Jest?**
To run your tests automatically every time code is pushed or a pull request is made.

**Example:**

```yaml
- name: Run tests
  run: npm run test -- --ci
```

* `npm run test`: runs your test script from `package.json`.
* `--ci`: runs Jest in Continuous Integration mode for consistent output and performance.

---

### ✅ Lint Test Code with ESLint Rules

**What is Linting?**
Linting checks your code for bugs and style issues.

**Why lint test code?**
To keep test files clean, readable, and consistent across a team.

**How to lint test files:**

* Add lint rules for test files in `.eslintrc.js` or `eslint.config.js`.
* Use plugins like `eslint-plugin-jest`.

Example config:

```js
overrides: [
  {
    files: ['**/__tests__/**/*.ts', '**/*.test.ts'],
    env: { jest: true },
    plugins: ['jest'],
    extends: ['plugin:jest/recommended']
  }
]
```

---

### ✅ Use `ts-jest` for TypeScript

**Why use ts-jest?**
Jest does not understand TypeScript out of the box. `ts-jest` compiles `.ts` files before running them.

**Steps:**

1. Install `ts-jest`:

   ```bash
   npm install --save-dev ts-jest
   ```
2. Configure Jest:

   ```bash
   npx ts-jest config:init
   ```
3. Add `preset: 'ts-jest'` in `jest.config.js`.

**Now you can write tests in `.ts` and `.tsx` files** and still use all TypeScript features.

---

### ✅ Common Performance Issues

**Slow tests can hurt CI pipelines. Common causes:**

* Too many setup/teardown operations
* Using real APIs instead of mocks
* Unoptimized loops or database calls in tests
* Global states not reset properly

**Tips to fix:**

* Use `beforeEach` wisely
* Avoid external calls, use mocks
* Run tests in parallel if safe
* Use `--maxWorkers` to control concurrency

---

### ✅ Real-World Monorepo Testing Strategies

**What is a Monorepo?**
A repository that contains multiple packages or apps (e.g., frontend + backend).

**Challenges:**

* Running all tests can be slow
* Shared code changes can affect many packages

**Strategies:**

* Use tools like [Nx](https://nx.dev), [Turborepo](https://turbo.build/) to run only affected tests
* Run tests in isolated packages
* Cache results using GitHub Actions or CI tools
* Use code coverage to see which packages are impacted

---

This phase helps you go from writing tests to **automatically running them in production pipelines**, ensuring reliability, performance, and teamwork.

---

## 🚀 PHASE 8: Open Source & Contributions

### 🎯 Goal: Contribute to OSS projects confidently

---

### ✅ Reading existing Jest tests in open source projects

* Explore how large, real-world projects like **React** or **Vite** organize and write their tests.
* Look at:

  * Folder structure (`__tests__`, `*.test.ts`)
  * How mocks/stubs are used
  * How they test edge cases and async behavior
* Learn patterns used in production: setup files, custom matchers, utilities.

---

### ✅ Adding/improving test coverage

* **Test coverage** shows how much of your code is tested.
* OSS projects often have tools like `coverage/` reports in PRs.
* Look for:

  * Untested code paths
  * Complex functions missing edge case tests
* Use `jest --coverage` locally to check what’s missing.
* Add meaningful tests, not just for % increase — aim for **quality**.

---

### ✅ Understanding test structure in large repos (e.g., Vite, React)

* Large repos are modular; they separate tests by package or feature.
* You’ll find:

  * `setupTests.ts` for global configs (mocks, polyfills, etc.)
  * `utils/` for custom test helpers
  * Tests close to source code (`src/component/Button.test.ts`)
* Read and follow the structure already in use.

---

### ✅ Following code style and coverage reports

* OSS projects usually have:

  * ESLint + Prettier rules
  * Test coverage thresholds
  * GitHub Actions that run tests on PRs

To contribute well:

* Match the existing code style (indentation, naming, etc.)
* Pass linting and coverage checks
* Read the `CONTRIBUTING.md` file (usually contains test commands, coverage tools, and coding standards)

---

## 📦 Bonus Tools to Know

* **`msw` (Mock Service Worker)**

  * Mocks network requests in tests.
  * Useful for REST/GraphQL APIs — no real backend needed.
  * Works in both unit and integration tests.

* **`jest-dom`**

  * Extends `expect()` with custom DOM matchers.
  * Example: `expect(button).toBeDisabled()`
    Makes tests more readable and user-centric.

* **`vitest`**

  * A faster alternative to Jest, especially for Vite projects.
  * Jest-compatible API — easy to migrate.
  * Built-in TypeScript support and ESM-friendly.

---

## 🔁 Recap: Progression Summary

| Level | Focus                         | Tools Used                   |
| ----- | ----------------------------- | ---------------------------- |
| 1     | Understand testing            | plain `jest`                 |
| 2     | Write unit tests              | `jest`, `expect`, async      |
| 3     | Learn mocking                 | `jest.fn`, `jest.mock`       |
| 4     | Test React UIs                | `@testing-library/react`     |
| 5     | Master coverage + CI          | `--coverage`, GitHub Actions |
| 6     | Contribute to OSS confidently | Read/write prod-level tests  |

---

This phase prepares you to **read, write, and improve tests in real-world open source codebases**, contribute valuable patches, and follow best practices used by industry professionals.

---


