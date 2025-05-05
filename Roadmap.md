## 🧭 Jest Learning Roadmap (Beginner → Advanced)

> ✅ Each phase builds on the last. We’ll include theory + hands-on examples + best practices.

---

### 🔰 PHASE 1: Basics of Testing

#### 🎯 Goal: Understand what testing is and why it matters.

* ✅ What is testing?
* ✅ Types of tests: Unit, Integration, E2E
* ✅ Why Jest? (Popular, fast, zero-config, works with React, Node, etc.)

📚 Resources:

* [Jest Docs – Introduction](https://jestjs.io/docs/getting-started)

---

### 🧪 PHASE 2: Jest Fundamentals

#### 🎯 Goal: Learn Jest's core syntax and test-running behavior.

* ✅ Installing Jest (`npm install --save-dev jest`)
* ✅ Your first test: `test()`, `expect()`, `toBe()`
* ✅ Matchers: `toEqual`, `toContain`, `toBeTruthy`, etc.
* ✅ Running tests: `npx jest` / configuring in `package.json`

🛠 Example:

```js
test("adds 1 + 2 to equal 3", () => {
  expect(1 + 2).toBe(3);
});
```

📚 Resources:

* [Jest Matchers](https://jestjs.io/docs/using-matchers)

---

### 🧩 PHASE 3: Testing Functions, Modules, & Async Code

#### 🎯 Goal: Write real-world tests for different JavaScript functions.

* ✅ Testing pure functions (utilities)
* ✅ Importing modules into test files
* ✅ Testing async code (`async/await`, `done`, promises)
* ✅ Setup and teardown (`beforeEach`, `afterAll`)

🛠 Example:

```js
async function fetchData() {
  return "data";
}

test("fetchData returns data", async () => {
  const result = await fetchData();
  expect(result).toBe("data");
});
```

---

### 🎭 PHASE 4: Mocks and Spies

#### 🎯 Goal: Understand mocking — a crucial part of testing external behavior.

* ✅ `jest.fn()` — mock functions
* ✅ Mocking modules
* ✅ Spying on function calls (`jest.spyOn`)
* ✅ Mocking API calls (`fetch`, `axios`)
* ✅ Clearing mocks (`mockClear`, `mockReset`)

🛠 Example:

```js
const myMock = jest.fn();
myMock("called");

expect(myMock).toHaveBeenCalled();
```

📚 Resources:

* [Jest Mock Functions](https://jestjs.io/docs/mock-functions)

---

### ⚙️ PHASE 5: Testing React (with Jest + Testing Library)

#### 🎯 Goal: Test React components like a pro.

* ✅ Setup with `@testing-library/react`
* ✅ Rendering components
* ✅ Firing events
* ✅ Assertions on DOM
* ✅ Mocking props, state, APIs

🛠 Example:

```js
render(<Button onClick={mockFn}>Click</Button>);
fireEvent.click(screen.getByText("Click"));
expect(mockFn).toHaveBeenCalled();
```

📚 Resources:

* [React Testing Library Docs](https://testing-library.com/docs/react-testing-library/intro/)

---

### 🚦 PHASE 6: Coverage, Best Practices, and Advanced Features

#### 🎯 Goal: Write clean, reliable, maintainable tests.

* ✅ Code coverage (`--coverage`)
* ✅ Snapshot testing
* ✅ Testing edge cases and error boundaries
* ✅ Test folders & naming conventions
* ✅ Organizing test suites (`describe`, `it`)
* ✅ Custom matchers

📚 Tools:

* `jest-extended` — for custom matchers
* `jest-mock-axios` — for API-heavy apps

---

### 🚢 PHASE 7: CI/CD Integration and Production Readiness

#### 🎯 Goal: Use Jest in real-world and team-based codebases.

* ✅ Run Jest in GitHub Actions
* ✅ Lint test code with ESLint rules
* ✅ Use `ts-jest` for TypeScript
* ✅ Common performance issues
* ✅ Real-world monorepo testing strategies

📚 Example GitHub Actions:

```yaml
- name: Run tests
  run: npm run test -- --ci
```

---

### 🚀 PHASE 8: Open Source & Contributions

#### 🎯 Goal: Contribute to OSS projects confidently.

* ✅ Reading existing Jest tests in open source projects
* ✅ Adding/improving test coverage
* ✅ Understanding test structure in large repos (e.g., Vite, React)
* ✅ Following code style and coverage reports

---

## 📦 Bonus Tools to Know

* `msw` – Mock Service Worker for mocking REST/GraphQL in tests
* `jest-dom` – Helpful DOM assertions
* `vitest` – Jest-compatible faster test runner (for Vite projects)

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

