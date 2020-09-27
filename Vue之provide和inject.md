# Vue之provide和inject

祖先provide，后代inject，作用是大范围隔N代共享信息。
`provide` 选项应该是一个对象或返回一个对象的函数。该对象包含可注入其子孙的 property。
`inject` 选项应该是：

- 一个字符串数组，或
- 一个对象，对象的 key 是本地的绑定名，value 是：
   - 在可用的注入内容中搜索用的 key (字符串或 Symbol)，或
   - 一个对象，该对象的：
      - `from` property 是在可用的注入内容中搜索用的 key (字符串或 Symbol)
      - `default` property 是降级情况下使用的 value

示例
父组件provide
```javascript
<template>
  <div :class="`app theme-${themeName}`">
    <Child1/>
    <button>x</button>
  </div>
</template>

<script>
import Child1 from "./components/Child1.vue";
export default {
  name: "App",
  data() {
    return {
      themeName: "blue", // 'red'
      fontSize: "normal" // 'big' | 'small'
    };
  },
  provide(){
    return {changeColor: this.changeColor}
  },
  components: {
    Child1
  },
  methods:{
    changeColor(){
      if(this.themeName==='blue'){
        this.themeName = 'red'
      }else{
        this.themeName = 'blue'
      }
    }
  }
};
</script>

<style>
.app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.app.theme-blue button {
  background: blue;
  color: white;
}
.app.theme-blue {
  color: darkblue;
}

.app.theme-red button {
  background: red;
  color: white;
}
.app.theme-red {
  color: darkred;
}
</style>
```
子组件inject
```javascript
<template>
  <div>
    <button @click="changeColor">换肤</button>
  </div>
</template>

<script>
export default {
  inject:['changeColor']
}
</script>
```


