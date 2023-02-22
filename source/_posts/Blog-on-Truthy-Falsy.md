---
title: Blog_on_Truthy_Falsy
date: 2023-02-22 16:26:24
tags:
---

# Truthy - Falsy

In Java Script we have primitive boolean values called true and false.
Java Script uses type conversion to treat any value as true or false when it is needed in the context like conditionals and loops.
So in boolean context like if or while the values will be considered as true or false, these values are devided into truthy and falsy values in Java Script.

## Falsy

Falsy is a value treated as false when it is in a boolean context.

List of values which are considered as falsy in Java Script are,

1. false
1. 0
1. -0
1. 0n
1. "", '', ``
1. null
1. undefined
1. NaN

#### Examples

```javascript
if (0) {
  console.log("false"); // this is not reachable
}

if (!null) {
  console.log("false"); // prints false
}

let x = Number("Alphabet");
// x = NaN (Not a Number)
while (x) {
  // not reachable
}

let x = null;
// type of x is object
while (x) {
  // not reachable
}
```

### For clear understanding of the boolean context

```javascript
let a = 0; // a is Number and it is a falsy value
let b = flase; // b is boolean

console.log(a); // prints 0 as it is in Number context
if (a) {
  console.log("true");
} else {
  console.log("false");
}
// prints false as it is in boolean context a is considered as false.
```

## Truthy

Truthy is a value treated as true when it is in a boolean context.

All the values which are not falsy are considered as truthy.

#### Examples

```javascript
if (1) {
  console.log("true"); // prints true
}

if ({}) {
  console.log("true"); // prints true
}
```

## Strict Situations

These are the situations where we need to check for only true and false values.
for example,

In a situation where you need to pass the conditions for 0 as it is a number.

```javascript
let a = 0;
if (a) {
  console.log("It is a number"); // this is not reachable
}

//In order to pass the condition we need to strictly evaluate a

let a = 0;
if (a !== false) {
  console.log("It is a number"); // Prints "It is a number" as a is not false.
}
```
