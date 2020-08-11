# DOM编程

JS不能直接操作网页，通过DOM(Document Object Model)
document是挂在window上的对象


DOM很难用！！！


### 获取元素(标签)

- window.xxx或者直接xxx (xxx为id名)
- document.getElementById('xxx')
- document.getElementsByTagName('div')[0]       // 伪数组
- document.getElementsByClassName('red')[0]
- document.querySelector('#idxxx')    // 只要是CSS的选择器就行
- document.querySelectorAll('.red')[0]



#### 用哪一个？

- 工作中用document.querySelector('#idxxx') 和 document.querySelectorAll('.red')[0]
- demo中用window.xxx或者直接xxx (xxx为id名)
- 兼容IE才用getElement(s)Byxxx



#### 获取特定元素

- 获取html元素：document.documentElement
- 获取head元素：document.head
- 获取body元素：document.body
- 获取窗口(不是元素)：window
- 获取所有元素：document.all

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596969802727-5d3228f0-18b1-47a1-b8b6-8f8adacb2ba8.png#align=left&display=inline&height=45&margin=%5Bobject%20Object%5D&name=image.png&originHeight=90&originWidth=710&size=38244&status=done&style=none&width=355)
document.all是IE发明的, 在IE里为真，其他浏览器里为假
是第6个falsy值


#### div6层原型
```javascript
let div = document.querySelectorAll('div')[0]

div.__proto__ === HTMLDivElement.prototype
true
HTMLDivElement.prototype.__proto__ === HTMLElement.prototype
true
HTMLElement.prototype.__proto__ === Element.prototype
true
Element.prototype.__proto__ === Node.prototype
true
Node.prototype.__proto__ === EventTarget.prototype
true
EventTarget.prototype.__proto__ === Object.prototype
true
```
#### Node包含以下几种
x.nodeType

- 1 Element
- 3 Text
- 8 Comment
- 9 Document
- 11 DocumentFragment



### 增删改查
#### 增
##### 创建标签节点
let div1 = document.createElement('div')
document.createElement('style')
document.createElement('script')
document.createElement('li')


##### 创建文本节点
text1 = document.createTextNode('你好')


##### 标签里插入文本
div1.appendChild(text1)
div1.innerText = '你好'
div1.textContent = '你好'


##### 插入页面中
document.body.appendChild(div1)
> 一个创建的元素只能出现在一个地方

#### 删
旧方法：parentNode.removeChild(childNode)
新方法：childNode.remove()


一个node被移出页面(DOM树)，还能再次回到页面中
div1.remove()
document.body.appendChild(div1)


#### 改属性
##### 写标准属性
改class: div.className = 'red blue' (全覆盖)
改class: div.classList.add('red')
改style: div.style = 'width:100px; color: blue;'
改style的一部分：div.style.backgroundColor = 'white'
改data-*属性： div.dataset.x = 'xxx'       添加了 data-x属性


##### 读属性
div.classList/a.href
div.getAttribute('class')  /  a.getAttribute('href')


##### 改事件处理函数
div.onclick默认为null
div.onclick = fn
浏览器这样调用：fn.call(div, event)
div会被当做this
event包含了点击事件的所有信息


div.addEventListener是div.onclick的升级版


##### 改内容
改文本
div.innerText = 'xxx'
div.textContent = 'xxx'


改HTML内容
div.innerHTML = '<strong>重要内容</strong>'


改标签
div.innerHTML = ''
div.appendChild(div2)


改父节点
newParent.appendChild(div)
直接给一个附加到一个新节点就可以


#### 查
父节点：node.parentNode或者node.parentElement  
爷爷： node.parentNode.parentNode
子代： node.childNodes 或者 node.children
兄弟姐妹： node.parentNode.childNodes 或者 node.parentNode.children
查看老大： node.firstChild
老幺： node.lastChild
上一个sibling: node.previousSibling
下一个sibling: node.nextSibling


**childNodes与children的区别**：
childNodes 属性返回所有的节点，包括文本节点(包括换行和空格)、注释节点；
children 属性只返回元素节点；


### DOM操作跨线程

- JS引擎不能操作页面，只能操作JS
- 渲染引擎不能操作JS, 只能操作页面
- 浏览器发现JS在body里添加了一个div1,就会通知渲染引擎在页面里新增一个div元素































