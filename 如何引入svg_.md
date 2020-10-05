# 如何引入svg?

在[https://www.iconfont.cn/](https://www.iconfont.cn/)下载svg格式图标，在项目的assets目录新建icons文件夹，导入图标


import 图片报错
```javascript
import x from '@/assets/icons/label.svg'
```
解决办法: 在d.ts文件里添加
```javascript
declare module '*.svg' {
  const content: string;
  export default content;
}
```
### 使用svg-sprite-loader
安装
```bash
npm install svg-sprite-loader -D
或
yarn add --dev svg-sprite-loader -D
```


在vue.config.js中配置以下代码
```javascript
const path = require('path');
module.exports = {
   lintOnSave: false,
   chainWebpack: config => {
       const dir = path.resolve(__dirname, 'src/assets/icons')
       config.module
           .rule('svg-sprite')
           .test(/\.svg$/)
           .include.add(dir).end()
           .use('svg-sprite-loader').loader('svg-sprite-loader').options({extract: false}).end()
       config.plugin('svg-sprite').use(require('svg-sprite-loader/plugin'), [{plainSprite: true}])
       config.module.rule('svg').exclude.add(dir)
   }
};
```


在需要使用到svg的文件中template部分写以下代码
```vue
<template>
    <svg>
         <use xlink:href="#xxx"/>
    </svg>
</template>
```
### eslint报错处理
解决方法一
在eslintrc.js文件的rules里添加
```javascript
  rules: {
    '@typescript-eslint/no-var-requires':0,
  },
```
解决方法二
用webstorm的提示添加注释
```javascript
// eslint-disable-next-line @typescript-eslint/no-var-requires
const path = require('path')
```
解决方法三
使用import(node10一下不支持)
```javascript
import path from 'path'
```
### import整个目录
svg-sprite-loader会把svg变成symbol，symbol对应的id为label，并在symbol外套一个svg，在body里生成。
如要使用多个svg，那在文件里添加几次svg，使用几次use，在ts里import几次即可，但这样很麻烦，可以引入一个目录，把ts里的代码改成如下


```typescript
<script lang="ts">
  let importAll = (requireContext: __WebpackModuleApi.RequireContext) => requireContext.keys().forEach(requireContext);
  try {
    importAll(require.context('../assets/icons', true, /\.svg$/));//使用require
  } catch (error) {
    console.log(error);
  }
  export default {
    name: 'Icon'
  };
</script>
```
### SVG的坑
如果svg里自带颜色`fill="red"`，就无法用css更改颜色，可以把svg中的fill删掉，但svg太多，不可能一个一个去删。
另一个办法是安装**svgo-loader**
`**yarn add --dev svgo-loader**`
并在vue.config.js的config.module下添加两句代码


```javascript
config.module
            .use('svgo-loader').loader('svgo-loader')
            .tap(options=>({...options,plugins:[{removeAttrs:{attrs:'fill'}}]})).end();
```
**
### 在React项目中同样要做这些操作
但是在安装svg-sprite-loader和svgo-loader之前要先yarn eject，生成webpack.config.js，之后在该文件module→rules→oneOf中添加以下代码


```javascript
{
  test: /\.svg$/,
  use: [
    { loader: 'svg-sprite-loader', options: {} },
    { loader: 'svgo-loader', options: {} }
  ]
}
```
同样引入svg也要添加下面两行代码


```javascript
let importAll = (requireContext: __WebpackModuleApi.RequireContext) => requireContext.keys().forEach(requireContext);
  try {importAll(require.context('icons', true, /\.svg$/));} catch (error) {console.log(error);}
```
这时 __WebpackModuleApi和require会报错，安装@types/webpack-env(`yarn add --dev @types/webpack-env`)错误就会消除


### 封装icon
新建icon.vue
```vue
<template>
  <svg class="icon">
    <use :xlink:href="'#'+name"/>  <!-- 动态绑定 -->
  </svg>
</template>

<script lang="ts">
const importAll = (requireContext: __WebpackModuleApi.RequireContext) => requireContext.keys().forEach(requireContext);
try {importAll(require.context('../assets/icons', true, /\.svg$/));} catch (error) {console.log(error);}

export default {
  props:['name'],   // 用props传图标名
  name: 'icon'
};
</script>

<style lang="scss" scoped>
  /* 拷贝iconfont官网帮助文档里的css */
.icon {
  width: 1em; height: 1em;
  vertical-align: -0.15em;
  fill: currentColor;
  overflow: hidden;
}
</style>
```
在main.js注册全局component后，使用组件
```vue
<template>
  <div class="nav">
    <router-link to="/labels">
      <icon name="label"/>
      标签
    </router-link>
  </div>
</template>

// 可通过.icon设置样式
<style>
  .icon {
    width: 32px;
    height: 32px;
  }
</style>
```
### 
