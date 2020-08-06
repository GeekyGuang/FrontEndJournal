# JS对象

### 2种声明方式
```javascript
let obj1 = {name: "jack", age: 18}
let obj2 = new Object({name: "jack", age: 18})

// 新建空对象
let obj1 = {}
let obj2 = new Object()
```
#### 细节

- 键名是字符串，不是标识符，可以包含任意字符
- 引号可以省略，省略之后只能写成标识符或纯数字形式
- 就算省略引号，键名也还是字符串



#### 奇怪的属性名
```javascript
let obj = {
  1: 'a',
  3.2: 'b',
  1e2:true,
  1e-2:true,
  .234:true,
  0xFF:true
}

Object.keys(obj)  // (6) ["1", "100", "255", "3.2", "0.01", "0.234"]
```


#### 变量做属性名
```javascript
let sss = "name"
let obj = {
  [sss]:"jack"
}
// {name: "jack"}
```
[]会先求值再转为字符串


### 原型和原型链
每个对象都有一个隐藏属性__proto__，指向一个由共有属性组成的对象
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596263007362-a6f5b910-0594-4b0a-bd1b-9643eb5f086d.png#align=left&display=inline&height=45&margin=%5Bobject%20Object%5D&name=image.png&originHeight=47&originWidth=375&size=2392&status=done&style=none&width=358)


window.Object.prototype是对象的根
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596263102068-1c3c73fc-a72b-4b96-ba88-74e915ed4361.png#align=left&display=inline&height=45&margin=%5Bobject%20Object%5D&name=image.png&originHeight=49&originWidth=389&size=2307&status=done&style=none&width=356)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596263076242-10da891c-8cdd-408b-a0a9-17ad28a74592.png#align=left&display=inline&height=43&margin=%5Bobject%20Object%5D&name=image.png&originHeight=47&originWidth=393&size=2690&status=done&style=none&width=360)
#### 修改原型
```javascript
let obj = {}
obj.__proto__.toString = "xxx"  // 不推荐
Object.prototype.toString = "xxx"

let common = {name: "hello"}
let obj = Object.create(common)    // 以common为共有属性创建对象
```
##### 修改原型为其他对象，则产生原型链
#### ![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596263561125-b9e733e9-a1d3-46f7-b39e-02fb056b6512.png#align=left&display=inline&height=91&margin=%5Bobject%20Object%5D&name=image.png&originHeight=104&originWidth=552&size=5204&status=done&style=none&width=482)


### 查
```javascript
Object.keys() // 获取自身所有属性名
Object.values() // 获取自身所有属性值
Object.entries() // 获取自身所有键值对数组
console.dir() // 查看自身和共有的属性

// 判断属性名是否在对象内(包括自身和共有的)
"toString" in obj   // true

// 判断一个属性是自身还是共有的：
obj.hasOwnProperty('toString')   // false

/* 访问属性 */
obj["name"]  // 字符串
obj.name  // 标识符形式键名
obj[name]   // 变量

// 数字形式的键名只能用 obj["123"]
// 也可以不加引号 obj[123]
```


### 删
```javascript
delete obj["xxx"]    // 完全删除
obj["xxx"] = undefined   // 并未删除
```


### 增/改
```javascript
let obj = {}
obj.name = "jack"   // 新增
obj.name = "rose"   // 修改

Object.assign(obj, {age: 18, weight: 100})   // 批量赋值
```














































