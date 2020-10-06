# 开发money组件的css技巧及模块化

### html
先按结构写html，
每个模块用div包起来，给class名
再逐一细化每个模块
写html先不要管样式


### CSS
reset.scss单独一个文件
@import要用分号结尾


#### font和全局变量
搜索 **"font.css" 中文**
[https://zenozeng.github.io/fonts.css/](https://zenozeng.github.io/fonts.css/)
复制font-familiy的值
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600307352631-807d732e-ad15-4082-ae06-30094a1d4f74.png#align=left&display=inline&height=181&margin=%5Bobject%20Object%5D&name=image.png&originHeight=362&originWidth=1802&size=84361&status=done&style=none&width=901)
新建helper.scss文件，定义变量**$font-hei**的值为复制的值，在其他文件中引用，设置body的font-family为$font-hei，
楷体和宋体也引入，方便后面用到($font-kai, $font-song)
line-height一般是1.5
color一般用 #333, 不要用纯黑色
```css
@import "~@/assets/style/helper.scss";
@import "~@/assets/style/reset.scss";

body{
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  line-height: 1.5;
  font-family: $font-hei;
  color: #333;
}
```
helper.scss只放**变量**或**函数**，不要放**class**的样式

`**ctrl + shift + F**`全局搜索


body和input不会继承body的字体
```css
button, input {
  font: inherit;
}
```
#### 让文字垂直居中
如果确定只有一行，则让height和line-height相等即可

#### button
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600311135768-d5b4dc42-ae41-4da2-8d5e-da96b6fd5b9b.png#align=left&display=inline&height=63&margin=%5Bobject%20Object%5D&name=image.png&originHeight=63&originWidth=160&size=2496&status=done&style=none&width=160)
```css
button {
  background: transparent;  /* 默认样式很丑 */
  border: none;
  color: #999;
  border-bottom: 1px solid;  /* border不给颜色则和color相同 */
  padding: 0 4px;  /* 让border比文字长  */
}
```


webstorm 直接另起一行的快捷键`** shift + enter**`


#### 去除input选中时的边框
```css
:focus {
  outline: none;
}
```


#### 让文字水平居中
```css
text-align: center;
```


#### ::before和::after不要忘了content
```css
&.selected{
  &::before{
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    height: 4px;
    width: 100%;
    background: #333;
  }
}
```


#### 等宽字体
```css
font-family: Consolas, monospace;
```


当用flex布局行不通时，改用float


父元素要加clearfix
```css
.clearfix::after {
  content: '';
  display: block;
  clear: both
}
```
#### SCSS使用继承@extend和选择器占位符%x
在helper.scss里写
```css
// place holder
// %clearFix只是一个占位符，其他选择器会替换掉这里
%clearFix {
  content: '';
  display: block;
  clear: both;
}
```
使用继承
```css
.buttons {
  @extend %clearFix;
}
```
#### 使用颜色函数
```css
button {
   $bg: #f2f2f2;   // 块级作用域

    &:nth-child(1) {
      background: $bg;
    }

    &:nth-child(2), &:nth-child(5) {
      background: darken($bg, 4%);
    }

    &:nth-child(3), &:nth-child(6), &:nth-child(9) {
      background: darken($bg, 4*2%);
    }

    &:nth-child(4), &:nth-child(7), &:nth-child(10) {
      background: darken($bg, 4*3%);
    }

    &:nth-child(8), &:nth-child(11), &:nth-child(13) {
      background: darken($bg, 4*4%);
    }

    &:nth-child(14) {
      background: darken($bg, 4*5%);
    }

    &:nth-child(12) {
      background: darken($bg, 4*6%);
    }
}
```
#### 内阴影
**阴影可以添加多个，用逗号分隔**
**inset**代表内阴影
**fade_out**函数改变颜色透明度
```css
box-shadow: inset 0 -3px 3px -3px fade_out(black, .75),
    inset 0 3px 3px -3px fade_out(black, .75);
```
#### 使用classPrefix
当要用props给一个组件传class时，为避免参数过多，可以使用classPrefix方法
```vue
<template>
  <div class="content-wrapper"  :class="`${classPrefix}-wrapper`">
    <div class="content" :class="`${classPrefix}-content`">
      <slot></slot>
    </div>
    <Nav/>
  </div>
</template>

<script lang="ts">
export default {
  name: 'Layout',
  props:['classPrefix']
};
</script>
```
#### 在vue文件中可以有多个<style>标签
```vue
<Layout class-prefix="layout">  // 给classPrefix传值
...
</Layout>

// 定义全局style，但会存在相互覆盖的问题，可使用deep解决
<style lang="scss">
.layout-content {
  display: flex;
  flex-direction: column-reverse;
}
</style>
```
### 模块化
代码超过150行就要模块化，把大组件拆分成小模块封装到components里，且放到同一个文件夹
别忘了组件名**首字母大写**




