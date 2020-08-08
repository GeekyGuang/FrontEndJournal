# JS函数对象

函数是对象


### 定义函数的4种方式
#### 具名函数
```javascript
// 函数名为fn
function fn (x, y) {
  return x + y
}

fn()  // 调用函数
```
#### 匿名函数
```javascript
// 将函数的地址复制给a, 右边的也叫函数表达式
let a = function (x, y) {
  return x + y
}

a()  // 调用函数
```
具名函数也可以赋值给变量，不过不能用函数名调用
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596374439670-53b8e2a5-b63e-47a8-a67d-2908e81a95aa.png#align=left&display=inline&height=162&margin=%5Bobject%20Object%5D&name=image.png&originHeight=194&originWidth=484&size=51939&status=done&style=none&width=403)
#### 箭头函数
```javascript
let f1 = () => console.log("hello")   // 无参数
f1()

let f2 = x => x * x  // 一个参数， 省略了return
f2(10)

let f3 = (x, y) => {return x + y}   // 两个参数就要加(), 有return或2个以上语句就要加{}
f3(2, 3)

let f4 = x => ({name: x})  // {}优先解释为代码块，返回对象要加()
```
#### 构造函数
```javascript
let fn = new Function('x', 'y', 'return x + y')
// 所有函数都由Function构造出来
```
### 调用时机
```javascript
let a = 1
function fn(){
  setTimeout(()=>{
  console.log(a)
  },0)
}

fn()
a = 2

// 打印出2
```
```javascript
let i = 0
for(i = 0; i<6; i++){
  setTimeout(()=>{
  console.log(i)
  },0)
}

// 打印出6个6
```
```javascript
for(let i = 0; i<6; i++){
  setTimeout(()=>{
  console.log(i)
  },0)
}

// 打印出0,1,2,3,4,5
// JS在for和let一起用时会加东西，每次循环都保留那个i,再新创建一个i
```
### 作用域
let 的作用域只在{}里
```javascript
function fn(){
  let a = 1
}
fn() 
console.log(a)  // 访问不到a
```
在顶级作用域声明的变量为全局变量
window的属性为全局变量
其他为局部变量

给window加属性，可以在任何位置
```javascript
let b = 1

function f2() {
  window.c = 2  // 给window添加属性
}
f2()   // 必须执行，才能声明c

function f1() {
  console.log(c)
}
f1()
```


函数嵌套
```javascript
function f1(){
  let a = 1
  
  function f2(){
    let a = 2
    console.log(a)  // // step2: a = 2
  }
  
  console.log(a)  // step1: a = 1
  a = 3
  f2()
}

f1()

// 输出结果为 1, 2
```
```javascript
function f1(){
  let a = 1
  function f2(){
    let a = 2
    function f3(){
      console.log(a)
    }   
    a = 22
    f3()   // step2: a = 22
  }  
  console.log(a)  // step1: a = 1
  a = 100
  f2()
}
f1()

// 输出结果为: 1, 22
```
嵌套的函数并不能从外部调用
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596379963754-e47fb3e5-7b93-4f63-ae3f-2876e155261d.png#align=left&display=inline&height=192&margin=%5Bobject%20Object%5D&name=image.png&originHeight=384&originWidth=762&size=30225&status=done&style=none&width=381)
#### 作用域规则

- 如果多个作用域有同名变量a, 查找a的声明时，向上取最近的作用域
- 简称“就近原则”
- 查找a的过程与函数执行无关
- 但a的值与函数执行有关
- 与函数执行无关的作用域叫静态作用域(词法作用域)



