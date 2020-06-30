#Array Sort Comparison
Response : b

There are a couple concepts at play here. First, the array sort method sorts your original array and also returns a reference to that array. This means that when you write arr2.sort(), the arr2 array object is sorted.

It turns out, however, the sort order of the array doesn't matter when you're comparing objects. Since arr1.sort() and arr1 point to the same object in memory, the first equality test returns true. This holds true for the second comparison as well: arr2.sort() and arr2 point to the same object in memory.

In the third test, the sort order of arr1.sort() and arr2.sort() are the same; however, they still point to different objects in memory. Therefore, the third test evaluates to false.

#Array sort and clear
Solution : `Array.from(new Set(arr1)).sort()` or `[...new Set(arr1)].sort()`

Use Set is the good way for store unique values. Array.from() create an array and the method sort(), allow sort it

#Prototypal Inheritance
Response : a

Every time we create a new Dog instance, we set the speak property and that return string woof. we never use the prototypal speak property on Dog that returns the arf string.

#Promise.all Resolve Order
Response : a

The order in which the Promises resolve does not matter to Promise.all.

#Reduce Math
Response : d

1 + 1 _ 1 = 2
2 + 2 _ 2 = 6
6 + 6 _ 3 = 24
24 + 24 _ 4 = 120

So, 120 it is!

#Short-Circuit Notification(s)
Response : c

If we want our snippet to work correctly, we could consider a ternary operator. Because template string the result of test

#IIFE, HOF, or Both
Response : c

The snippet clearly illustates an IIFE as we immediately invoke a function by passing console.log and 5 to it. Additionally, we find that this is a HOF as fn is a function, and a HOF is defined as any function that takes another function as a parameter or returns a function.

#Function Function Syntax
Response : a

This is a common pattern for a higher-order function. If myFunc(val1) returns a function, then that function will be called with val2 as an argument.

#Greatest Number in an Array
Response : b

if all values are below 0, it s not the greater who are return but greatest

#Hoisting

#Closure

#React test1
Response : b

React can't return multi childs. Use React.fragment in Columns component
