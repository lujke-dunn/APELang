# APELang Interpreter

An interpreter of the Monkey and Lox programming language.

## About APELang

APELang is a programming language designed for learning about interpreter design. This implementation follows the references below with some custom enhancements, and different design choices.

### Key Features

- C-like syntax
- Variable bindings with `let` statements
- Integer, boolean, and string data types
- Arrays and hash maps (dictionaries)
- First-class and higher-order functions
- Closures
- Built-in functions
- Custom array methods (map, filter, reduce)
- Custom random number generator


## Usage

Run the REPL (Read-Eval-Print-Loop) to interactively use the APE language:

```bash
./APELang
```

## Language Examples

### Variables and Basic Types

```
// Define variables
let age = 25;
let name = "Monkey";
let isActive = true;

// Expressions
let sum = 10 + 15;
```

### Functions

```
// Define a function
let add = fn(a, b) {
  return a + b;
};

// Call a function
let result = add(1, 2);

// Higher-order functions
let twice = fn(f, x) {
  return f(f(x));
};
```

### Arrays

```
// Create an array
let arr = [1, 2, 3, 4, 5];

// Access elements
let first = arr[0];

// Built-in array functions
let head = first(arr);  // 1
let tail = rest(arr);   // [2, 3, 4, 5]
let last_item = last(arr);  // 5

// Array methods
let doubled = arr.map(fn(x) { x * 2 });  // [2, 4, 6, 8, 10]
let evens = arr.filter(fn(x) { x % 2 == 0 });  // [2, 4]
let sum = arr.reduce(fn(acc, x) { acc + x }, 0);  // 15
```

### Hash Maps

```
// Create a hash map
let person = {
  "name": "Monkey",
  "age": 5,
  "hobbies": ["coding", "eating bananas"]
};

// Access hash map values
let personName = person["name"];  // "Monkey"
```

### Conditionals

```
// If-else statements
if (5 > 3) {
  return "greater";
} else {
  return "less";
}
```

## Built-in Functions

The interpreter includes several built-in functions:

- `len(str)` - Returns the length of a string
- `first(array)` - Returns the first element of an array
- `last(array)` - Returns the last element of an array
- `rest(array)` - Returns all elements except the first one
- `push(array, item)` - Adds an item to the end of an array
- `puts(args...)` - Prints the arguments to the console
- `random(max)` - Returns a random integer between 0 and max-1. This is a custom extension not in the original book.

## Custom Extensions

This implementation includes several extensions not found in the original book:

### Random Number Generator

The `random` function provides a way to generate random integers:

```
// Generate a random number between 0 and 9
let rand = random(10);

// Generate a random dice roll (1-6)
let diceRoll = random(6) + 1;

// Error handling
random(0);    // Error: argument to `random` must be a positive integer
random(-10);  // Error: argument to `random` must be a positive integer
random("10"); // Error: argument to `random` not supported, got=STRING
```

### Custom Array Methods

- `array.map(fn)` - Returns a new array with each element transformed by the function
- `array.filter(fn)` - Returns a new array with elements that pass a test function
- `array.reduce(fn, initialValue)` - Reduces an array to a single value using a function

## Project Structure

```
src/APE/
├── ast/       - Abstract Syntax Tree definitions
├── evaluator/ - Execution engine
├── lexer/     - Tokenizer
├── object/    - Runtime object system
├── parser/    - Parser that builds AST
├── repl/      - Read-Eval-Print Loop
├── token/     - Token definitions
└── main.go    - Entry point
```

## Interpreter Implementation Details

The interpreter follows the design described in "Writing An Interpreter In Go" and Crafting Interpreters By Robert Nystrom includes:

- A lexer that transforms source code into tokens
- A recursive descent parser that creates an Abstract Syntax Tree (AST)
- An evaluator that executes the AST using a tree-walking approach
- A REPL (Read-Eval-Print-Loop) for interactive code testing

## Acknowledgments

This implementation is based on the resources in the following books:
- ["Crafting Interpreters"](craftinginterpreters.com)
- ["Writing An Interpreter In Go"](https://interpreterbook.com/)
- Dragon Book (Compilers principles techniques and tools)
