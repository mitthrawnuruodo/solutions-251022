# Solutions — Functional Programming (Part 1)
## Task 1 — Pure function: addTax(price)
```js
// A pure function: output depends only on input; no side effects.
const addTax = (price) => price * 1.25;

// Quick checks
console.log(addTax(100)); // 125
console.log(addTax(0));   // 0
```

## Task 2 — Immutability with objects
```js
const book = { title: "1984", author: "Orwell", year: 1949 };

// Create a NEW object (do not mutate 'book')
const updatedBook = { ...book, year: 1950 };

console.log(book.year);        // 1949 (unchanged)
console.log(updatedBook.year); // 1950 (new copy)
```

## Task 3 — First-class functions with applyDiscount(prices, fn)
```js
// Higher-order function: takes another function as a parameter.
const applyDiscount = (prices, fn) => prices.map(fn);

// Two different "strategy" functions
const tenPercent = (p) => p * 0.9;
const halfPrice  = (p) => p * 0.5;

// Demo
const prices = [100, 200, 300];
console.log(applyDiscount(prices, tenPercent)); // [90, 180, 270]
console.log(applyDiscount(prices, halfPrice));  // [50, 100, 150]
// Note: 'prices' remains unchanged (immutability of arrays via map)
```

## Task 4 — Function returning a function: makeGreeting(language)
```js
const makeGreeting = (language) => (name) => {
  if (language === "en") return `Hello, ${name}!`;
  if (language === "no") return `Hei, ${name}!`;
  if (language === "sv") return `Hej, ${name}!`;
  return `Hi, ${name}!`; // default fallback
};

// Demo
const greetEN = makeGreeting("en");
const greetNO = makeGreeting("no");
console.log(greetEN("Lasse")); // "Hello, Lasse!"
console.log(greetNO("Lasse")); // "Hei, Lasse!"
```

## Task 5 — Step Counter (closure with parameter)
```js
function createStepCounter(step) {
  let total = 0;                // private state
  return function () {          // closure over 'step' and 'total'
    total += step;
    return total;
  };
}

// Demo
const stepByTwo = createStepCounter(2);
console.log(stepByTwo()); // 2
console.log(stepByTwo()); // 4
console.log(stepByTwo()); // 6

const stepByFive = createStepCounter(5);
console.log(stepByFive()); // 5
console.log(stepByFive()); // 10
```

## Task 6 — Score Keeper (closure)
```js
function createScoreKeeper() {
  let score = 0; // private variable

  function add(points) {
    score += points;
  }

  function get() {
    return score;
  }

  // Return both functions so they share the same closure
  return { add, get };
}

// Demo
const player1 = createScoreKeeper();
const player2 = createScoreKeeper();

player1.add(10);
player1.add(5);
console.log(player1.get()); // 15

player2.add(7);
console.log(player2.get()); // 7
```

## Task 7 — Secret value (getter/setter via closure)
```js
function createSecret(initialValue) {
  let secret = initialValue;     // private
  const get = () => secret;      // reads from closure
  const set = (newValue) => {    // writes to closure
    secret = newValue;
  };
  return { get, set };
}

// Demo
const s = createSecret("hush");
console.log(s.get());   // "hush"
s.set("new secret");
console.log(s.get());   // "new secret"
```

## Task 8 — Bonus: makeLogger(prefix) (closure + higher-order)
```js
function makeLogger(prefix) {
  // Return a function that "remembers" the chosen prefix
  return function (message) {
    console.log(`${prefix}: ${message}`);
  };
}

// Demo
const warn = makeLogger("Warning");
const info = makeLogger("Info");
warn("Low battery");     // "Warning: Low battery"
info("Connected WiFi");  // "Info: Connected WiFi"
```