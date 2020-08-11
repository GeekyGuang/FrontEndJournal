# Eloquent JavaScript(chapter 3)

## Function
A `return` keyword without an expression after it will cause the function to return `undefined`. Functions that don’t have a `return` statement at all, similarly return `undefined`.
#### Bingdings
Bindings declared with `let` and `const` are in fact local to the _block_ that they are declared in, so if you create one of those inside of a loop, the code before and after the loop cannot “see” it.
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1597106785658-bfe4e160-d0bf-4c22-84fd-7fe30524ea6c.png#align=left&display=inline&height=214&margin=%5Bobject%20Object%5D&name=image.png&originHeight=214&originWidth=481&size=17477&status=done&style=none&width=481)
在for()内用let声明的变量，其scope在{}内

#### 函数提升
```javascript
console.log("The future says:", future());

function future() {
  return "You'll never have flying cars";
}
```
#### Arrow functions
```javascript
const power = (base, exponent) => {
  let result = 1;
  for (let count = 0; count < exponent; count++) {
    result *= base;
  }
  return result;
};

// 下面两个等价
const square1 = (x) => { return x * x; };
const square2 = x => x * x;
```
#### Optional arguments
```javascript
function fn(a, b) {do something}

fn(a,b,c,d)   // 传多的参数会被忽略
fn(a)  // 少传的参数为undefined

function fn(a, b = 2) // 设置默认值
{do something}   
```
#### The call stack
```javascript
function chicken() {
  return egg();
}
function egg() {
  return chicken();
}
console.log(chicken() + " came first.");
// → ??
```
#### Closure闭包
```javascript
function wrapValue(n) {
  let local = n;
  return () => local;
}

// wrap1和wrap2是wrapValue返回的函数
let wrap1 = wrapValue(1);
let wrap2 = wrapValue(2);
console.log(wrap1());
// → 1
console.log(wrap2());
// → 2


function multiplier(factor) {
  return number => number * factor;
}

let twice = multiplier(2);
console.log(twice(5));
// → 10
```
This feature—being able to reference a specific instance of a local binding in an enclosing scope—is called **_closure_**. A function that references bindings from local scopes around it is called _a_ **closure**.

A good mental model is to think of function values as containing both the code in their body and the **environment **in which they are created. When called, the function body sees the environment in which it was created, not the environment in which it is called.

#### Recursion递归
```javascript
function findSolution(target) {
  function find(current, history) {
    if (current == target) {
      return history;
    } else if (current > target) {
      return null;
    } else {
      return find(current + 5, `(${history} + 5)`) ||
             find(current * 3, `(${history} * 3)`);
    }
  }
  return find(1, "1");
}

console.log(findSolution(24));
// → (((1 * 3) + 5) * 3)
```
### exercises
#### 1. minimum
```javascript
let min = (a,b) => a > b ? b : a;

console.log(min(0, 10));
console.log(min(0, -10));
```
#### 2. isEven
```javascript
function isEven(x) {
  if (x === 0) return true
  else if (x === 1) return false
  else if (x < 0) return isEven(-x)
  else return isEven(x - 2)
}

console.log(isEven(50));
// → true
console.log(isEven(75));
// → false
console.log(isEven(-1));
```
#### 3. Bean counting
```javascript
function countBs(str) {
  return countChar(str, 'B')
}

function countChar(str, char) {
   let count = 0
  for (let i = 0; i < str.length; i++)
    if (str[i] === char) count += 1
  return count
}

console.log(countBs("BBC"));
// → 2
console.log(countChar("kakkerlak", "k"));
// → 4
```