### 闭包 closure**
如果一个函数用到了外部的变量，那么这个函数加这个变量就叫做闭包
**![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596380077832-35dd016f-739f-466c-a480-37dad5746ced.png#align=left&display=inline&height=300&margin=%5Bobject%20Object%5D&name=image.png&originHeight=599&originWidth=812&size=42538&status=done&style=none&width=406)**
### 形参和返回值
形参 parameter  实参 argument


形参只是声明
```javascript
function add(x) {
  return x + arguments[1]
}

add(1, 2)
```


返回值

- 只有函数才有返回值
- 且每个函数都有返回值，没写return则返回undefined
```javascript
function xxx() {
  return console.log("hi")    // 返回值是undefined
}
```
### 调用栈
JS引擎在调用一个函数前，需要把函数所在的环境push到一个数组里，这个数组叫做调用栈。
等函数执行完毕，就会把环境pop出来，回到之前的环境，继续执行后续代码


递归：先递进后回归  递进是压栈，回归是弹栈


![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596430419686-8e33dc7e-049d-41f5-92de-4b485ee87c9e.png#align=left&display=inline&height=437&margin=%5Bobject%20Object%5D&name=image.png&originHeight=873&originWidth=1468&size=266335&status=done&style=none&width=734)
栈的容量是有限的，压入过多，就会爆栈
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596430633568-78d44cb7-b63e-45c2-9748-0f80dfaeaa87.png#align=left&display=inline&height=376&margin=%5Bobject%20Object%5D&name=image.png&originHeight=468&originWidth=590&size=162073&status=done&style=none&width=474)
### 函数提升
function fn(){}
不管把具名函数声明在哪里，都会跑到第一行


let fn = function(){}
用匿名函数赋值变量不会函数提升


let不允许重复声明
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596430834086-de60d654-336e-4507-827f-ef4d9553f2b1.png#align=left&display=inline&height=92&margin=%5Bobject%20Object%5D&name=image.png&originHeight=141&originWidth=696&size=51749&status=done&style=none&width=456)


### arguments 和 this
JS三座大山

- 闭包
- this
- AJAX

翻过三座大山才算入门


arguments是包含所有参数的伪数组
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596458446458-ca490868-a8d6-4b5a-b265-203bba32c40b.png#align=left&display=inline&height=245&margin=%5Bobject%20Object%5D&name=image.png&originHeight=490&originWidth=1067&size=51003&status=done&style=none&width=533.5)
调用fn就传入arguments




不给条件，this默认指向window
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596458532554-fde36f26-6737-405d-9791-9342ef8afa99.png#align=left&display=inline&height=90&margin=%5Bobject%20Object%5D&name=image.png&originHeight=179&originWidth=1259&size=26468&status=done&style=none&width=629.5)


用call传入this，如果传入的不是对象，会被自动转为对象
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596459258643-cfb275cb-2f6b-46e0-abb4-e07e2ca61351.png#align=left&display=inline&height=126&margin=%5Bobject%20Object%5D&name=image.png&originHeight=186&originWidth=735&size=15683&status=done&style=none&width=499)
'use strict' 阻止转换
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596459463279-43f7313a-9386-4901-9cc9-a809e691711a.png#align=left&display=inline&height=196&margin=%5Bobject%20Object%5D&name=image.png&originHeight=269&originWidth=614&size=16312&status=done&style=none&width=448)


调用对象里的函数，this默认传的是对象本身
可以使用call显示的传入this
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596459017231-b6d89b6c-9bbd-4b06-a48a-4ffff8f25662.png#align=left&display=inline&height=411&margin=%5Bobject%20Object%5D&name=image.png&originHeight=557&originWidth=664&size=49951&status=done&style=none&width=490)
call第一个参数是this, 之后的参数都是arguments


![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596459612212-0da5596d-6508-4951-b316-ae1c79730fab.png#align=left&display=inline&height=155&margin=%5Bobject%20Object%5D&name=image.png&originHeight=266&originWidth=1157&size=34499&status=done&style=none&width=675)


总结：

1. 在 new fn() 调用中，fn 里的 this 指向新生成的对象，这是 new 决定的
1. 在 fn() 调用中， this 默认指向 window，这是浏览器决定的
1. 在 obj.fn() 调用中， this 默认指向 obj，这是 JS 的隐式传 this
1. 在 fn.call(xxx) 调用中，this 就是 xxx，这是开发者通过 call 显式指定的 this
1. 在 arrow() 调用中，arrow 里面的 this 就是 arrow 外面的 this，因为箭头函数里面没有自己的 this
1. 在 arrow.call(xxx) 调用中，arrow 里面的 this 还是 arrow 外面的 this，因为箭头函数里面没有自己的 this



以后都使用call调用函数
fn.call(undefined, 1, 2, 3)
fn.apply(undefined, [1, 2, 3])

绑定this
使用.bind让this不被改变
```javascript
function f1(p1, p2){
  console.log(this, p1, p2)
}
let f2 = f1.bind({name:'xxx'})

f2()  // 等价于 f1.call({name:'xxx'})

// 也可以绑定参数

let f3 = f1.bind({name:'xxx'}, 1, 2}
```


箭头函数没有arguments和this
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596460182377-0994be3c-dbcd-4194-8f97-26591e3bd69c.png#align=left&display=inline&height=208&margin=%5Bobject%20Object%5D&name=image.png&originHeight=356&originWidth=1264&size=54244&status=done&style=none&width=738)


### 立即执行函数
立即执行函数用来造局部变量
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596460260717-34cc13ef-b3e5-4196-8068-0fcc01e1a19e.png#align=left&display=inline&height=179&margin=%5Bobject%20Object%5D&name=image.png&originHeight=223&originWidth=543&size=12095&status=done&style=none&width=435)


用let可以轻松制造局部变量
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596460350855-fb5b418e-4f75-4780-8ef7-b764f0d906bd.png#align=left&display=inline&height=221&margin=%5Bobject%20Object%5D&name=image.png&originHeight=350&originWidth=920&size=28008&status=done&style=none&width=582)



