---
title: Blog-on-call-by-value-call-by-reference
date: 2023-03-01 17:38:36
tags:
---

# Call-by-Value and Call-by-Reference

Based on the arguments passed to a function we can classify the function call as call by value or call by reference.

## Call by Value :

While calling a function if we pass the value as an argument we can call that function call as a call by value.

In this case, the original value of the argument passed will not be affected by any of the changes made to it in the called function.

Here we are just passing the value to the function and that function will make a copy of the argument we passed in a separate memory location so the original value will not be affected.

example:

```javascript
function callByValue(value) {
  value += 1; // Incrementing value by 1
  console.log(value); // prints 11
}
let value = 10;
callByValue(value);
console.log(value); // prints 10
```

As we can see in this example we are passing an argument (value) to callByValue function, the function is making an extra copy of the argument passed in a variable called 'value' in a separate memory location.

So the value outside the function is not changed.

In Java Script the primitive data types like Numbers, strings, boolean, etc will be passed by value.

## Call by Reference:

While calling a function if we pass the reference to the value as an argument we can call that function call as a call by Reference.

In this case, the original value of the argument passed will be changed by any of the changes made to it in the called function.

Here we are passing the reference to the variable as an argument so the function which is called will store the reference to that argument passed in a separate variable. But any changes made with that variable will also reflect in the original value.

It is just two references to the same value in a memory location.

examples:

```javascript
function callByReference(valueObjReference) {
  value["position"] = "inside function";
  console.log(valueObjReference); // prints {position : inside funnction}
}
let valueObj = { position: "outside function" };
console.log(valueObj); // prints {position : outside funnction}
callByReference(valueObj);
console.log(valueObj); // prints {position : inside funnction}
```

As we can see in this example we are passing the variable valueObj as an argument to the callByReference function. The function is creating another reference to the argument passed in a variable called valueObjReference .

Any changes made using this variable will also affect the original. So the value of the variable outside the function is changed.

In the same way for arrays

```javascript
let array = [1, 2, 3, 4];
function arrayCallByReference(array) {
  array[0] = 10;
  console.log(array); // prints [10,2,3,4]
}
// before calling function
console.log(array); // prints [1,2,3,4]
arrayCallByReference(array);
// after calling function
console.log(array); //prints [10,2,3,4]
```

In this example also we are passing an array to the function, the function is storing the address of the array so any changes made using that variable will make changes in the original array also.

In Java Script the non-primitive data types like array and object will be passed by reference.

In conclusion, we can say that call by value and call by reference are two different ways of passing arguments to functions in JavaScript. Call by value passes a copy of the variable value to the function, while call by reference passes a reference to the variable.
