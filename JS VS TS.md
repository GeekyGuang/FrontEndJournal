# JS VS TS

### JS组件写法
```vue
<template>
  <ul class="type">
    <li :class="type === '-' && 'selected' " @click="selectType('-')">支出</li>
    <li :class="type === '+' && 'selected' " @click="selectType('+')">收入</li>
  </ul>
</template>

<script>
export default {
  name: "type",
  data() {
    return {
      type: '-'
    }
  },
  methods: {
    selectType(type) {
      if (type !== '-' && type !== '+') {
        throw new Error("type is unknown")
      }
      this.type = type
    }
  }
}
</script>
```
### TS组件
```typescript
<script lang="ts">
import Vue from 'vue'
import {Component} from 'vue-property-decorator';

@Component   // 先写@Component,tab键自动import上一句
export default class Types extends Vue {
    // data
    type= '-'
  
    // methods
    selectType(type: string) {
      if (type !== '-' && type !== '+') {
        throw new Error("type is unknown")
      }
      this.type = type
    }
    
    // 还可以写生命周期
    created(){}
    mounted(){}

}
</script>
```
JS也支持class语法，但是要把**编译时类型**去掉，JS不支持


### props
#### Vue Class Component里的props
```typescript
import Vue from 'vue';
import Component, {mixins} from 'vue-class-component';

const TypesProps = Vue.extend({
  props: {
    name: Number
  }
})

@Component
export default class Types extends mixins(Vue, TypesProps) {
  type = '-';

  selectType(type: string) {
    if (type !== '-' && type !== '+') {
      throw new Error('type is unknown');
    }
    this.type = type;
  }

  mounted(){
    console.log(this.name.toString());
  }

}
```
文档：[https://class-component.vuejs.org/](https://class-component.vuejs.org/)
#### vue-property-decorator里的@Prop
```typescript
import Vue from 'vue';
import { Component, Prop } from 'vue-property-decorator'

@Component
export default class Types extends Vue {
  
  @Prop(Number) readonly name: number | undefined
  // @Prop装饰器告诉Vue这是prop，不是data
  // Number告诉vue 运行时类型 是Number
  // number | undefined 告诉TS 编译时类型
  
  type = '-';   // 给了初始值就可以不指定类型
                // type:string = '-'

  selectType(type: string) {
    if (type !== '-' && type !== '+') {
      throw new Error('type is unknown');
    }
    this.type = type;
  }

  mounted(){
    // TypeScript会智能纠错
    if (this.name === undefined) {
      console.log("name is undefined")
    } else {
      console.log(this.name.toString());
    }
  }

}
```
TypeScript ->**编译时**-> JavaScript ->**运行时**->浏览器
TSC即使编译报错，还是会生成js文件
### 将webpack里的TS升级到最新版
查看最新版
```bash
npm info typescript version
```
将package.json里的typescript版本号改成最新版
最后执行
```bash
yarn install
```
### TypeScript的好处

1. 类型提示：更智能的提示
1. 编译时报错： 还没运行代码就知道自己写错了
1. 类型检查： 无法点出错误的属性
### 写Vue组件的三种方式(单文件)

1. 用JS对象
```javascript
export default {data, props, methods, created, ...}
```


2. 用TS类 <script lang="ts">
```typescript
@Component
export default class xxx extends Vue {
  xxx: string = 'hi';
  @Prop(Number) xxx: number | undefinded;
}
```

3. 用 JS 类 <script lang="js">
```javascript
@Component
export default class xxx extends Vue {
  xxx = 'hi'
}
```




