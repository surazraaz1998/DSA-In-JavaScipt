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
A **zero-indexed ordered collection** that can store multiple data types. Key characteristics:
- Dynamic size (no fixed length)
- Type flexibility (can mix data types)
- Optimized for sequential access
- Underlying implementation: Specialized object
 
While arrays are objects, they have optimized memory allocation for sequential access. The `length` property is automatically maintained, but unlike traditional arrays, JavaScript arrays can have "holes" (empty slots) when using constructor initialization.


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
let arr2 = new Array(3);       // Creates array with 3 empty slots
let arr3 = new Array(1, 2, 3); // [1, 2, 3]
```

## Core Operations

### Add Elements
| Method                     | Description                  | Example                              | Time Complexity     |
|----------------------------|------------------------------|--------------------------------------|---------------------|
| `push(items)`              | Add to end                   | `arr.push(4)` → `[1,2,3,4]`          |  O(1)               |
| `unshift(items)`           | Add to start                 | `arr.unshift(0)` → `[0,1,2]`         |  O(n)               |
| `splice(start, 0, items)`  | Insert at position           | `arr.splice(1, 0, 'a')` → `[1,'a',2]`|  O(n)               |

### Remove Elements
| Method                 | Description                  | Example                                           |  Time Complexity |
|------------------------|------------------------------|---------------------------------------------------|------------------|
| `pop()`                | Remove from end              | `arr.pop()` → Removes last item                   |  O(1)            |
| `shift()`              | Remove from start            | `arr.shift()` → Removes first item                |  O(n)            |
| `splice(start, count)` | Remove items                 | `arr.splice(1, 2)` → Removes 2 items from index 1 |  O(n)            |

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

## Essential Methods Deep Dive
**1. slice() vs splice()**
. slice(): Creates new array (non-mutating)
```javascript
const arr = [1, 2, 3];
arr.slice(1, 3); // Returns [2, 3], original array remains [1, 2, 3]
```

.splice(): Modifies original array (mutating)
```javascript
arr.splice(1, 2); // Returns [2, 3], original becomes [1]
```
**2. reverse() Nuances**
```javascript
const arr = [1, 2, 3];
const reversed = arr.reverse(); 
// Both arr and reversed become [3, 2, 1] (mutates original)
```


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

**6. Maximum Subarray Sum (Kadane's Algorithm)**
```javascript
function maxSubArray(nums) {
  let maxCurrent = maxGlobal = nums[0];
  for(let i = 1; i < nums.length; i++) {
    maxCurrent = Math.max(nums[i], maxCurrent + nums[i]);
    maxGlobal = Math.max(maxGlobal, maxCurrent);
  }
  return maxGlobal;
}
```
**7. Find All Duplicates**
```javascript
function findDuplicates(nums) {
  const result = [];
  for(let i = 0; i < nums.length; i++) {
    const index = Math.abs(nums[i]) - 1;
    if(nums[index] < 0) result.push(index + 1);
    nums[index] = -nums[index];
  }
  return result;
}
```
**8. Merge Intervals**
```javascript
function merge(intervals) {
  if(!intervals.length) return [];
  intervals.sort((a, b) => a[0] - b[0]);
  const result = [intervals[0]];
  
  for(let [start, end] of intervals) {
    const lastEnd = result[result.length-1][1];
    if(start <= lastEnd) {
      result[result.length-1][1] = Math.max(end, lastEnd);
    } else {
      result.push([start, end]);
    }
  }
  return result;
}
```
## Output-Based Questions
**1. What does this code output?**
```javascript
const arr = [1, 2, 3];
arr[10] = 10;
console.log(arr.length); // 11
console.log(arr[5]);     // undefined
```
**2. Predict the output:**
```javascript
let arr = [1, 2, 3];
const result = arr.push(4).pop();
console.log(result); // TypeError: Cannot read property 'pop' of number
```
**3. What's logged here?**
```javascript
const arr = ['a', 'b'];
arr.splice(1, 0, 'c');
console.log(arr); // ['a', 'c', 'b']
```
**4. What's the final array?**
```javascript
const arr = [1, 2, 3, 4];
arr.slice(1, 3);
arr.splice(1, 3);
console.log(arr); // [1]
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
| 3Sum | Medium | [Problem](https://leetcode.com/problems/3sum/) | Two Pointers |
| Container With Most Water | Medium | [Problem](https://leetcode.com/problems/container-with-most-water/) | Greedy Algorithm |
| Subarray Sum Equals K | Medium | [Problem](https://leetcode.com/problems/subarray-sum-equals-k/) | Prefix Sum |
| Find Peak Element | Medium | [Problem](https://leetcode.com/problems/find-peak-element/) | Binary Search|
| Rotate Image | Medium | [Problem](https://leetcode.com/problems/rotate-image/) | Matrix Manipulation |

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
**Matrix Transpose**
```javascript
function transpose(matrix) {
  return matrix[0].map((_, i) => matrix.map(row => row[i]));
}

// Example:
const matrix = [
  [1, 2, 3],
  [4, 5, 6]
];
console.log(transpose(matrix)); 
// [[1,4], [2,5], [3,6]]
```
**Spiral Traversal**
```javascript
function spiralOrder(matrix) {
  const result = [];
  while(matrix.length) {
    result.push(...matrix.shift());
    for(const row of matrix) {
      if(row.length) result.push(row.pop());
    }
    matrix.reverse().forEach(row => row.reverse());
  }
  return result;
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

5. Avoid shift/unshift in loops - O(n) time complexity

**Happy Coding! 🚀*