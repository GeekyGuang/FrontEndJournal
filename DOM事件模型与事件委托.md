# DOM事件模型与事件委托

### 事件模型
DOM事件模型分为事件**捕获**和事件**冒泡**

- 当用户点击按钮，浏览器会从 window 从上向下遍历至用户点击的按钮，逐个触发事件处理函数。(由网景提出)
- 浏览器从用户点击的按钮从下往上遍历至 window，逐个触发事件处理函数。(由微软提出)

W3C标准规定先捕获，后冒泡


#### addEventListener
.addEventListener('click', fn, bool)

- 如果bool不传或为falsy则走冒泡
- 如果bool为true则走捕获



示例：[http://js.jirengu.com/yemebalaqi/1/edit?html,js,output](http://js.jirengu.com/yemebalaqi/1/edit?html,js,output)
(e在事件结束之后就不要再调用)


#### target v.s. currentTarget

- e.target是用户操作的元素
- e.currentTarget是监听的元素



#### 特例
只有一个div被监听，
fn分别在捕获和冒泡阶段监听click事件
用户点击的就是开发者监听的


那么，**谁先监听谁就先执行**


#### 取消冒泡
e.stopPropagation()


查看是否可取消冒泡
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1597751258933-45fcf627-c164-415a-90c9-1c77f5e9d6bd.png#align=left&display=inline&height=182&margin=%5Bobject%20Object%5D&name=image.png&originHeight=324&originWidth=953&size=22818&status=done&style=none&width=535)


#### 阻止滚动
scroll事件不可取消冒泡


JS阻止wheel和touchstart默认动作
```javascript
x.addEventListener('wheel', (e)=>{
  e.preventDefault()
})

x.addEventListener('touchstart',(e)=>{
  e.preventDefault()
})
```
CSS隐藏滚动条
```css
::-webkit-scrollbar {
  width:0 !important;
}
```
### 事件委托
事件委托就是把事件监听放在祖先元素（如父元素、爷爷元素）上。
#### 2种情形

1. 如果有n多个元素要添加点击事件，直接监听它们的祖先，等冒泡时判断target是不是其中的一个

示例：[http://js.jirengu.com/cotal/1/edit?html,js,output](http://js.jirengu.com/cotal/1/edit?html,js,output)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1597753070537-eea14031-4320-4b97-8ac3-45d169f315f6.png#align=left&display=inline&height=188&margin=%5Bobject%20Object%5D&name=image.png&originHeight=376&originWidth=1473&size=107491&status=done&style=none&width=736.5)

2. 要监听不存在的元素的点击事件，监听祖先，等点击时看是不是要监听的元素

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1597753422225-937bfe17-5666-4f17-b5b0-99091b49a176.png#align=left&display=inline&height=212&margin=%5Bobject%20Object%5D&name=image.png&originHeight=424&originWidth=1494&size=78383&status=done&style=none&width=747)
#### 优点

- 省监听数(内存)
- 可以监听动态元素



### 封装
```javascript
on('click', '#div1', 'button', ()=>{
  console.log('button 被点击了')
})

function on(eventType, element, selector, fn){
  if(!(element instanceof Element)){
    element = document.querySelector(element)
  }
  element.addEventListener(eventType, (e)=>{
    const t=e.target
    if(t.matches(selector)){
      fn(e)
    }
  })
}
```






