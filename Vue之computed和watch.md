# Vue之computed和watch

### computed
computed是计算属性，根据依赖的数据动态显示新的计算结果，计算的结果会被缓存，除非依赖的属性值变化才会重新计算。computed里面的属性虽然是函数，但是也可以不加括号，直接当属性来用。
```javascript
var vm = new Vue({
  data: { a: 1 },
  computed: {
    // 仅读取
    aDouble: function () {
      return this.a * 2
    },
    // 读取和设置
    aPlus: {
      get: function () {
        return this.a + 1
      },
      set: function (v) {
        this.a = v - 1
      }
    }
  }
})
vm.aPlus   // => 2
vm.aPlus = 3
vm.a       // => 2
vm.aDouble // => 4
```
实现性别筛选
```javascript
Vue.config.productionTip = false;
let id = 0;
const createUser = (name, gender) => {
  id += 1;
  return { id, name, gender };
};
new Vue({
  data() {
    return {
      users: [
        createUser("方方", "男"),
        createUser("圆圆", "女"),
        createUser("小新", "男"),
        createUser("小葵", "女")
      ],
      gender:""
    };
  },
  
  computed:{   
    displayusers(){
      const {users, gender} = this
      if(gender===""){
        return users
      }else if(typeof gender==="string"){
        return users.filter(item => item.gender===gender)
      }else {
        throw new Error("gender 是意外值")
      }
    }
  },
  // 如何给三个按钮加事件处理函数
  // 思路一：点击之后改 users
  // 思路二：使用 computed
  template: `
    <div>
      <div>
      <button @click="gender=''">全部</button>
      <button @click="gender='男'">男</button>
      <button @click="gender='女'">女</button></div>
      <ul>
        <li v-for="u in displayusers" :key="u.id">
          {{u.name}} - {{u.gender}}
        </li>
      </ul>
    </div>
  `
}).$mount("#app");
```
### watch
watch是侦听，当数据变化时，执行一个函数，方法中可传入新值(val)和旧值(oldVal)，还可以定义handler方法，同时设置deep和immediate属性；还可以当Vue实例化后调用$watch;
语法如下
```javascript
var vm = new Vue({
  data: {
    a: 1,
    b: 2,
    c: 3,
    d: 4,
    e: {
      f: {
        g: 5
      }
    }
  },
  watch: {
    // 函数，可传入新值和旧值
    // 不要用箭头函数，没有this
    a: function (val, oldVal) {
      console.log('new: %s, old: %s', val, oldVal)
    },
    
    // 方法名
    b: 'someMethod',
    
    // 该回调会在任何被侦听的对象的 property 改变时被调用，不论其被嵌套多深
    c: {
      handler: function (val, oldVal) { /* ... */ },
      deep: true
    },
    
    // 该回调将会在侦听开始之后被立即调用
    d: {
      handler: 'someMethod',
      immediate: true
    },
    
    // 你可以传入回调数组，它们会被逐一调用
    e: [
      'handle1',
      function handle2 (val, oldVal) { /* ... */ },
      {
        handler: function handle3 (val, oldVal) { /* ... */ },
        /* ... */
      }
    ],
    
    // watch vm.e.f's value: {g: 5}
    'e.f': function (val, oldVal) { /* ... */ }
  }
})

vm.a = 2 // => new: 2, old: 1


// 还可以使用$watch
vm.$watch('xxx', fn, {deep:..., immediate:...})
// 'xxx'可以改为一个返回字符串的函数
```
### 总结
1.如果一个数据依赖于其他数据，那么使用computed
2.如果你需要在某个数据变化时做一些事情，那么使用watch
