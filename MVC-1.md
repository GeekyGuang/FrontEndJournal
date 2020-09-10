# MVC-1

DRY原则：Don't Repeat Yourself
相同的三行代码写了两遍就应该重构
MVC用来重构代码，减少重复


不学MVC会怎样？

- 写spaghetti code 意大利面条式代码
- 变成外包式程序员
   - 不停重复自己
   - 不会封装，不会造轮子
   - 不能提高自己



### MVC是啥
每个模块可以写成三个对象，分别是M、V、C

- M-Model (数据模型) 负责操作所有数据
- V-View (视图) 负责所有UI界面
- C-Controller (控制器) 负责其他



### 用JS引入CSS,jQuery
#### CSS
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1598883043400-c8152889-a43f-4eea-aba6-46532aff7803.png#align=left&display=inline&height=148&margin=%5Bobject%20Object%5D&name=image.png&originHeight=272&originWidth=772&size=25912&status=done&style=none&width=420)
#### jQuery
在终端输入如下命令
```bash
yarn init -y
yarn add jquery
```
在js里引入jQuery
```javascript
import $ from 'jquery'
```
### 功能1：加减乘除
```javascript
const $add = $('#add')
const $result = $('#result')
const n = localStorage.getItem('n')  // 读取localStorage
$result.text(n || 100)

$add.on('click',()=>{
    let n = parseInt($result.text())  // 获取text内容,转换为数值
    n += 1
    localStorage.setItem('n',n)   // 存入localStorage
    $result.text(n)  // 修改text内容
}) 
```
> 滚动条的宽度在14-19之间

### 功能2：标签页切换
```html
<section id="app2">
  <ol>
    <li>1</li>
    <li>2</li>
  </ol>
  <ol>
    <li>内容1</li>
    <li>内容2</li>
  </ol>
</section>
```


**不要用.css，不要用.show/.hide等操作css的api**
**用.addClass和.removeClass**
**样式与行为分离，JS永远不要操作CSS**
```javascript
import $ from 'jquery'

const $tabBar = $('#app2 .tab-bar');
const $tabContent = $('#app2 .tab-content')

$tabBar.on('click', 'li', (e)=>{
    const $li = $(e.currentTarget)
    const index = $li.index()
    $tabBar.children()
      .eq(index).addClass('selected')
      .siblings().removeClass('selected')
    $tabContent.children()
      .eq(index).addClass('active')
      .siblings().removeClass('active')
})

$tabBar.children().eq(0).trigger('click')  // 默认触发点击事件
```
### 功能3：左晃右晃
```css
#app3 > .square {
    margin-top: 5vw;
    margin-left: 5vw;
    width: 5vw;
    height: 5vw;
    border: 1px solid black;
    transition: transform 1s;
}

#app3 > .square.active {
    transform: translateX(15vw)
}
```
toggleClass，如果class存在则添加，没有则删除
```javascript
import './app3.css'
import $ from 'jquery'

const $square = $('#app3 > .square')

$square.on('click', ()=>{
    $square.toggleClass('active')
})
```
### 功能4： 悬浮变色
alternate交替
```css
#app4 > .circle {
    border: 1px solid grey;
    width: 20vw;
    height: 20vw;
    border-radius: 50%;
}

@keyframes changeColor {
    0%{background: red;}
    100%{background: blue;}
}
#app4 > .circle.active {
    animation: changeColor 1s infinite linear alternate;  
}
```
```javascript
import './app4.css'
import $ from 'jquery'

const $circle = $('#app4 > .circle')

$circle.on('mouseenter', ()=>{
    $circle.addClass('active')
}).on('mouseleave', ()=>{
    $circle.removeClass('active')
})
```


