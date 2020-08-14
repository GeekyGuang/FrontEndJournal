# Eloquent JavaScript(chapter 4)

### properties
"xxx".length


属性名都是字符串
用 . 只能访问满足变量名规则的属性
用["a b"]可以访问数字/特殊字符串形式的属性名


Properties that contain functions are generally called **_methods_ **


### Object
```javascript
let descriptions = {
  work: "Went to work",
  "touched tree": "Touched a tree"
};
```
删除属性
```javascript
let obj = {a: 1, b: 2}
delete obj.b

// 与 obj.b = undefined 是不同的
```
in 操作符 , Object.keys(obj),  Object.assign()
```javascript
Object.assign(obj, {a:1, b:2, c:3})   // 把一个对象的属性复制给另一个对象
// {a: 1, b: 2, c: 3}
Object.keys(obj)
// (3) ["a", "b", "c"]
"a" in obj
// true
```
对象与基本类型的区别
```javascript
let a = "xxx"
let b = "xxx"
a === b
// true

let c = {a:1}
let d = {a:1}
c === d
// false

const score = {visitors: 0, home: 0};
score.visitors = 1; // This is okay
score = {visitors: 1, home: 1}; // This isn't allowed
```
简写
```javascript
let a = 1, b = [1,2,3]
let c = {a,b}  // 属性可简写变量名
c
// {a: 1, b: Array(3)}
```
Math.sqrt()  求平方根 square root
### Array
array的**includes**方法
```javascript
let arr = ['a', 'b', 'c']
arr.includes('a')  // 判断数组是否包含这个值
```
**of **遍历数组
```javascript
for (let i of arr) {
  console.log(i)   // i是arr里的值
}
```
indexOf和lastIndexOf
```javascript
console.log([1, 2, 3, 2, 1].indexOf(2));
// → 1
console.log([1, 2, 3, 2, 1].lastIndexOf(2));
// → 3

"one two three".indexOf("ee")  // 字符串也有indexOf
```
slice(a,b)  a和b都是索引，[a,b)半闭半开区间，**注意b不是长度**
```javascript
console.log([0, 1, 2, 3, 4].slice(2, 4));
// → [2, 3]
console.log([0, 1, 2, 3, 4].slice(2));
// → [2, 3, 4]
```
concat
```javascript
arr.concat("x")  // 不是数组会转为数组
```
其他
```javascript
/* trim */
console.log("  okay \n ".trim());

/* padStart */
console.log(String(6).padStart(3, "0"));
// → 006


/* split和join */
let sentence = "Secretarybirds specialize in stomping";
let words = sentence.split(" ");  // 生成数组
console.log(words);
// → ["Secretarybirds", "specialize", "in", "stomping"]
console.log(words.join(". "));  // 数组转为字符串
// → Secretarybirds. specialize. in. stomping  
```
### Rest parameters
```javascript
function fn(...numbers) {
  console.log(...numbers)
  console.log(numbers)   // numbers是参数数组
}

fn(1,2,3,4)
// 1 2 3 4
// [1, 2, 3, 4]

let a = [1, 2, 3, 4]
fn(...a)  // 把数组分解成独立的参数，等价于fn(1,2,3,4)

```
### Math Object
```javascript
Math.max (maximum)
Math.min (minimum)
Math.sqrt (square root)
Math.PI
Math.random()
Math.floor()
Math.ceil()
Math.round()
Math.abs()
```
### 析构 destructuring
```javascript
// 数组
function phi([n00, n01, n10, n11]) {
  return (n11 * n00 - n10 * n01) /
    Math.sqrt((n10 + n11) * (n00 + n01) *
              (n01 + n11) * (n00 + n10));
}

// 对象
let {name} = {name: "Faraji", age: 23};
console.log(name);
// → Faraji
```
### JSON
```javascript
// 格式
{
  "squirrel": false,
  "events": ["work", "touched tree", "pizza", "running"]
}


/* JSON.stringify 和 JSON.parse */
let string = JSON.stringify({squirrel: false,
                             events: ["weekend"]});
console.log(string);
// → {"squirrel":false,"events":["weekend"]}
console.log(JSON.parse(string).events);
// → ["weekend"]
```
### Exercises
#### 1. sum(range(a,b))
```javascript
// Your code here.
function range(start, end, step=1) {
  let arr = []
  if (step < 0) {
    for (let i = start; i >= end; i += step) 
      arr.push(i)
  }else {
    for (let i = start; i <= end; i += step) 
      arr.push(i)
  }
  
  return arr
}

function sum(arr) {
  let sum = 0
  for (let i of arr) {
    sum += i
  }
  
  return sum
}


console.log(range(1, 10));
// → [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
console.log(range(5, 2, -1));
// → [5, 4, 3, 2]
console.log(sum(range(1, 10)));
// → 55
```
#### 2. arr.reverse()
```javascript
function reverseArray(arr) {
  let output = []
  let x = arr[0]
  while(x){
    output.push(arr.pop())
    x = arr[0]
  }
  return output
}

function reverseArrayInPlace(arr) {
  for(let i = 0; i<Math.floor(arr.length / 2); i++){
    let temp = arr[i]
    arr[i] = arr[arr.length - i -1]
    arr[arr.length - i -1] = temp
  }
  return arr
}

console.log(reverseArray(["A", "B", "C"]));
// → ["C", "B", "A"];
let arrayValue = [1, 2, 3, 4, 5];
reverseArrayInPlace(arrayValue);
console.log(arrayValue);
// → [5, 4, 3, 2, 1]
```
#### 3. list
```javascript
/*********** arrayToList **************/
// 递归实现
function arrayToList(arr){
  if (arr.length === 1){
    return {value:arr[0], rest:null}
  }else if (arr.length > 1){
    return {value:arr[0], rest:arrayToList(arr.slice(1))}
  }
}
// for循环实现
function arrayToList(arr){
  let list = null
  for(let i = 0; i < arr.length; i++){
    list = {value:arr[i], rest:list}
  }
  return list
}

/*********** listToArray **************/
function listToArray(list){
  if (list.rest === null) {
    return [list.value]
  } else {
    return [list.value].concat(listToArray(list.rest))
  }
}

function listToArray(list){
  let arr = []
  for(let node=list; node; node = node.rest){
    arr.push(node.value)
  }
  return arr
}
/*********** prepend **************/
function prepend(value, list) {
  return {value:value, rest:list}
}
/*********** nth **************/
function nth(list, number) {
  if(number === 0) {
    return list.value
  } else if (number > 0) {
    return nth(list.rest, number-1)
  }
}

function nth(list, number) {
  let node = list
  for (let i = 1; i <= number; i++){
    node = node.rest
  }
  return node.value
}



console.log(arrayToList([10, 20]));
// → {value: 10, rest: {value: 20, rest: null}}
console.log(listToArray(arrayToList([10, 20, 30])));
// → [10, 20, 30]
console.log(prepend(10, prepend(20, null)));
// → {value: 10, rest: {value: 20, rest: null}}
console.log(nth(arrayToList([10, 20, 30]), 1));
// → 20
```
#### 4. Deep comparison
```javascript
function deepEqual(a,b) {
  if (a === b) return true
  
  if (a==null || typeof a !== "object" 
      || b==null || typeof b !== "object")
    return false
  
  let keysA = Object.keys(a), keysB = Object.keys(b)
  
  if (keysA.length !== keysB.length) return false
  
  for (let key of keysA) {
    if (!keysB.includes(key) || !deepEqual(a[key], b[key])) return false
  }
  
  return true
}

let obj = {here: {is: "an"}, object: 2};
console.log(deepEqual(obj, obj));
// → true
console.log(deepEqual(obj, {here: 1, object: 2}));
// → false
console.log(deepEqual(obj, {here: {is: "an"}, object: 2}));
// → true
```


