# JavaScript Arrays: Ultimate Guide

A complete guide to mastering arrays in JavaScript. Includes fundamentals, methods, practice problems, and LeetCode exercises.

---

## Table of Contents
- [What is a JavaScript Array?](#what-is-a-javascript-array)
- [Creating Arrays](#creating-arrays)
- [Core Operations](#core-operations)
  - [Add Elements](#add-elements)
  - [Remove Elements](#remove-elements)
  - [Access Elements](#access-elements)
  - [Iteration Methods](#iteration-methods)
- [Essential Methods](#essential-methods)
- [Practice Problems](#practice-problems)
- [LeetCode Exercises](#leetcode-exercises)
- [Multi-dimensional Arrays](#multi-dimensional-arrays)
- [Arrays vs Objects](#arrays-vs-objects)
- [Conclusion](#conclusion)

---

## What is a JavaScript Array?
A **zero-indexed ordered collection** that can store multiple data types. Unlike traditional arrays:
- Dynamic size (no fixed length)
- Can mix data types
- Optimized for sequential access

**Example:**
```javascript
let mixedArr = [42, 'apple', true, {id: 1}, [1, 2]];

```
## Creating Arrays
**1. Literal Syntax (Recommended):** 
```javascript
let empty = [];
let fruits = ['apple', 'banana'];
```

**2. Constructor Syntax:** 
```javascript
let arr1 = new Array();        // []
let arr2 = new Array(3);       // [empty × 3]
let arr3 = new Array(1, 2, 3); // [1, 2, 3]
```

## Core Operations

### Add Elements
| Method               | Description                  | Example                          |
|----------------------|------------------------------|----------------------------------|
| `push(items)`        | Add to end                   | `arr.push(4)` → `[1,2,3,4]`     |
| `unshift(items)`     | Add to start                 | `arr.unshift(0)` → `[0,1,2]`    |
| `splice(start, 0, items)` | Insert at position    | `arr.splice(1, 0, 'a')` → `[1,'a',2]` |

### Remove Elements
| Method               | Description                  | Example                          |
|----------------------|------------------------------|----------------------------------|
| `pop()`              | Remove from end              | `arr.pop()` → Removes last item  |
| `shift()`            | Remove from start            | `arr.shift()` → Removes first item |
| `splice(start, count)` | Remove items              | `arr.splice(1, 2)` → Removes 2 items from index 1 |

### Access Elements
```javascript
let first = arr[0];                // First element
let last = arr[arr.length - 1];    // Last element
console.log(arr[5]);               // undefined (if index doesn't exist)
```

### Iteration Methods

**1. Classic For Loop:**
```javascript
for(let i=0; i<arr.length; i++) {
  console.log(arr[i]);
}
```
**2. forEach:**
```javascript
arr.forEach((item, index) => {
  console.log(index, item);
});
```
**3. for...of:**
```javascript
for(const item of arr) {
  console.log(item);
}
```

## Essential Methods

| Method               | Description                          | Example                          |
|----------------------|--------------------------------------|----------------------------------|
| `slice(start, end)`  | Copy subarray (non-mutating)         | `arr.slice(1, 3)`               |
| `concat(arr2)`       | Merge arrays                         | `arr1.concat(arr2)`             |
| `indexOf(item)`      | Find first occurrence index          | `arr.indexOf('a')`              |
| `includes(item)`     | Check existence (ES6+)               | `arr.includes(5)`               |
| `join(separator)`    | Convert to string                    | `arr.join('-')` → "1-2-3"       |
| `reverse()`          | Reverse array (mutates)              | `arr.reverse()`                 |

## Practice Problems
**1. Reverse Array (In-place)**
```javascript
function reverseArray(arr) {
  let left = 0, right = arr.length - 1;
  while(left < right) {
    [arr[left], arr[right]] = [arr[right], arr[left]];  //swaping two numbers in javascript using destructuring 
    left++;
    right--;
  }
  return arr;
}
```
**2. Find Max/Min in Array**
```javascript
function findMaxMin(arr) {
  if(arr.length === 0) return null;
  let max = min = arr[0];
  for(let num of arr) {
    if(num > max) max = num;
    if(num < min) min = num;
  }
  return {max, min};
}
```

**3. Remove Duplicates (Sorted)**
```javascript
function removeDuplicates(arr) {
  if(arr.length === 0) return 0;
  let writeIndex = 0;
  for(let i=1; i<arr.length; i++) {
    if(arr[i] !== arr[writeIndex]) {
      arr[++writeIndex] = arr[i];
    }
  }
  return writeIndex + 1;
}
```
**4. Two Sum (Optimized using map)**
```javascript
function twoSum(nums, target) {
  const map = new Map();
  for(let i=0; i<nums.length; i++) {
    const complement = target - nums[i];
    if(map.has(complement)) {
      return [map.get(complement), i];
    }
    map.set(nums[i], i);
  }
  return [];
}
```

**5. Rotate Array**
```javascript
function rotateArray(arr, k) {
  k = k % arr.length;
  const removed = arr.splice(arr.length - k);
  arr.unshift(...removed);
  return arr;
}
```
## LeetCode Exercises

| Problem | Difficulty | Link | Key Concept |
|---------|------------|------|-------------|
| Two Sum | Easy | [Problem](https://leetcode.com/problems/two-sum/) | Hash Maps |
| Best Time to Buy Stock | Easy | [Problem](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) | Single Pass |
| Remove Duplicates | Easy | [Problem](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) | Two Pointers |
| Rotate Array | Medium | [Problem](https://leetcode.com/problems/rotate-array/) | Array Rotation |
| Contains Duplicate | Easy | [Problem](https://leetcode.com/problems/contains-duplicate/) | Set/Hash |
| Product of Array Except Self | Medium | [Problem](https://leetcode.com/problems/product-of-array-except-self/) | Prefix/Suffix |


## Multi-dimensional Arrays
**Arrays containing other arrays:**
```javascript
// 2D Array (Matrix)
let matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

// Access element
console.log(matrix[1][2]); // 6

// Nested iteration
for(let row of matrix) {
  for(let num of row) {
    console.log(num);
  }
}
```
## Arrays vs Objects

| Feature              | Arrays                               | Objects                          |
|----------------------|--------------------------------------|----------------------------------|
| Ordering             | Index-based order                    | No guaranteed order              |
| Access               | Numeric indices                      | String/Symbol keys               |
| Use Case             |Sequential data                       | Key-value pairs                  |
| Performance          | Faster iteration                     | Faster key lookups               |

## Check Array Type:
```javascript
console.log(Array.isArray([1,2])); // true
console.log(Array.isArray({}));    // false
```
## Conclusion
1. Arrays are versatile for storing ordered collections

2. Core methods: push/pop, shift/unshift, splice, slice

3. Common patterns: two pointers, sliding window

4. Arrays for sequential data, objects for key-value pairs

**Happy Coding! 🚀*