/* =====================================================================
   JAVASCRIPT BASICS GUIDE
   Run it with:  node js_basics_guide.js
   Each section = one MAIN TOPIC, with small sub-topics explained inside.
   ===================================================================== */

// Helper to print neat section titles in the console
const section = (title) => console.log(`\n===== ${title} =====`);


/* =====================================================================
   1. VARIABLES & DATA TYPES
   ===================================================================== */
section("1. Variables & Data Types");

// var   -> old way, function-scoped (avoid in modern code)
// let   -> block-scoped, value CAN change
// const -> block-scoped, value CANNOT be reassigned
let age = 25;            // number
const name = "Asha";     // string
let isStudent = true;    // boolean
let nothing = null;      // intentional "empty" value
let notSet;              // undefined (declared but no value)

age = 26;                // OK, because we used let
// name = "Ravi";        // ERROR: can't reassign a const

console.log(typeof age, typeof name, typeof isStudent, typeof nothing, typeof notSet);
// Note: typeof null is "object" (a famous JS quirk)

// Template literals: use backticks and ${} to embed values in a string
console.log(`${name} is ${age} years old.`);


/* =====================================================================
   2. OPERATORS
   ===================================================================== */
section("2. Operators");

console.log(10 + 3, 10 - 3, 10 * 3, 10 / 3, 10 % 3, 2 ** 3); // arithmetic
console.log(5 == "5");   // true  -> loose equality (converts types)
console.log(5 === "5");  // false -> strict equality (checks type too). PREFER ===
console.log(true && false, true || false, !true); // logical: AND, OR, NOT

// Nullish coalescing: use right side only if left is null/undefined
const username = null ?? "Guest";
console.log(username); // "Guest"

// Optional chaining: safely read deep properties without crashing
const user = { profile: { city: "Kolkata" } };
console.log(user.profile?.city);     // "Kolkata"
console.log(user.address?.street);   // undefined (no error!)


/* =====================================================================
   3. CONDITIONS (decision making)
   ===================================================================== */
section("3. Conditions");

const marks = 72;

// if / else if / else
if (marks >= 90) {
  console.log("Grade A");
} else if (marks >= 60) {
  console.log("Grade B");
} else {
  console.log("Grade C");
}

// Ternary: a short if/else in one line -> condition ? ifTrue : ifFalse
console.log(marks >= 40 ? "Pass" : "Fail");

// switch: good when comparing one value against many fixed options
const day = 3;
switch (day) {
  case 1: console.log("Monday"); break;   // break stops the fall-through
  case 3: console.log("Wednesday"); break;
  default: console.log("Other day");
}


/* =====================================================================
   4. LOOPS
   ===================================================================== */
section("4. Loops");

// Classic for loop: (start; condition; step)
for (let i = 1; i <= 3; i++) console.log("for:", i);

// while loop: runs as long as the condition is true
let count = 0;
while (count < 2) {
  console.log("while:", count);
  count++;
}

const fruits = ["apple", "banana", "mango"];

// for...of -> loops over VALUES of an array
for (const fruit of fruits) console.log("for...of:", fruit);

// for...in -> loops over KEYS of an object
const car = { brand: "Tata", year: 2022 };
for (const key in car) console.log("for...in:", key, "=", car[key]);


/* =====================================================================
   5. FUNCTIONS
   ===================================================================== */
section("5. Functions");

// Function declaration (hoisted: can be called before it is defined)
function add(a, b) {
  return a + b;
}

// Function expression (stored in a variable)
const multiply = function (a, b) {
  return a * b;
};

// Arrow function: shorter syntax, very common in modern JS
const square = (n) => n * n;

// Default parameter: used when no argument is passed
const greet = (person = "friend") => `Hello, ${person}!`;

// Rest parameter: collects all extra arguments into an array
const sumAll = (...numbers) => numbers.reduce((total, n) => total + n, 0);

console.log(add(2, 3), multiply(2, 3), square(4));
console.log(greet(), greet("Asha"));
console.log(sumAll(1, 2, 3, 4));


/* =====================================================================
   6. ARRAYS & ARRAY METHODS
   ===================================================================== */
section("6. Arrays");

const nums = [1, 2, 3, 4, 5];

nums.push(6);      // add to the end
nums.pop();        // remove from the end
console.log(nums.length, nums[0]); // size and first item

