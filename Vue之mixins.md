# Vue之mixins

directives的作用是减少DOM操作的重复
mixins的作用是减少data、methods、钩子的重复


### 创建mixin文件
将重复的data、methods、钩子放到一个js文件内
```javascript
const log = {
  data() {
    return {
      name: undefined,
      time: undefined
    };
  },
  created() {
    if (!this.name) {
      throw new Error("need name");
    }
    this.time = new Date();
    console.log(`${this.name}出生了`);
  },
  beforeDestroy() {
    const now = new Date();

    console.log(`${this.name}死亡了，共生存了 ${now - this.time} ms`);
  }
};

export default log;
```
### 在其他文件中引入mixins
```javascript
<template>
  <div>Child1</div>
</template>

<script>
// 引入文件
import log from "../mixins/log.js";
export default {
  data() {
    return {
      name: "Child1"
    };
  },
  created() {
    console.log("Child 1 的 created");
  },
  // 设置mixins
  mixins: [log]
};
</script>
```
### 选项合并
当组件和混入对象含有同名选项时，这些选项将以恰当的方式进行“合并”。

- 数据对象在内部会进行递归合并，并在发生冲突时以组件数据优先。
- 同名钩子函数将合并为一个数组，因此都将被调用。另外，混入对象的钩子将在组件自身钩子**之前**调用。
- 值为对象的选项，例如 `methods`、`components` 和 `directives`，将被合并为同一个对象。两个对象键名冲突时，取组件对象的键值对。





