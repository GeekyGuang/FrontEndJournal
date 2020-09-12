# Vue.js与Vue.runtime.js的区别

### 区别
- Vue.js是Vue完整版，Vue.runtime.js是非完整版
- Vue完整版有compiler, 非完整版没有compiler，非完整版相比完整版体积要小大约 30%
- Vue完整版视图写在HTML里或者写在template选项，非完整版写在render函数里，用h来创建标签
- cdn引入时文件名不同
- webpack引入时，完整版需配置alias, 默认为非完整版
- @vue/cli引入完整版需额外配置，默认为非完整版
- 推荐总是使用非完整版，配合vue-loader和vue文件



### Vue单文件组件
新建一个demo.vue文件,里面包含**template**, **script**, **style**三部分
```vue
<template>
    <div class="red">
        {{n}}
        <button @click="add">+1</button>
    </div>
</template>

<script>
export default {
    data(){
        return {
            n: 0
        }
    },
    methods: {
        add(){
            this.n += 1
        }
    }
}
</script>

<style scoped>
.red {
    color: red;
}
</style>
```
在main.js里引入demo.vue文件，并新建Vue实例
```javascript
import Vue from 'vue'
import demo from './demo.vue'

new Vue({
  el: '#app',
  render: h => h(demo)
})
```