// map    -> transforms every item, returns a NEW array
console.log(nums.map((n) => n * 2));
// filter -> keeps items that pass a test
console.log(nums.filter((n) => n % 2 === 0));
// reduce -> boils the array down to a single value
console.log(nums.reduce((sum, n) => sum + n, 0));
// find   -> first item that matches
console.log(nums.find((n) => n > 3));
// includes -> does the array contain this value?
console.log(nums.includes(3));


/* =====================================================================
   7. OBJECTS
   ===================================================================== */
section("7. Objects");

const person = {
  name: "Ravi",
  age: 30,
  // A function inside an object is called a method
  introduce() {
    return `Hi, I'm ${this.name}`; // "this" refers to the object itself
  },
};

console.log(person.name, person["age"]); // dot notation and bracket notation
console.log(person.introduce());

person.city = "Delhi";   // add a new property
delete person.age;       // remove a property
console.log(Object.keys(person));    // list of keys
console.log(Object.values(person));  // list of values


/* =====================================================================
   8. DESTRUCTURING, SPREAD & REST
   ===================================================================== */
section("8. Destructuring & Spread");

// Destructuring: pull values out of arrays/objects into variables
const [first, second] = ["a", "b", "c"];
const { brand, year } = car;
console.log(first, second, brand, year);

// Spread (...): copies/expands items
const arr1 = [1, 2];
const arr2 = [...arr1, 3, 4];                 // [1, 2, 3, 4]
const updatedCar = { ...car, year: 2024 };    // copy object, change one field
console.log(arr2, updatedCar);


/* =====================================================================
   9. SCOPE & CLOSURES
   ===================================================================== */
section("9. Scope & Closures");

// Scope = where a variable can be accessed
const globalVar = "I am global";
function showScope() {
  const localVar = "I am local";   // only visible inside this function
  console.log(globalVar, "|", localVar);
}
showScope();

// Closure: an inner function "remembers" variables of its outer function
function makeCounter() {
  let count = 0;                   // private variable
  return function () {
    count++;
    return count;
  };
}
const counter = makeCounter();
console.log(counter(), counter(), counter()); // 1 2 3


/* =====================================================================
   10. CLASSES (Object-Oriented Programming)
   ===================================================================== */
section("10. Classes");

class Animal {
  constructor(name) {      // runs when you create an object with "new"
    this.name = name;
  }
  speak() {
    return `${this.name} makes a sound.`;
  }
}

// Inheritance: Dog gets everything from Animal and can override it
class Dog extends Animal {
  speak() {
    return `${this.name} barks!`;
  }
}

console.log(new Animal("Generic").speak());
console.log(new Dog("Bruno").speak());


/* =====================================================================
   11. ERROR HANDLING
   ===================================================================== */
section("11. Error Handling");

function divide(a, b) {
  if (b === 0) throw new Error("Cannot divide by zero"); // create an error
  return a / b;
}

try {
  console.log(divide(10, 2));
  console.log(divide(5, 0));   // this throws, so we jump to catch
} catch (error) {
  console.log("Caught:", error.message);
} finally {
  console.log("finally always runs");  // good for cleanup
}


/* =====================================================================
   12. ASYNCHRONOUS JS (Callbacks, Promises, async/await)
   JS runs one thing at a time, but can "wait" for slow tasks
   (network, timers, files) without freezing everything.
   ===================================================================== */

// A Promise represents a value that will arrive LATER.
// It can be: pending -> fulfilled (resolve) or rejected (reject)
const wait = (ms, value) =>
  new Promise((resolve) => setTimeout(() => resolve(value), ms));

// async/await: write asynchronous code that reads like normal code
async function runAsyncDemo() {
  section("12. Async / Await");
  console.log("Start");

  const result = await wait(500, "Data loaded");  // pauses here, not the whole app
  console.log(result);

  // Promise.all: run several tasks at the same time and wait for all
  const [a, b] = await Promise.all([wait(300, "A done"), wait(200, "B done")]);
  console.log(a, "&", b);

  // Errors in async code are handled with try/catch too
  try {
    await Promise.reject(new Error("Network failed"));
  } catch (err) {
    console.log("Caught async error:", err.message);
  }

  console.log("End");
}

console.log("\n(Sync code above finishes first; async demo runs after.)");
runAsyncDemo();


/* =====================================================================
   QUICK SUMMARY
   - Use const by default, let when value changes, avoid var.
   - Use === instead of ==.
   - Prefer arrow functions + map/filter/reduce for arrays.
   - Use destructuring & spread to write shorter code.
   - Use async/await for anything that takes time.
   ===================================================================== */
