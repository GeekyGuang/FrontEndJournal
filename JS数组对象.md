# JS数组对象

JS没有真正的数组，是用对象模拟

- 元素的数据类型可以不同
- 内存不一定连续(随机存储)
- 数字下标其实是字符串，arr[1]是自动把数字转为字符串
- 数组可以有任何key, 比如arr['xxx'] = 'aaa'



### 创建一个数组
#### 新建
```javascript
let arr = [1, 2, 3]
let arr = new Array(1, 2, 3)   // 参数是元素
let arr = new Array(3)    // 只给一个参数是length
```
#### 转化
```javascript
let arr = '1,2,3,4'.split(',')   // 字符串转数组
let arr = "abcdefg".split('')
let arr = Array.from("123abc")  
```
Array.from()会尝试将不是数组的东西转为数组
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596346514850-73b568b6-63f8-4a5b-894f-57af87585fbc.png#align=left&display=inline&height=195&margin=%5Bobject%20Object%5D&name=image.png&originHeight=328&originWidth=1045&size=36989&status=done&style=none&width=620)


#### 伪数组
有数组形式，但没有数组共有属性(pop, push)的数组称为伪数组
```javascript
let divList = document.querySelectorAll('div')   // 伪数组
let divArr = Array.from(divList)   // 转为真数组
```
#### 合并与截取
```javascript
arr1.concat(arr2)   // 合并2个数组

arr1.slice(1)  // 从index 1开始截取
arr1.slice(1, 3)  // 截取索引1到3

// 注意，JS只提供浅拷贝
```


### 删元素
#### delete

- length = 最大整数key+1
- 用delete删除元素，形成empty空位元素不影响length

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596347404850-aa6e320f-2278-4af1-9a04-5285d6fd1db1.png#align=left&display=inline&height=219&margin=%5Bobject%20Object%5D&name=image.png&originHeight=348&originWidth=636&size=23080&status=done&style=none&width=401)


有空位元素的数组称为“稀疏数组”，不建议使用


#### 更改length
直接更改length也可以删元素
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596347626039-afeee788-4c2e-495c-8166-762e0e2bfd6b.png#align=left&display=inline&height=178&margin=%5Bobject%20Object%5D&name=image.png&originHeight=273&originWidth=549&size=14373&status=done&style=none&width=357)
#### 推荐的方法
```javascript
let arr = [1, 2, 3, 4, 5]
arr.pop()  // 删除最后一个元素，并返回被删的元素值
arr.shift()  // 删除第一个元素，并返回被删的元素值

arr.splice(1, 2) // 从index=1开始删除2个元素, 并返回被删的元素值
arr.splice(1, 2, 'x')  // 删除之后，添加元素'x'
arr.splice(1, 2, 'x', 'y')  // 删除之后添加元素'x', 'y'
```
### 查元素
#### for循环
```javascript
let arr = [1, 2, 3, 4] 
arr.x = 'xxx'
Object.keys(arr)   //  ["0", "1", "2", "3", "x"]

// in操作符会列出所有key(数字和非数字)
for (let key in arr) { 
  console.log(`${key}:${arr[key]}`)
}

// 只遍历数字key
for (let i = 0; i < arr.length; i++ ) {
  console.log(`${i}:${arr[i]}`)
}
```
(`${expression}`)中的引号是反引号 ``


#### forEach
`**forEach()**` 方法对数组的每个元素执行一次给定的函数。
```javascript
let arr = ['a', 'b', 'c'];
arr.forEach(function(element){console.log(element)})
arr.forEach(element => console.log(element));

arr.forEach(function(xxx,yyy){
  console.log(`${yyy}:${xxx}`)
})

arr.forEach((xxx,yyy) =>
  console.log(`${yyy}:${xxx}`)
)

// 参数依次为：元素，索引，数组本身
arr.forEach(function(element, index, arr){do something})  
```


for 循环与 forEach的区别：

- for循环可以break和continue，forEach只能对每个元素执行，直到结束
- for循环是块级作用域，forEach有函数作用域



#### 查看单个属性
**`arr[key]`** 用key访问元素
```javascript
let arr = [1, 2, 3]
arr[4]  // 越界返回 undefined
```
**`indexOf()`** 查找某个值的索引
```javascript
let arr = [1, 2, 3, 4]
arr.indexOf(1)
arr.indexOf('xxx')   // -1表示未找到
```
**`find(fn)`** 找出第一个符合条件的元素
```javascript
let arr = [1, 2, 3, 4, 5]

// 找出第一个大于2的elment值
arr.find(element => element > 2)

// 找出第一个大于2的elment值的索引
arr.findIndex(element => element > 2)

// 和forEach()一样可以传3个参数
arr.find((element, index) => console.log(`${index}:${element}`))
```
### 增/改
#### 插入元素
```javascript
let arr = []

// 在尾部插入
arr.push('a')
arr.push('b','c','d')

// 在头部插入
arr.unshift(100)

// 在中间插入
arr.splice(2, 0 , 'x', 'y') 
```
#### 排列顺序
**`sort() `**如果没有指明 `compareFunction` , 则按每个字符的Unicode位点进行排序
```javascript
let arr = [1, 100,  0 , -1, 'a', 'z', 6, 'c']
arr.sort()

// [-1, 0, 1, 100, 6, "a", "c", "z"]
```


