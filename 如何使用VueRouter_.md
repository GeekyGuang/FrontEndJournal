# 如何使用VueRouter?

#### 将页面文件创建在views文件夹
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600143478417-e5f0c644-0072-417d-915f-cf078e9f4720.png#align=left&display=inline&height=137&margin=%5Bobject%20Object%5D&name=image.png&originHeight=183&originWidth=257&size=6386&status=done&style=none&width=193)
#### 在router目录的index.ts文件里填写路径
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600143543937-5fd5134e-f30e-418d-8423-69df3d87af57.png#align=left&display=inline&height=51&margin=%5Bobject%20Object%5D&name=image.png&originHeight=78&originWidth=287&size=2596&status=done&style=none&width=186)
```javascript
const routes: Array<RouteConfig> = [
  {
    path: '/',       // 根目录自动跳转/money
    redirect: '/money'
  },
  {
    path: '/money',
    component: Money
  },
  {
    path: '/labels',
    component: Labels
  },
  {
    path: '/statistics',
    component: Statistics
  }

];
```
#### 使用router-view显示页面，router-link跳转
```vue
<template>
  <div>
    <router-view/>
    <hr>
    <router-link to="/labels">标签</router-link> |
    <router-link to="/money">记账</router-link> |
    <router-link to="/statistics">统计</router-link>
  </div>
</template>
```
#### 将导航栏注册为全局组件
```javascript
import Nav from '@/components/Nav.vue';
Vue.component('Nav', Nav)
```
#### 添加404页面
在路由最后面添加路径，路由时从上到下一次判断的
```javascript
  {
    path: '*',
    component: NotFound
  }
```
#### fixed还是flex?
手机上千万不要用fixed
Vue<style>标签里**scoped**代表样式只在当前页面有效
#### 
