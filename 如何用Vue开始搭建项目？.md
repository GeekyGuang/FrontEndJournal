# 如何用Vue开始搭建项目？

### node设置taobao源
```bash
npm install -g nrm --registry=https://registry.npm.taobao.org
nrm use taobao
```
### 安装@vue/cli
```bash
yarn global add @vue/cli@4.1.2
vue --version  # 版本号应该是 4.1.2
```
### 创建项目
```bash
vue create morney
```
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600068630760-0df9f202-b321-43c3-b40d-54672df8d483.png#align=left&display=inline&height=242&margin=%5Bobject%20Object%5D&name=image.png&originHeight=306&originWidth=632&size=23870&status=done&style=none&width=500)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600068709399-ae852f83-9922-4f85-91c8-a4ba15fbaebb.png#align=left&display=inline&height=237&margin=%5Bobject%20Object%5D&name=image.png&originHeight=373&originWidth=787&size=47822&status=done&style=none&width=500)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600068755094-a7d4449c-c2bd-4e39-90be-5ea010d1c0f5.png#align=left&display=inline&height=122&margin=%5Bobject%20Object%5D&name=image.png&originHeight=147&originWidth=601&size=12377&status=done&style=none&width=500)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600068779859-572099c3-a8ba-452b-8b1b-d716d5ba9855.png#align=left&display=inline&height=104&margin=%5Bobject%20Object%5D&name=image.png&originHeight=104&originWidth=487&size=5786&status=done&style=none&width=487)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600068821728-8c62b80e-953e-472f-85f6-95e4ceff68e3.png#align=left&display=inline&height=37&margin=%5Bobject%20Object%5D&name=image.png&originHeight=53&originWidth=722&size=4875&status=done&style=none&width=500)
### 修改默认template
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600070059408-d3184420-1ade-4d61-8a40-c6f172d2d2ab.png#align=left&display=inline&height=878&margin=%5Bobject%20Object%5D&name=image.png&originHeight=878&originWidth=1227&size=124756&status=done&style=none&width=1227)
#### 改成TS类模板
```typescript
<template>
  <div>#[[$END$]]#</div>
</template>

<script lang="ts">
import Vue from 'vue'
import {Component} from 'vue-property-decorator'
@Component
export default class ${COMPONENT_NAME} extends Vue{

}
</script>

<style lang="scss" scoped>

</style>
```
vscode可以用插件：vue vscode snippets 和 Vetur
### JS或TS里使用@
@代表src目录，按住ctrl可访问对应文件
```typescript
<script lang="ts">
  import x from '@/components/test.vue'
</script>
```
### CSS或SCSS使用@
@必须和~一起使用
新建scss文件
```css
$bgcolor: #f60;
```
引入文件
```typescript
<style lang="scss">
@import "~@/assets/styles/test.scss";

#app {
  background: $bgcolor;
}
</style>
```
最新版webstorm里已经配置好了，不会报警
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600071295172-92c0d022-3e07-4afe-93fd-13f0e9623703.png#align=left&display=inline&height=355&margin=%5Bobject%20Object%5D&name=image.png&originHeight=355&originWidth=1121&size=32201&status=done&style=none&width=1121)
