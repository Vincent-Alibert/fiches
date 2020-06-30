---
title: Question js
---

# Array Sort Comparison

Consider the following arrays. What gets logged in various sorting conditions?

```javascript
const arr1 = ["a", "b", "c"];
const arr2 = ["b", "c", "a"];

console.log(
  arr1.sort() === arr1,
  arr2.sort() == arr2,
  arr1.sort() === arr2.sort()
);
```

Select one:

- a/ true true true
- b/ true true false
- c/ false false false
- d/ true false true

# Array sort and clear

Consider the following array. How to sort it without there being 2 times the same value ?

```javascript
const arr1 = [1, 2, 3, 5, 4, 4, 7, 8, 9, 5, 8, 0];
```

# Prototypal Inheritance

In this question, we have a Dog constructor function. Our dog obviously knows the speak command. What gets logged in the following example when we ask Pogo to speak?

```javascript
function Dog(name) {
  this.name = name;
  this.speak = function() {
    return "woof";
  };
}

const dog = new Dog("Pogo");

Dog.prototype.speak = function() {
  return "arf";
};

console.log(dog.speak());
```

Select one:

- a/ woof
- b/ arf

# Promise.all Resolve Order

In this question, we have a timer function that returns a Promise that resolves after a random amount of time. We use Promise.all to resolve an array of timers. What gets logged?

```javascript
const timer = a => {
  return new Promise(res =>
    setTimeout(() => {
      res(a);
    }, Math.random() * 100)
  );
};

const all = Promise.all([timer("first"), timer("second")]).then(data =>
  console.log(data)
);
```

Select one:

- a/["first", "second"]
- b/It is random

# Reduce Math

Math time! What gets logged?

```javascript
const arr = [x => x * 1, x => x * 2, x => x * 3, x => x * 4];

console.log(arr.reduce((agg, el) => agg + el(agg), 1));
```

Select one:

- a/ 1
- b/ 60
- c/ 100
- d/ 120

# Short-Circuit Notification(s)

Let's display some notifications to our user! What gets logged in the following snippet?

```javascript
const notifications = 1;

console.log(
  `You have ${notifications} notification${notifications !== 1 && "s"}`
);
```

Select one:

- a/ You have 1 notification
- b/ You have 1 notifications \* c/ Something else

# IIFE, HOF, or Both

Does the following snippet illustrate an Immediately-Invoked Function Expression (IIFE), a Higher-Order Function (HOF), both, or neither?

```javascript
((fn, val) => {
  return fn(val);
})(console.log, 5);
```

Select one:

- a/ IIFE only
- b/ HOF only
- c/ Both IIFE and HOF
- d/ Neither

# Function Function Syntax

Let's say myFunc is a function, val1 is a variable, and val2 is a variable. Is the following syntax allowed in JavaScript?

```javascript
myFunc(val1)(val2);
```

Select one:

- a/ Yes
- b/ No

# Greatest Number in an Array

Will the following function always return the greatest number in an array?

```javascript
function greatestNumberInArray(arr) {
  let greatest = 0;
  for (let i = 0; i < arr.length; i++) {
    if (greatest < arr[i]) {
      greatest = arr[i];
    }
  }
  return greatest;
}
```

Select one:

- a/ Yes
- b/ No

# Hoisting

What is hoisting in js ?

# Closure

What is closure in js ?

# React test1

Consider the following code. What will be the return ?

```javascript
class Table extends React.Component {
  render() {
    return (
      <table>
        <tr>
          <Columns />
        </tr>
      </table>
    );
  }
}

class Columns extends React.Component {
  render() {
    return (
        <td>Hello</td>
        <td>World</td>
    );
  }
}

```

Select one:

- a/ HTML table
- b/ Error
- c/ Something else
