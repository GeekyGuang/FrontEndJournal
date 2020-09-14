# Vue之数据响应式

### getter，setter
```javascript
let obj0 = {
  姓: "高",
  名: "圆圆",
  age: 18
};

// 需求一，得到姓名

let obj1 = {
  姓: "高",
  名: "圆圆",
  姓名() {
    return this.姓 + this.名;
  },
  age: 18
};

console.log("需求一：" + obj1.姓名());
// 姓名后面的括号能删掉吗？不能，因为它是函数
// 怎么去掉括号？

// 需求二，姓名不要括号也能得出值

let obj2 = {
  姓: "高",
  名: "圆圆",
  get 姓名() {
    return this.姓 + this.名;
  },
  age: 18
};

console.log("需求二：" + obj2.姓名);

// 总结：getter 就是这样用的。不加括号的函数，仅此而已。

// 需求三：姓名可以被写

let obj3 = {
  姓: "高",
  名: "圆圆",
  get 姓名() {
    return this.姓 + this.名;
  },
  set 姓名(xxx){
    this.姓 = xxx[0]
    this.名 = xxx.slice(1)
  },
  age: 18
};

obj3.姓名 = '高媛媛'

console.log(`需求三：姓 ${obj3.姓}，名 ${obj3.名}`)

// 总结：setter 就是这样用的。用 = xxx 触发 set 函数
```
### Object.defineProperty()
`**Object.defineProperty()**` 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象。
```javascript
const object1 = {};

Object.defineProperty(object1, 'property1', {
  value: 42,
  writable: false
});

object1.property1 = 77;
// throws an error in strict mode

console.log(object1.property1);
// expected output: 42
```
设置get，set，使用proxy
```javascript
let data0 = {
  n: 0
}

// 需求一：用 Object.defineProperty 定义 n
let data1 = {}

Object.defineProperty(data1, 'n', {
  value: 0
})

console.log(`需求一：${data1.n}`)

// 总结：这煞笔语法把事情搞复杂了？非也，继续看。

// 需求二：n 不能小于 0
// 即 data2.n = -1 应该无效，但 data2.n = 1 有效

let data2 = {}

data2._n = 0 // _n 用来偷偷存储 n 的值

Object.defineProperty(data2, 'n', {
  get(){
    return this._n
  },
  set(value){
    if(value < 0) return
    this._n = value
  }
})

console.log(`需求二：${data2.n}`)
data2.n = -1
console.log(`需求二：${data2.n} 设置为 -1 失败`)
data2.n = 1
console.log(`需求二：${data2.n} 设置为 1 成功`)

// 抬杠：那如果对方直接使用 data2._n 呢？
// 算你狠

// 需求三：使用代理

let data3 = proxy({ data:{n:0} }) // 括号里是匿名对象，无法访问

function proxy({data}/* 解构赋值，别TM老问 */){
  const obj = {}
  // 这里的 'n' 写死了，理论上应该遍历 data 的所有 key，这里做了简化
  // 因为我怕你们看不懂
  Object.defineProperty(obj, 'n', { 
    get(){
      return data.n
    },
    set(value){
      if(value<0)return
      data.n = value
    }
  })
  return obj // obj 就是代理
}

// data3 就是 obj
console.log(`需求三：${data3.n}`)
data3.n = -1
console.log(`需求三：${data3.n}，设置为 -1 失败`)
data3.n = 1
console.log(`需求三：${data3.n}，设置为 1 成功`)

// 杠精你还有话说吗？
// 杠精说有！你看下面代码
// 需求四

let myData = {n:0}
let data4 = proxy({ data:myData }) // 括号里是匿名对象，无法访问

// data3 就是 obj
console.log(`杠精：${data4.n}`)
myData.n = -1
console.log(`杠精：${data4.n}，设置为 -1 失败了吗！？`)

// 我现在改 myData，是不是还能改？！你奈我何
// 艹，算你狠

// 需求五：就算用户擅自修改 myData，也要拦截他

let myData5 = {n:0}
let data5 = proxy2({ data:myData5 }) // 括号里是匿名对象，无法访问

function proxy2({data}/* 解构赋值，别TM老问 */){
  // 这里的 'n' 写死了，理论上应该遍历 data 的所有 key，这里做了简化
  // 因为我怕你们看不懂
  let value = data.n
  Object.defineProperty(data, 'n', {
    get(){
      return value
    },
    set(newValue){
      if(newValue<0)return
      value = newValue
    }
  })
  // 就加了上面几句，这几句话会监听 data

  const obj = {}
  Object.defineProperty(obj, 'n', {
    get(){
      return data.n
    },
    set(value){
      if(value<0)return//这句话多余了
      data.n = value
    }
  })
  
  return obj // obj 就是代理
}

// data3 就是 obj
console.log(`需求五：${data5.n}`)
myData5.n = -1
console.log(`需求五：${data5.n}，设置为 -1 失败了`)
myData5.n = 1
console.log(`需求五：${data5.n}，设置为 1 成功了`)


// 这代码看着眼熟吗？
// let data5 = proxy2({ data:myData5 }) 
// let vm = new Vue({data: myData})

// 现在我们可以说说 new Vue 做了什么了
```
### 数据响应式
Vue的data是响应式
const vm = new Vue({data: {n: 0}})
如果修改vm.n, 那么UI中的n就会响应我
Vue2 通过Object.defineProperty来实现数据响应式
#### data的bug
如果属性一开始就不存在，就不会被监听
```javascript
new Vue({
  data: {
    obj: {
      a: 0 // obj.a 会被 Vue 监听 & 代理
    }
  },
  template: `
    <div>
      {{obj.b}}
      <button @click="setB">set b</button>
    </div>
  `,
  methods: {
    setB() {
      this.obj.b = 1; //请问，页面中会显示 1 吗？
    }
  }
}).$mount("#app");
```
#### 解决办法
使用Vue.set或this.$set
作用：
新增key
自动创建代理和监听(如果没创建过)
触发UI更新(但并不会立刻更新)
```javascript
new Vue({
  data: {
    obj: {
      a: 0 // obj.a 会被 Vue 监听 & 代理
    }
  },
  template: `
    <div>
      {{obj.b}}
      <button @click="setB">set b</button>
    </div>
  `,
  methods: {
    setB() {    
      // this.obj.b = 1; //请问，页面中会显示 1 吗？
      console.log(Vue.set === this.$set)
      Vue.set(this.obj, 'b', 1)
      // this.$set(this.obj, 'b', 1)
    }
  }
}).$mount("#app");
```
#### 遇到数组怎么办？
不可能提前监听所有key
```javascript
new Vue({
  data: {
    array: ["a", "b", "c"]
  },
  template: `
    <div>
      {{array}}
      <button @click="setD">set d</button>
    </div>
  `,
  methods: {
    setD() {
      this.array[3] = "d"; //请问，页面中会显示 'd' 吗？
      // 等下，你为什么不用 this.array.push('d')
    }
  }
}).$mount("#app");
```
可以用Vue.set或this.$set新增key
```javascript
new Vue({
  data: {
    array: ["a", "b", "c"]
  },
  template: `
    <div>
      {{array}}
      <button @click="setD">set d</button>
      <button @click="add">+1</button>
    </div>
  `,
  methods: {
    setD() {
      Vue.set(this.array, 3, 0)   // 会更新UI
    },
    add(){
      this.array[3] += 1   // 点击+1不会有反应
    }
  }
}).$mount("#app");
```
尤雨溪篡改了7个数组API,使用这些api也可以
##### [变更方法](https://cn.vuejs.org/v2/guide/list.html#%E5%8F%98%E6%9B%B4%E6%96%B9%E6%B3%95)
Vue 将被侦听的数组的变更方法进行了包裹，所以它们也将会触发视图更新。这些被包裹过的方法包括：

- `push()`
- `pop()`
- `shift()`
- `unshift()`
- `splice()`
- `sort()`
- `reverse()`

你可以打开控制台，然后对前面例子的 `items` 数组尝试调用变更方法。比如 `example1.items.push({ message: 'Baz' })`
#### 注意
[官方文档：检查变化的注意事项](https://cn.vuejs.org/v2/guide/reactivity.html#%E6%A3%80%E6%B5%8B%E5%8F%98%E5%8C%96%E7%9A%84%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9)
Vue 不能检测以下数组的变动：

1. 当你利用索引直接设置一个数组项时，例如：`vm.items[indexOfItem] = newValue`
1. 当你修改数组的长度时，例如：`vm.items.length = newLength`



