# CSS动画

### 移动div
#### 方案一
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595571436257-99d5eab1-5c99-4024-bbe7-61a4c8f96a22.png#align=left&display=inline&height=364&margin=%5Bobject%20Object%5D&name=image.png&originHeight=364&originWidth=1432&size=57581&status=done&style=none&width=1432)
间隔函数：setInterval(函数，间隔时间)   
箭头函数：`()=>{ do something }`

#### 方案二

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595572540970-3de25ad4-0328-4be2-b091-4be0f171b1b9.png#align=left&display=inline&height=307&margin=%5Bobject%20Object%5D&name=image.png&originHeight=307&originWidth=1284&size=48643&status=done&style=none&width=1284)
延时函数：setTimeout(函数，间隔时间)

#### 调出rendering(渲染)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595571792254-a2c64e02-3555-4e7b-ae12-723a82d0b7f3.png#align=left&display=inline&height=445&margin=%5Bobject%20Object%5D&name=image.png&originHeight=582&originWidth=526&size=62956&status=done&style=none&width=402)
### 浏览器渲染原理
#### 渲染步骤

- 根据HTML构建HTML树(DOM)
- 根据CSS构建CSS树(CSSOM)
- 将两棵树合并成一颗渲染树(render tree)
- Layout布局(文档流、盒模型、计算大小和位置)
- Paint绘制(把边框颜色、文字颜色、阴影等画出来)
- Composite合成(根据层叠关系展示画面)



#### 用JS更新样式

- div.style.background = 'red'
- div.style.background = 'none'
- div.classList.add('red')  // 推荐
- div.remove()  // 删掉节点



#### 三种渲染更新方式
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595760035758-62e8a756-9417-4b45-8ff6-eebd165406a6.png#align=left&display=inline&height=387&margin=%5Bobject%20Object%5D&name=image.png&originHeight=727&originWidth=1039&size=359309&status=done&style=none&width=553)

1. div.remove()触发当前消失，其他元素relayout，全走
1. 改变背景色，跳过layout
1. 改变transform, 跳过layout和paint



查询网站：[https://csstriggers.com/](https://csstriggers.com/)


#### CSS动画优化

- JS: 使用requestAnimationFram代替setTimeout或setInterval
- CSS: 使用will-change或translate



### transform
#### translate 位移
```css
transform: translateX(100px);
transform: translateY(100px);

transform: translateZ(100px);
/* Z轴位移要配合父元素上加上perspective透视点 */
.wrapper{perspective: 100px}  /* 透视点在父元素中心距屏幕向内100px */

/* 简写 */
transform: translate(100px, 100px);
transform: translate3d(100px, 100px, 100px);

/* 也可用百分数，表示自身宽度/高度的百分比 */
transform: translate(50%, 60%);
```


transform: translate(-50%, -50%)用于居中定位
```css
#demo {
  border: 1px solid red;
  width: 100px;
  height: 100px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%)
}

.wrapper {
  border: 1px solid blue;
  height: 500px;
  position: relative;
}
```


#### scale 缩放
```css
transform: scale(1.2); /* 放大 */
transform: scaleX(1.2);
transform: scaleY(1.2);
```
#### rotate 旋转
```css
transform: rotate(45deg); /* 默认绕Z轴 */
transform: rotateX(45deg); /* 绕X轴 */
transform: rotateY(45deg);
```
#### skew 变形
```css
transform: skew(45deg);
```
#### 综合使用
```css
transform: translate(50%) skew(45deg) rotate(30deg);
```
### 制作红心
demo1: [http://js.jirengu.com/nosic/2/edit?html,css,output](http://js.jirengu.com/nosic/2/edit?html,css,output)
demo2: [http://js.jirengu.com/namuh/5/edit?html,css,output](http://js.jirengu.com/namuh/5/edit?html,css,output)


### transition 过渡
**`transition` **[CSS](https://developer.mozilla.org/en/CSS) 属性是 [`transition-property`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition-property)，[`transition-duration`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition-duration)，[`transition-timing-function`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition-timing-function) 和 [`transition-delay`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition-delay) 的一个[简写属性](https://developer.mozilla.org/en-US/docs/CSS/Shorthand_properties)。
```css
transition: width 1s linear 100ms;  /* linear 匀速 ease 先快后慢 */
transition: all 1s;
```
display:none到block不能过渡
visibility:hidden; 到 visibility: visible; 可以
opacity透明度不推荐


### animation
[CSS](https://developer.mozilla.org/zh-CN/docs/Web/CSS) **animation** 属性是 [`animation-name`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-name)，[`animation-duration`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-duration), [`animation-timing-function`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-timing-function)，[`animation-delay`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-delay)，[`animation-iteration-count`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-iteration-count)，[`animation-direction`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-direction)，[`animation-fill-mode`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-fill-mode) 和 [`animation-play-state`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-play-state) 属性的一个简写属性形式。


step1：设置关键帧@keyframes
```css
/* 方法一 */
@keyframes xxx {
  0% {
    transform: scale(1.0);
  }
  100% {
    transform: scale(1.5);
  }
}

/* 方法二 */
@keyframes xxx {
  from {
    transform: margin-left: -20%;
  }
  to {
    transform: margin-left: 100%;
  }
}

```
step2: 添加animation
```css
.className {
  animation: xxx 800ms infinite alternate forwards;
}
```


