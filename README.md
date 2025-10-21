
# Lesson Tasks - Functional Programming (Part 1)

## Part A — Functional Thinking (basics)

### Task 1 — Pure Function
Write a function `addTax(price)` that adds 25% tax to a price.
Make sure it **doesn’t change the original value**, and only **returns** the new one.

Hint: Use `return price * 1.25;` and test with different prices.

### Task 2 — Immutability
You have this object:
```js
const book = { title: "1984", author: "Orwell", year: 1949 };
```
Create a new object called `updatedBook` where the year is set to 1950,
**without changing the original object**.

Hint: Use the **spread operator** (`{ ...book, year: 1950 }`).

### Task 3 — First-Class Functions
Write a function `applyDiscount(prices, fn)` that takes:
* an array of prices, and
* a function `fn` to apply to each price.

Then call it with two different functions:
* `tenPercent` (returns price × 0.9)
* `halfPrice` (returns price × 0.5)

Hint: Use `map()` to apply the function to all elements.

### Task 4 — Function Returning Function
Write a function `makeGreeting(language)` that returns another function which takes a `name` and returns a greeting.

Example expected behavior:
```js
const englishGreeting = makeGreeting("en");
console.log(englishGreeting("Lasse")); // "Hello, Lasse!"

const norwegianGreeting = makeGreeting("no");
console.log(norwegianGreeting("Lasse")); // "Hei, Lasse!"
```

Hint: Inside `makeGreeting`, return a function that checks the language and returns the correct text.

## Part B — Working with Closures

### Task 5 — Step Counter (closure variant)
Make a function `createStepCounter(step)` that remembers a step size.
Each time you call it, it should increase the total by that step.

Example:
```js
const stepByTwo = createStepCounter(2);
console.log(stepByTwo()); // 2
console.log(stepByTwo()); // 4
console.log(stepByTwo()); // 6
```

Hint: Similar to Basic Example from Closures, but your outer function should take `step` as a parameter and add it each time.

### Task 6 — Score Keeper (closure)

Create a function `createScoreKeeper()` that returns two functions:
* `add(points)` → adds points to the score
* `get()` → returns the current score

Each “score keeper” should remember its own total independently:
```js
const player1 = createScoreKeeper();
const player2 = createScoreKeeper();

player1.add(10);
player1.add(5);
console.log(player1.get()); // 15

player2.add(7);
console.log(player2.get()); // 7
```

(No need for classes or global variables — the functions should remember their score.)

Hint: Use a variable like `let score = 0`; inside the outer function, and return an object with two inner functions that share that variable. 

### Task 7 — Secret Value (closure with private data)
Write a function `createSecret(initialValue)` that returns two functions:
* get() → returns the secret
* set(newValue) → changes the secret

Example usage:
```js
const secret = createSecret("hush");
console.log(secret.get()); // "hush"
secret.set("new secret");
console.log(secret.get()); // "new secret"
```

Hint: Return an object with `{ get, set }` methods that both use the same `secret` variable from the outer scope.

### Task 8 — Bonus Challenge (closure + higher-order)
Create a function `makeLogger(prefix)` that returns a function which logs messages with a prefix.
```js
const warn = makeLogger("Warning");
warn("Low battery"); // "Warning: Low battery"
```
Then create another logger with `"Info"` and try it out.