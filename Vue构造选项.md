# Vue构造选项

### 概述
- 把Vue的实例命名为**vm**是作者的习惯，应该沿用
- vm对象**封装**了对视图的所有操作， 包括**数据读写**、**事件绑定**、**DOM更新**
- vm的**构造函数**是Vue, 按照ES6的说法，vm所属的**类是Vue**
- options是new Vue的参数， 一般称之为**选项**或**构造函数**

**
### new Vue有哪些选项
#### el挂载
```javascript
new Vue({
  el: '#app',   // 挂载到id为app的元素
  render: h => h(demo)
})
```
可与**$mount**替换
```javascript
new Vue({
  render: h => h(demo)
}).$mount('#app')
```
### data()
完整版Vue.js写法
推荐用函数
有个bug
```javascript
new Vue({
  data(){
    return {
      n:0
    }
  },
  template:`
  <div class="red">
        {{n}}
        <button @click="add">+1</button>
    </div>
  `,
  methods:{
    add(){
      this.n += 1
    }
  }
  
}).$mount('#app')
```
### methods
事件处理函数或普通函数
可以替代filter
缺点是每次渲染其他部分也会调用这个函数
```javascript
new Vue({
  data(){
    return {
      array: [1,2,3,4,5,6,7,8]
    }
  },
  template:`
  <div class="red">
        {{filter()}}
    </div>
  `,
  methods:{
    filter(){
      return this.array.filter(item => item%2 === 0)
    }
  }
  
}).$mount('#app')
```
### components
#### 方法一：将vue文件引入为组件
优先使用方法一，模块化
```javascript
import Demo from './demo.vue'

new Vue({
  // 组件名
  components:{
    Demo   // Demo: Demo 的ES6简写 
  },
  data(){
    return {
      n:0,
    }
  },
  template:`
  <div class="red">
        {{n}}
        <button @click="add">+1</button>
        <hr>
        <Demo>   <!--使用组件-->
    </div>
  `,
  methods:{
    add(){
      this.n += 1
    }
  }
  
}).$mount('#app')
```
文件名最好全小写，win10分不清大小写
组件名首字母用大写
#### 方法二：Vue.component 声明全局组件
```javascript
// 注册全局组件
Vue.component('Demo2', {
  template:`
  <div >
      Demo222222
    </div>
  `
})


new Vue({
  data(){
    return {
      n:0,
    }
  },
  template:`
  <div class="red">
        {{n}}
        <button @click="add">+1</button>
        <hr>
        <Demo2>  <!--使用组件-->
    </div>
  `,
  methods:{
    add(){
      this.n += 1
    }
  }
  
}).$mount('#app')
```
#### 方法三：在components属性里声明
```javascript
new Vue({
  components: {
    Demo3: {
      template:`
      <div >
          Demo3333
        </div>
      `
    }

  },
  data(){
    return {
      n:0,
    }
  },
  template:`
  <div class="red">
        {{n}}
        <button @click="add">+1</button>
        <hr>
        <Demo3> <!--使用组件-->
    </div>
  `,
  methods:{
    add(){
      this.n += 1
    }
  }
  
}).$mount('#app')
```
template里可以将大写变小写中间加-
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1599908420322-d73f44ac-b82b-48aa-bc19-97708ff3d92f.png#align=left&display=inline&height=316&margin=%5Bobject%20Object%5D&name=image.png&originHeight=455&originWidth=652&size=146523&status=done&style=none&width=453)
### 4个钩子
```javascript
new Vue({
  data(){
    return {
      n:0,
    }
  },
  template:`
  <div class="red">
        {{n}}
        <button @click="add">+1</button>
    </div>
  `,
  methods:{
    add(){
      this.n += 1
    }
  },
  
  /* 4个钩子 */
  
  created(){
    // debugger  添加断点
    console.log('这玩意儿出现在内存中，还没有出现在页面中')},
  mounted(){
    console.log('这玩意儿出现在页面中')
  },
  updated(){
    console.log("更新了")
    console.log(this.n)
  },
  destroyed(){
    console.log('已经消亡了')
  }
}).$mount('#app')
```
### props
property
从外部引入属性
在vue文件中添加props
```vue
<template>
    <div class="red">
        我是外部demo<br>
        {{message}}
        <button @click="add2">+2</button>
    </div>
</template>

<script>
export default {
    props:['message','add2'], // 以字符串数组形式列出属性
}
</script>

<style scoped>
.red {
    color: red;
}
</style>
```
在main.js中传入外部属性值
不加冒号是静态绑定，只能传字符串
v-bind或冒号，是动态绑定，传入的是JS代码
```html
<!-- 静态 -->
<blog-post title="My journey with Vue"></blog-post>

<!-- 动态赋予一个变量的值 -->
<blog-post v-bind:title="post.title"></blog-post>

<!-- 动态赋予一个复杂表达式的值 -->
<blog-post
  v-bind:title="post.title + ' by ' + post.author.name"
></blog-post>
```




