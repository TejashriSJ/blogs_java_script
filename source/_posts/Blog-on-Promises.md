---
title: Blog-on-Promises
date: 2023-03-14 12:01:13
tags:
---

# Promises

In JavaScript Promise is an object that represents the eventual completion or failure of an asynchronous operation and its resulting value.

Some of the important methods of promises are explained below.

- Promise.all
- Promise.allSettled
- Promise.any
- Promise.race

## Promise.all

This is a Promise method that takes an iterable object of promises as input and returns a single promise.

- This promise will be fulfilled when all of the input's promises are fulfilled, with an array of fulfillment values.
- This promise will reject when any one of the input's promises rejects, with the first rejection reason.

Example:

```javascript
let promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("promise 1");
  }, 1000);
});
let promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("promise 2");
  }, 3000);
});
let promise3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("promise 3");
  }, 1000);
});
```

Here 3 promises promise1, promise2, and promise3 are declared which contain respective promise objects.

```javascript
Promise.all([promise1, promise2, promise3])
  .then((promiseValues) => {
    console.log(promiseValues);
  })
  .catch((firstRejectMessage) => {
    console.error(firstRejectMessage);
  });
//Prints [ 'promise 1', 'promise 2', 'promise 3' ]
```

If we call Promise.all method with an array of our promise objects the Promise.all will return a promise object which will resolve when all of the input's promises are resolved.

This will resolve with an array of resolved values as we got in the above example.

In the same way, if any one of the input's promises rejects, the Promise.all method will return a promise object with the first error message.

```javascript
let promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject("promise 1");
  }, 1000);
});
let promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject("promise 2");
  }, 3000);
});
let promise3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("promise 3");
  }, 1000);
});

Promise.all([promise1, promise2, promise3])
  .then((promiseMessages) => {
    console.log(promiseMessages);
  })
  .catch((firstRejectMessage) => {
    console.error(firstRejectMessage);
  });

// Prints promise1
```

As we can see in the example, 2 promises are rejected but Promise.all will return the first reject message.

## Promise.allSettled

This method will take an iterable object of promises and returns a single Promise.

- This returned promise will be fulfilled when all of the input's promises settle(fulfill or reject).
- This will be fulfilled with an array of objects that describe the outcome of each promise.

Example:

```javascript
let promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Promise 1 Value");
  }, 2000);
});
let promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject("Promise 2 Rejected Reason");
  }, 3000);
});
Promise.allSettled([promise1, promise2]).then((promiseMessages) => {
  console.log(promiseMessages);
});
/* 
[
{ status: 'fulfilled', value: 'Promise 1 Value' },
{ status: 'rejected', reason: 'Promise 2 Rejected Reason' }
]*/
```

As we can see in this example Promise.allSettled method returns an object with the status of each promise.

The output order of promises will be the same as the order we passed to Promise.allSettled method.

This method is typically used when we have multiple asynchronous functions that are not dependent on one another and we want to know the result of each promise.

## Promise.any

This method takes an iterable object of promises as input and returns a single Promise.

- The returned promise will be fulfilled when any one of the input's promises is fulfilled.
- The returned promise will reject when all of the input's promises rejects, with an array of rejection reasons.

This is similar and opposite to Promise.all method.

Example:

```javascript
let promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Promise 1 Resolved");
  }, 2000);
});
let promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Promise 2 Resolved");
  }, 1000);
});
let promise3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject("promise 3 Rejected");
  }, 1000);
});

Promise.any([promise1, promise2, promise3])
  .then((promiseMessage) => {
    console.log(promiseMessage);
  })
  .catch((rejectMessages) => {
    console.error(rejectMessages);
  });
// Promise 2 Resolved
```

As we can see in this example the Promise.any method will be fulfilled as soon as promise 2 is resolved with the value "Promise 2 Resolved"

```javascript
let promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject("Promise 1 Rejected");
  }, 2000);
});
let promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject("Promise 2 Rejected");
  }, 3000);
});
let promise3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject("Promise 3 Rejected");
  }, 1000);
});
Promise.any([promise1, promise2, promise3])
  .then((promiseMessage) => {
    console.log(promiseMessage);
  })
  .catch((rejecteMessages) => {
    console.error(rejecteMessages);
  });
/*
[AggregateError: All promises were rejected] {
  [errors]: [ 'Promise 1 Rejected', 'Promise 2 Rejected', 'Promise 3 Rejected' ]
}
*/
```

If any of the promises is not get fulfilled then after all the input's promises are rejected the Promise.any will reject with an array of rejected reasons.

## Promise.race

This method will take an iterable object of promises and return a single promise.

- The returned promise will resolve with the message of the first promise that is settled as fulfilled from the given iterable object.
- The returned promise will reject with the message of the first promise that is settled as rejected from the given iterable object.

Example:

```javascript
let promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("promise 1");
  }, 4000);
});
let promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("promise 2");
  }, 3000);
});
let promise3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("promise 3");
  }, 1000);
});

Promise.race([promise1, promise2, promise3])
  .then((promiseMessage) => {
    console.log(promiseMessage);
  })
  .catch((rejectMessage) => {
    console.error(rejectMessage);
  });
// Prints promise 3
```

As we can see in this example promise 3 will settle first as it takes less time to execute when compared to other promises.

So the Promise.race method will return the resolved message from promise 3.

```javascript
let promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("promise 1");
  }, 4000);
});
let promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("promise 2");
  }, 3000);
});
let promise3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject("promise 3");
  }, 1000);
});

Promise.race([promise1, promise2, promise3])
  .then((promiseMessage) => {
    console.log(promiseMessage);
  })
  .catch((RejectMessage) => {
    console.log(RejectMessage);
  });
// Prints promise 3
```

In the same way, if the first promise which has been settled (promise 3 in this example) has been rejected, then the promise.race method will return the reject message from that promise.
