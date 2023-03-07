---
title: Blog-on-Sort
date: 2023-03-06 11:29:49
tags:
---

# SORT

In Java Script the sort method is used to sort the array elements. The default sort order is ascending, And it will return the reference to the same array.

Here it will convert the array elements into strings for sorting.

Let us see how we can use the sort function in different situations.

## Strings

In strings, we can see two different situations,

- All characters are in lowercase or uppercase
- String is mixed with upper case and lower case characters.

examples:

##### All characters are in lower case or upper case.

```javascript
let stringArray1 = ["apple", "mango", "jackfruit"]; // all lowercase
let stringArray2 = ["APPLE", "MANGO", "JACKFRUIT"]; // all upper case

console.log(stringArray1.sort()); //['apple', 'jackfruit', 'mango']
console.log(stringArray2.sort()); //['APPLE', 'JACKFRUIT', 'MANGO']
```

Here it will sort according to our expectation

##### String is mixed with upper case and lower case characters.

```javascript
let stringArray = ["apple", "Mango", "JackFruit"];
console.log(stringArray.sort()); // ['JackFruit', 'Mango', 'apple']
```

As we can see in this example we are not getting the result we expected, because the sort method will sort them by comparing their ASCII character order values.

We can solve this by converting them to lowercase or uppercase

```javascript
let stringArray = ["apple", "Mango", "JackFruit"];
console.log(
  stringArray.sort((fruit1, fruit2) => {
    fruit1InLower = fruit1.toLowerCase();
    fruit2InLower = fruit2.toLowerCase();
    if (fruit1InLower < fruit2InLower) {
      return -1;
    } else if (fruit1InLower > fruit2InLower) {
      return 1;
    } else {
      return 0;
    }
  })
); //  ['apple', 'JackFruit', 'Mango']
```

Here the sort function takes a compare function with two arguments, that define the sort order.
If we don't provide this function to specify the sort order it will sort the elements in ascending order by comparing their Unicode code point value.

If a compare function with arguments value1 and value2 returns a number,

- Greater than 0 sort value1 after value2
- Lesser than 0 sort value1 before value2
- Equal to 0 keep the original order

##### Different case strings

To sort the strings with non-ASCII characters, that is strings with languages other than English we can use the localeCompare() method.

The localeCompare() method compares two strings in the current locale. The current locale is based on the language settings of the browser. This enables case-insensitive sorting for an array.

We can use this method for the above problem also,

```javascript
let stringArray = ["apple", "Mango", "JackFruit"];
stringArray.sort((fruit1, fruit2) => {
  return fruit1.localeCompare(fruit2);
});
console.log(stringArray); // ['apple', 'JackFruit', 'Mango']
```

## Integers

The sort method will convert the integers into strings and sort them by comparing their ASCII character value

```javascript
let integerArray = [1, 10, 2, 3, 23];
console.log(integerArray.sort()); //[1, 10, 2, 23, 3]
```

To get the correct sorted values we can use compare function to specify the sorting method.

```javascript
let integerArray = [1, 10, 2, 3, 23];
console.log(
  integerArray.sort((num1, num2) => {
    return num1 - num2;
  })
); // [1, 2, 3, 10, 23]
```

##### Other examples on Integers

```javascript
let integerStringArray = ["1", "10", "2", "3", "23"];
let mixedIntegerArray = ["1", 10, "2", "3", 23];

console.log(
  integerStringArray.sort((num1, num2) => {
    return num1 - num2;
  }) // ['1', '2', '3', '10', '23']
);

console.log(
  mixedIntegerArray.sort((num1, num2) => {
    return num1 - num2;
  }) //['1', '2', '3', 10, 23]
);
```

## Floating point numbers

```javascript
let floatArray = [1.79, 10.3, 2.4, 2.5, 23.7];

console.log(floatArray.sort()); //  [1.79, 10.3, 2.4, 2.5, 23.7]
console.log(
  floatArray.sort((num1, num2) => {
    return num1 - num2;
  }) //  [1.79, 2.4, 2.5, 10.3, 23.7]
);
```

In the same way, as mentioned in an integer array, sort works the same for floating-point numbers.

## Objects

Examples on sorting an array of objects

```javascript
let objArray = [
  { name: "Akash", age: 22 },
  { name: "Bhagya", age: 27 },
  { name: "Anand", age: 21 },
];
// sort using the age property
objArray.sort((person1, person2) => {
  return person1.age - person2.age;
});
console.log(JSON.stringify(objArray));
//[{"name":"Anand","age":21},{"name":"Akash","age":22},{"name":"Bhagya","age":27}]

// sort using the name property
objArray.sort((person1, person2) => {
  return person1.name.localeCompare(person2.name);
});
console.log(JSON.stringify(objArray));
//[{"name":"Akash","age":22},{"name":"Anand","age":21},{"name":"Bhagya","age":27}]
```

##### Sorting Objects

Sorting values inside the Objects

```javascript
let objectToSort = {
  Akash: 20,
  Anand: 19,
  Bhagya: 27,
  Vinod: 23,
};

const sortedObj = Object.entries(objectToSort)
  .sort(([name1, age1], [name2, age2]) => {
    return age1 - age2;
  })
  .reduce((newObj, [name, age]) => {
    if (newObj[name] === undefined) {
      newObj[name] = [];
    }
    newObj[name] = age;
    return newObj;
  }, {});
console.log(JSON.stringify(sortedObj)); //{"Anand":19,"Akash":20,"Vinod":23,"Bhagya":27}
```

To sort the Object first we need to convert that into a sortable Array.
Here in this example object is converted to a sortable array by taking the entries from the object, we can also do this by taking keys.

```javascript
const sortedObj = Object.keys(objectToSort)
  .sort((key1, key2) => {
    return objectToSort[key1] - objectToSort[key2];
  })
  .reduce((newObj, key) => {
    return { ...newObj, [key]: objectToSort[key] }; //Using Object Destructing
  }, {});
```

##### Multiple keys in an object

Sorting an array of objects by taking multiple keys,

Here in this example we are sorting the objects based on the marks of the stidents and also by their names.

```javascript
let students = [
  {
    name: "Akash",
    Marks: 80,
  },
  {
    name: "Bhoomika",
    Marks: 90,
  },
  {
    name: "Anand",
    Marks: 90,
  },
];
students.sort((student1, student2) => {
  //Only if marks are same compare with names otherwise compare with marks
  if (student1.Marks === student2.Marks) {
    return student1.name.localeCompare(student2.name);
  } else {
    return student1.Marks - student2.Marks;
  }
});
console.log(JSON.stringify(students));
// [{"name":"Akash","Marks":80},{"name":"Anand","Marks":90},{"name":"Bhoomika","Marks":90}]
```

In this way, we can sort the different types of arrays and objects with the help of comparison functions.
