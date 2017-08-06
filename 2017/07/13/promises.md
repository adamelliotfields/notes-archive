# Promises

```javascript
// Create a new promise using the Promise constructor
const firstPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('First promise resolved');
    // reject('First promise rejected');
  }, Math.random() * 3000);
});

// Resolve code runs in the then block
firstPromise.then((success) => {
  console.log(success);
// Reject code runs in the catch block
}).catch((error) => {
  console.log(error);
});

// Create a second promise
const secondPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Second promise resolved');
    // reject('Second promise rejected');
  }, Math.random() * 3000);
});

secondPromise.then((success) => {
  console.log(success);
}).catch((error) => {
  console.log(error);
});

// Create a third promise that only rejects
const thirdPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('Third promise rejected');
  }, Math.random() * 3000);
});

// And one more that only resolves
const fourthPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Fourth promise rejected');    
  }, Math.random() * 3000);
});

// Pass array of promises to Promise.all
// The then block only runs after all promises have been resolved
// If any promise rejects, the catch block runs
Promise.all([thirdPromise, fourthPromise]).then(() => {
  console.log('Promises resolved');
}).catch((error) => {
  // This will be the error message from the promise that rejected
  console.log(error);
});

// Create a function that returns a promise
const promiseAdd = (a, b) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (typeof a === 'number' && typeof b === 'number') {
        resolve(a + b);
      } else {
        reject('Arguments must be numbers');
      }
    }, Math.random() * 3000);
  });
}

promiseAdd(2, 2).then((success) => {
  console.log(success);
}).catch((error) => {
  console.log(error);
});

// Node async/await example
(async function () {
  try {
    const sum = await promiseAdd(3, 3);
    console.log(sum);
  } catch (error) {
    console.log(error);
  }
}());

// Node util.promisify example
const fs = require('fs');
const path = require('path');
const { promisify } = require('util');

const readdir = promisify(fs.readdir);

(async function () {
  try {
    const results = await readdir('./');
    results.forEach(result => {
      // Only log files with an extension
      if (path.extname(result)) console.log(result);
    });
  } catch (error) {
    console.error(error.message);
  }
}());
```
