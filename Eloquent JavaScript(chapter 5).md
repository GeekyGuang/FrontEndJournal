# Eloquent JavaScript(chapter 5)

## Higher-Order Functions
Functions that operate on other functions, either by taking them as arguments or by returning them, are called _higher-order functions_. 

we can have functions that create new functions.
```javascript
function greaterThan(n) {
  return m => m > n;
}
let greaterThan10 = greaterThan(10);
console.log(greaterThan10(11));
// → true
```
we can have functions that change other functions.
```javascript
function noisy(f) {
  return (...args) => {
    console.log("calling with", args);
    let result = f(...args);
    console.log("called with", args, ", returned", result);
    return result;
  };
}
noisy(Math.min)(3, 2, 1);
// → calling with [3, 2, 1]
// → called with [3, 2, 1] , returned 1
```
We can even write functions that provide new types of control flow.
```javascript
function unless(test, then) {
  if (!test) then();
}

repeat(3, n => {
  unless(n % 2 == 1, () => {
    console.log(n, "is even");
  });
});
// → 0 is even
// → 2 is even
```
### forEach
There is a built-in array method, **`forEach`**, that provides something like a `for`/`of` loop as a higher-order function.
```javascript
["A", "B"].forEach(l => console.log(l));
// → A
// → B
```
### filter
```javascript
function filter(array, test) {
  let passed = [];
  for (let element of array) {
    if (test(element)) {
      passed.push(element);
    }
  }
  return passed;
}

console.log(filter(SCRIPTS, script => script.living));   // script.living的值为true或false
// → [{name: "Adlam", …}, …]

console.log(SCRIPTS)
console.log(SCRIPTS.filter(s => s.direction == "ttb"));
```
### map
```javascript
let arr = [{name: "Adlam", age:1},
{name: "Caucasian Albanian", age:1},
{name: "Ahom",age:1},
{name: "Arabic", age:1}]

console.log(arr.map(item => item.name))
```
### reduce(归纳)
```javascript
function reduce(array, combine, start) {
  let current = start;
  for (let element of array) {
    current = combine(current, element);
  }
  return current;
}

console.log(reduce([1, 2, 3, 4], (a, b) => a + b, 0));
// → 10


// The method will take the first element of the array as its start value 
// and start reducing at the second element.
console.log([1, 2, 3, 4].reduce((a, b) => a + b));
// → 10
```
### some
```javascript
// 有一个符合条件就返回true，所有都不符合返回false
const array = [1, 2, 3, 4, 5];

// checks whether an element is even
const even = (element) => element % 2 === 0;

console.log(array.some(even));
// expected output: true
```
### codePointAt
```javascript
// Two emoji characters, horse and shoe
let horseShoe = "🐴👟";
console.log(horseShoe.length);
// → 4
console.log(horseShoe[0]);
// → (Invalid half-character)
console.log(horseShoe.charCodeAt(0));
// → 55357 (Code of the half-character)
console.log(horseShoe.codePointAt(0));
// → 128052 (Actual code for horse emoji)


let roseDragon = "🌹🐉";
for (let char of roseDragon) {
  console.log(char);
}
// → 🌹
// → 🐉
```
### findIndex
```javascript
const array1 = [5, 12, 8, 130, 44];

const isLargeNumber = (element) => element > 13;

console.log(array1.findIndex(isLargeNumber));   // 找不到返回-1
// expected output: 3
```
### Exercises
#### Flattening
```javascript
let arrays = [[1, 2, 3], [4, 5], [6]]
console.log(arrays.reduce((a,b) => a.concat(b)))
// → [1, 2, 3, 4, 5, 6]
```
#### Your own loop
```javascript
function loop(start, test, update, body) {
  for (let value = start; test(value); value = update(value)) {
    body(value);
  }
}

loop(3, n => n > 0, n => n - 1, console.log);
// → 3
// → 2
// → 1
```
#### Everything
```javascript
// 用for循环实现
function every(array, test) {
  for(let i of array) {
    if (!test(i)){
      return false
    }
  }
  
  return true
}


// 用some实现
function every(array, test) {
  return !array.some(element => !test(element))
}

console.log(every([1, 3, 5], n => n < 10));
// → true
console.log(every([2, 4, 16], n => n < 10));
// → false
console.log(every([], n => n < 10));
// → true
```
#### 


