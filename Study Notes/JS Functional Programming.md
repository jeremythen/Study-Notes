Functional Programming tries to bring up the precession of mathematical functions in programming.

In FP, functions are completely separate from the data they work on.
In OOP, functions (methods) are part of the data (objects) the work on.

FP supports First-Class Functions.
FP functions should be pure.

With FP, you can create a validation function, like a middleware, so you wrap the target function with it and create a new function:

```javascript
const divide = (a, b) => a / 0;

const secondArgumentIsNotZero = (func) => (...args) => {
  if (args[1] == 0) {
    console.log("Error: dividing by zero");
    return null;
  }

  return func(...args);
};

const deviceSafe = secondArgumentIsNotZero(divide);

console.log(deviceSafe(7, 0));
```

# Functional programming is Declarative. OOP is Imperative.

## Imperative: How

- Set x equal to zero
- Add the first number in the array to x
- Repeat step 2 for the rest of the numbers in the array
- Device x by the length of the array

## Declarative: What

- X is the sum of all the numbers in the array, divided by the length of the array

# Core concepts of Functional Programming

1. Immutability

The value of a variable should not change.

```javascript
const x = 5;
```

x = 3 -> x is 3. Like in mathematics.

If you need to update the fields of an object, copy it with the new value to leave the old one intact.

2. Separating functions and data
3. First-class functions

## Ensuring immutability with ESLint

> npm install --save-dev eslint
> npx eslint --init # and select Use a popular style guide, Airbnb, etc.
> npm install eslint-plugin-immutable

In eslintrc.js

```javascript

{
    plugins: [
        'immutable',
    ],
    rules: {
        'immutable/no-mutation': 2, // 2 means it will treat mutations like an error, not a warning (1)
    }
}


```

# Partial Application and Currying

When we have a function with a list of arguments, and you fix one of those arguments to a value, like currying.

```javascript
const add = (x, y, z) => x + y + z;

const addPartial = (x, y) => (z) => add(x, y, z);

const add5And6 = addPartial(5, 6);

const sum = add5And6(7);

// or

addPartial(5, 6)(7);
```

# Recursion
