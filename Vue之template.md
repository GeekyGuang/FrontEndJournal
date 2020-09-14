# Vue之template

### template三种写法
#### 1. 完整版，写在html里
```html
<div id=xxx>
  {{n}}
  <button @click="add">+1</button>
</div>
```
```javascript
new Vue({
  el: '#xxx',
  data: {n:0}, // data可以改成函数
  methods:{add(){}}
})
```
#### 2. 完整版写在options里
```html
<div id=app>
</div>
```
```javascript
new Vue({
  template:`
  <div>
    {{n}}
    <button @click="add">+1</button>
  </div>
  `,
  data: {n:0},
  methods:{add(){this.n += 1}}
}).$mount('#app')

// 挂载到div#app, div的原内容会被替代
```
#### 3. 非完整版，配合xxx.vue文件
vue文件
```vue
<template>
  <div>
    {{n}}
    <button @click="add">+1</button>
  </div> 
</template>

<script>
export default {
  data(){return {n:0}},  // data必须为函数
  methods:{add(){this.n += 1}}
}
</script>

<style>这里写CSS代码</style>
```
在另一个地方引入vue文件，并render
```javascript
import Xxx from './xxx.vue'
// Xxx是一个options对象

new Vue({
  render: h => h(Xxx)
}).$mount('#app')
```
**注意**：<template>是HTML5的元素，不是Vue的
### 语法
#### 表达式
{{ object.a }} 表达式
{{ n + 1 }} 可以写任何运算
{{ fn(n) }} 可以调用函数，methods里的
如果值为 undefined 或 null 就不显示
另一种写法 <div v-text="表达式"></div>
#### v-html
更新元素的 `innerHTML`
假设 data.x 值为 <strong>hi</strong>
<div v-html="x"></idv>
#### v-pre
不对模板进行编译
```html
<span v-pre>{{ this will not be compiled }}</span>
```
#### v-bind绑定属性
```html
<!-- 绑定一个 attribute -->
<img v-bind:src="imageSrc">

<!-- 缩写 -->
<img :src="imageSrc">

<!-- style 绑定 -->
<div :style="{ fontSize: size + 'px' }"></div>
<div :style="[styleObjectA, styleObjectB]"></div>

<div :style="{ border: '1px solid red', height:100}"> </div>  
<!-- 100px 写成 100 -->
```
#### v-on
绑定事件监听器。事件类型由参数指定。表达式可以是一个方法的名字或一个内联语句，如果没有修饰符也可以省略
```html
<!-- 方法处理器 -->
<button v-on:click="doThis"></button>

<!-- 内联语句 -->
<button v-on:click="doThat('hello', $event)"></button>

<!-- 缩写 -->
<button @click="doThis"></button>

<!-- 停止冒泡 -->
<button @click.stop="doThis"></button>

<!-- 阻止默认行为 -->
<button @click.prevent="doThis"></button>

<!-- 阻止默认行为，没有表达式 -->
<form @submit.prevent></form>
```
#### 条件判断
`v-if` 指令用于条件性地渲染一块内容。这块内容只会在指令的表达式返回 truthy 值的时候被渲染
```html
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```
#### v-for
```html
<ul>
  <li v-for="(u,index) in users" :key="index">
    索引: {{index}} 值: {{u.name}}
  </li>
</ul>

<ul>
  <li v-for="(value,name) in obj" :key="name">
    属性名: {{name}} 属性值: {{value}}
  </li>
</ul>
```
#### v-show
另一个用于根据条件展示元素的选项是 `v-show` 指令。用法大致一样：
```html
<h1 v-show="n%2===0">Hello!</h1>
```
`v-show` 只是简单地切换元素的 CSS property `display`。
注意，`v-show` 不支持 `<template>` 元素，也不支持 `v-else`。
#### v-cloak
这个指令保持在元素上直到关联实例结束编译。和 CSS 规则如 `[v-cloak] { display: none }` 一起用时，这个指令可以隐藏未编译的 Mustache 标签直到实例准备完毕。
```html
[v-cloak] {
  display: none;
}
<div v-cloak>
  {{ message }}
</div>
```
不会显示，直到编译结束。
#### v-once
只渲染元素和组件**一次**。随后的重新渲染，元素/组件及其所有的子节点将被视为静态内容并跳过。这可以用于优化更新性能。
```html
<!-- 单个元素 -->
<span v-once>This will never change: {{msg}}</span>

<!-- 有子元素 -->
<div v-once>
  <h1>comment</h1>
  <p>{{msg}}</p>
</div>

<!-- 组件 -->
<my-component v-once :comment="msg"></my-component>

<!-- `v-for` 指令-->
<ul>
  <li v-for="i in list" v-once>{{i}}</li>
</ul>
```
#### 使用事件抛出一个值
有的时候用一个事件来抛出一个特定的值是非常有用的。例如我们可能想让 `<blog-post>` 组件决定它的文本要放大多少。这时可以使用 `$emit` 的第二个参数来提供这个值：
```html
<button v-on:click="$emit('enlarge-text', 0.1)">
  Enlarge text
</button>
```
然后当在父级组件监听这个事件的时候，我们可以通过 `$event` 访问到被抛出的这个值：
```html
<blog-post
  ...
  v-on:enlarge-text="postFontSize += $event"
></blog-post>
```
#### 修饰符
```html
@click.stop="add"表示阻止事件传播/冒泡
@click.prevent="add"表示阻止默认动作
@click.stop.prevent="add"同时表示两种意思
```


