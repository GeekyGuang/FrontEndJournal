# MVC-2

### toggleClass
toggleClass可以指定第二个参数，显式的指明要添加还是删除class
```javascript
import './app3.css'
import $ from 'jquery'

const $square = $('#app3 > .square')
const active = localStorage.getItem('app3.active') === 'yes'

$square.toggleClass('active', active)

$square.on('click', ()=>{
    if ($square.hasClass('active')) {
        $square.removeClass('active')
        localStorage.setItem('app3.active', 'no')   // 存到localStorage里的是字符串
    } else {
        $square.addClass('active')
        localStorage.setItem('app3.active', 'yes')
    }
})
```
### 最小知识原则
引入一个模块只需要引入一个js
模块化提供基础
#### 代价
这样做会使得页面一开始是空白的，没内容没样式
解决方法：菊花，骨架，占位内容
### MVC

- 数据相关放m
- 试图相关放v
- 其他放c



事件总线 eventBus


