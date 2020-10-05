# 如何使用slot？

做项目时，可以将相同的部分都写入components里，通过slot在组件里引入不相同的部分
写模板
```vue
<template>
  <div class="content-wrapper">
    <div class="content">
      <slot></slot>   <!-- slot会被传入的东西替换 -->
    </div>
    <Nav/>
  </div>
</template>
```
给slot传值
```vue
<template>
  <Layout>
    <p>Money.vue</p>  <!-- 这部分会替换slot -->
  </Layout>
</template>
```