给**`sort()`**指明compareFunction

- 如果 `compareFunction(a, b)` 小于 0 ，那么 a 会被排列到 b 之前；
- 如果 `compareFunction(a, b)` 等于 0 ， a 和 b 的相对位置不变。
- 如果 `compareFunction(a, b)` 大于 0 ， b 会被排列到 a 之前。
- `compareFunction(a, b)` 必须总是对相同的输入返回相同的比较结果，否则排序的结果将是不确定的。
```javascript
// 如果是比较字符串，必须返回确定的值
let arr = [1, 100, 20, 'a', 50, 'z', 33, 'f']
arr.sort(function(a,b){
  if (a > b) {return 1}
  else if (a === b) {return 0}
  else {return -1}
})

// 如果只比较数字，可以只返回a-b
let arr = [1,5,7,100,2,3,40]
arr.sort((a,b) => a - b)   // 升序
arr.sort((a,b) => b - a)   // 降序
```


**`reverse()`** 反转数组
```javascript
let arr = [1, 100,  0 , -1, 'a', 'z', 6, 'c']
arr.reverse()

// ["c", 6, "z", "a", -1, 0, 100, 1]

/* 反转字符串 */
let str = "aksmew193s"
str = str.split('').reverse().join('')   // "s391wemska"
```
#### 数组变换
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596353626652-11aa2f1a-4d40-45f1-adb6-917fc7957c02.png#align=left&display=inline&height=320&margin=%5Bobject%20Object%5D&name=image.png&originHeight=562&originWidth=1000&size=297030&status=done&style=none&width=569)
`**map()**` 方法创建一个新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值。
```javascript
let arr = [1,2,3,4,5,6]
arr.map(item => item * item)

arr.map(Math.sqrt)
```
`**filter()**` 方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。
```javascript
let arr = [1,2,3,4,5,6]
arr.filter(item => item%2 === 0 ? true : false)
arr.filter(item => item%2 === 0)
```
`**reduce()**` 方法对数组中的每个元素执行一个由您提供的**reducer**函数(升序执行)，将其结果汇总为单个返回值。
```javascript
/* 求和 */
let arr = [1, 2, 3, 4, 5, 6]
let sum = 0
for(let i=0; i<arr.length; i++){
  sum += arr[i]
}
console.log(sum)

arr.reduce((sum,item)=>sum+item, 0)  // 0是累加器sum的初始值
arr.reduce((sum,item)=>sum+item)     // 不提供初始值，默认为0

/* 实现filter()功能 */
let arr = [1, 2, 3, 4, 5]
arr.reduce((result, item)=>{
  if(item%2 === 1){
    return result
  }else{
    return result.concat(item)
  }
}, [])

arr.reduce((result, item)=> result.concat(item%2 === 1 ? [] : item), [])
```
### 习题
#### 1. 把数字变成星期
```javascript
let arr = [0,1,2,2,3,3,3,4,4,4,4,6]
let arr2 = arr.map((i)=>{
  const hash = {0:'周日',1:'周一',2:'周二',3:'周三',4:'周四',5:'周五',6:'周六'}
  return hash[i]
})
console.log(arr2) // ['周日', '周一', '周二', '周二', '周三', '周三', '周三', '周四', '周四', '周四', '周四','周六']
```
#### 2. 找出所有>60分的成绩
```javascript
let scores = [95,91,59,55,42,82,72,85,67,66,55,91]
let scores2 = scores.filter(item => item > 60)
console.log(scores2) //  [95,91,82,72,85,67,66, 91]
```
#### 3. 算出所有奇数之和
```javascript
let scores = [95,91,59,55,42,82,72,85,67,66,55,91]
let sum = scores.reduce((sum, n)=>{
  return n%2 === 1 ? sum+n : sum
},0)
console.log(sum) // 奇数之和：598 
```
#### 4. 面试题
```javascript
let arr = [
  {名称:'动物', id:1, parent: null},
  {名称:'狗', id:2, parent: 1},
  {名称:'猫', id:3, parent: 1}
]

// 数组变成对象
arr.reduce((result, item)=>{
  if (item.parent === null) {
    result.id = item.id
    result['名称'] = item['名称']
  } else {
    delete item.parent
    item.children = null
    result.children.push(item)
  }
  return result
}, {id:null, children:[]})

// 得到结果
{
  id:1, 名称: '动物', children:[
    {id:2,名称:'狗',children:null},
    {id:3,名称:'猫',children:null},
  ]
}

```




