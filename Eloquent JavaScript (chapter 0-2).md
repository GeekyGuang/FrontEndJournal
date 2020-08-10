# Eloquent JavaScript (chapter 0-2)

## Introduction
It is up to you to make the necessary effort. When you are struggling to follow the book, do not jump to any conclusions about your own capabilities. You are fine—you just need to keep at it. Take a break, reread some material, and make sure you read and understand the example programs and exercises. Learning is hard work, but everything you learn is yours and will make subsequent learning easier.

The art of programming is the skill of controlling complexity.

A sense of what a good program looks like is developed in practice, not learned from a list of rules.

## Values, Types, and Operators
### basic data type

- number
- string



**`**(backtick反引号)
escaping 转义 **\n**
concatenate: "con" **+** "cat" + "e" + "nate"
template literals:_ _`half of 100 is **${**100 / 2**}**`    `${xxx}`内的xxx会计算值
Unary operators(一元运算符)：**typeOf **"x"

- Boolean
- null 
- undefined
- symbol



short-circuit evaluation短路逻辑

- a || b : a为真则返回a,否则返回b
- a && b : a为假则返回a,否则返回b
## Program Structure
A fragment of code that produces a value is called an** _expression_**.
If an expression corresponds to a sentence fragment, a JavaScript **_statement_** corresponds to a full sentence. 
A program is a list of statements.


The simplest kind of statement is an expression with a semicolon after it.  **1;**
**a binding, or variable:**
```javascript
let caught = 5 * 5;
```
You should imagine bindings as **tentacles**, rather than boxes. They do not _contain_ values; they _grasp_ them—two bindings can refer to the same value.

The collection of bindings and their values that exist at a given time is called the **environment. **

Executing a function is called **_invoking_**, **_calling_**, or **_applying_** it

console.log
```javascript
let x = 30;
console.log("the value of x is", x);
// → the value of x is 30
```


When a function produces a value, it is said to **_return_** that value.
```javascript
Math.max(2,1,3,5,9)
// 9
Math.min(2,1,3,5,9)
// 1
```
**braces** (`{` and `}`)
The braces can be used to group any number of statements into a single statement, called a** _block_**.

indent 2 spaces


### exercises
#### 1. 打出三角形阵列
```javascript
for (let i = "#"; i.length < 8; i += "#")
  console.log(i)
```
#### 2. FizzBuzz
```javascript
for (let i = 1; i <= 100; i++) {
  let output = ''
  if (i % 3 === 0) output += "Fizz"
  if (i % 5 === 0) output += "Buzz"
  console.log(output || i)
}
```
#### 3. 象棋盘
```javascript
let size = 8
for (let i = 0; i < size; i++){
  let output = ''
  for(let j = 0; j < size; j++) {
    if ((i + j) % 2 === 0) output += " "
    else output += "#"
  }
  console.log(output)
}
```


