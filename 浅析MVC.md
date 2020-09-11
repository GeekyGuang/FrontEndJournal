# 浅析MVC

### 什么是MVC？
- M是modal(数据模型)的简称，它是用于操作所有数据
- V是view(视图)的简称，它是用于负责所有UI界面
- C是controller（控制器）的简称，它负责其他
### MVC的用途
再说它的用途之前，我们要说一说面条式代码。我知道对于一个初学者来说突然告诉你面条式代码大家都很难接受，其实也没有什么的，我们学习阶段所写的代码基本都是面条式的。
所谓的面条式代码：一团糟、代码重复率高，为此就有人发明了MVC框架。它的用途就是通过数据处理、事件绑定、重新渲染等模块化方式来把这一团糟糕的代码进行逐步简化成万金油的代码。
例
一般我们在进行页面开发都是在文件SRC下面建立index.html、main.js、style.css；今天我们通过MVC将传统的设计方式改成模块化。
```html
<body>
<section id="app">
<div class="output">
<span class="numbers">n</span>
</div>
<div class="actions">
<button class="add">+1</button>
<button class="reduce">-1</button>
<button class="mul">*2</button>
<button class="device">/2</button>
</div>
</body>
```
通过模块化改写，将页面中每一个板块分成一个个独立的模块；单独写它的Css、JS最后在main.js中将这些模块引入即可。如：
```javascript
import $ from 'jQuery'//引入jQuery
import './app.css'//引入独立的css
import './app.js'//引入独立的JS
```
上面这个引入还可以简写，我们把独立的css放在JS文件中，在JS文件开头引入css
```javascript
import './app.css'
```
最后，将整个JS文件节点导出
```javascript
export default x
```

---

上面我们说了模块化，将一个大的整体进行细分，自己写自己板块的css、JS；这样细分的好处在于某一个模块如果有所改动也不会影响其它模块的代码。下面我们继续通过MVC来将其代码进一步的改写。
#### M数据
获取数据n；对数据暴露出增删改查四个API，用于后期操作数据。
```javascript
const m = {
  data: {
    n: parseInt(localStorage.getItem('n'))
  },//获取数据
  create() {},//增
  delete() {},//删
  update(data) {
    Object.assign(m.data, data)
    eventBus.trigger('m:updated')
    localStorage.setItem('n', m.data.n)
  },//改
  get() {}
}//查
}
```
#### V视图
视图主要是渲染到页面，所以我们将之前的inedx.html放到了V上。
```javascript
const v = {
  el: null,//接受一个容器
  html: `//生成HTML
  <div>
    <div class="output">
      <span id="number">{{n}}</span>
    </div>
    <div class="actions">
      <button id="add1">+1</button>
      <button id="minus1">-1</button>
      <button id="mul2">*2</button>
      <button id="divide2">÷2</button>
    </div>
  </div>
`,
  init(container) {
    v.el = $(container)
  },//初始化容器
  render(n) {
    if (v.el.children.length !== 0) v.el.empty()
    $(v.html.replace('{{n}}', n))
      .appendTo(v.el)
  }//通过if else判断容器的后代是否存在进行增删，最后渲染到页面
}
```
#### C控制器
C里面主要是放一些事件的操作，如：click、on等等；这里面又设计到EventBus、表驱动编程等等。
```javascript
const c = {
//初始化容器
  init(container) {
    v.init(container)
    v.render(m.data.n) // view = render(data)
    c.autoBindEvents()//自动绑定事件
    eventBus.on('m:updated', () => {
      console.log('here')
      v.render(m.data.n)
    })//监听数据的变化，重新渲染到页面
  },
//事件太多，通过哈希表来一一列出，也正是我们所说的表驱动编程
  events: {
    'click #add1': 'add',
    'click #minus1': 'minus',
    'click #mul2': 'mul',
    'click #divide2': 'div',
  },
//每个事件点击对应着数据变化的操作函数
  add() {
    m.update({n: m.data.n + 1})
  },
  minus() {
    m.update({n: m.data.n - 1})
  },
  mul() {
    m.update({n: m.data.n * 2})
  },
  div() {
    m.update({n: m.data.n / 2})
  },
  autoBindEvents() {
    for (let key in c.events) {
      const value = c[c.events[key]]
      const spaceIndex = key.indexOf(' ')
      const part1 = key.slice(0, spaceIndex)
      const part2 = key.slice(spaceIndex + 1)
      v.el.on(part1, part2, value)
    }
  }
}
export default c
```
上面就是我们把index.html、css、js通过MVC进行改写，让代码由面条式变成了万金油（也就是模块化）；下面我们来说说C里面涉及到EventBus、表驱动编程。
#### EventBus
一种设计模式或框架，主要用于组件/对象间通信的优化简化。
EventBus里面涉及到很多API，下面我就列举几个常用，并对它们的用法进行分析。这个EventBus我们在运用的时候通常是这么来引入的：
```javascript
const eventBus = $(window)
```
放在window上的，但是我今天想说的是这样用起来不爽，每一个模块一开始都要通过这样的方式来引入它；我们是否可以考虑通过继承的方式把它放在原型上呢？
```
import $ from 'jquery'
class EventBus {
  constructor() {
    this._eventBus = $(window)
  }
  on(eventName, fn) {
    return this._eventBus.on(eventName, fn)
  }
  trigger(eventName, data) {
    return this._eventBus.trigger(eventName, data)
  }
  off(eventName, fn) {
    return this._eventBus.off(eventName, fn)
  }
}
export default EventBus
```
我们把EventBus直接放在原型是上，并暴露出一个节点方便使用。
Modal继承Eventbus
```javascript
import EventBus from './EventBus'
class Model extends EventBus {
  constructor(options) {
    super()
    const keys = ['data', 'update', 'create', 'delete', 'get']
    keys.forEach((key) => {
      if (key in options) {
        this[key] = options[key]
      }
    })
  }
  create() {
    console && console.error && console.error('你还没有实现 create')
  }
  delete() {
    console && console.error && console.error('你还没有实现 delete')
  }
  update() {
    console && console.error && console.error('你还没有实现 update')
  }
  get() {
    console && console.error && console.error('你还没有实现 get')
  }
}
export default Model
```
View继承Eventbus
```javascript
import $ from 'jquery'
import EventBus from './EventBus'
class View extends EventBus{
  // constructor({el, html, render, data, eventBus, events}) {
  constructor(options) {
    super() // EventBus#constructor()
    Object.assign(this, options)
    this.el = $(this.el)
    this.render(this.data)
    this.autoBindEvents()
    this.on('m:updated', () => {
      this.render(this.data)
    })
  }
  autoBindEvents() {
    for (let key in this.events) {
      const value = this[this.events[key]]
      const spaceIndex = key.indexOf(' ')
      const part1 = key.slice(0, spaceIndex)
      const part2 = key.slice(spaceIndex + 1)
      this.el.on(part1, part2, value)
    }
  }
}
export default View
```
EventBus中涉及到了三个API，分别是：on、trigger、off;
on:监听事件的变化
监听数据的变化，如果数据有变化，直接render（再次将变化后的数据渲染到页面）
```javascript
this.on('m:updated', () => {
      this.render(this.data)
    })
```
tirgger:自动触发事件
```javascript
update(data) {
    Object.assign(m.data, data)//把传进来的data直接放在m.data上
    eventBus.trigger('m:updated')//通过trigger自动更新数据
    localStorage.setItem('n', m.data.n)//储存数据
```
off：关闭的意思
#### 表驱动编程
表驱动编程就是将诸多事件进行简化的一种写法，因为这些事件涉及到很多的代码重复问题。
例
```javascript
import "./app1.css";
import $ from "jquery";
const $button1 = $("#add1");
const $button2 = $("#minus1");
const $button3 = $("#mul2");
const $button4 = $("#divide2");
const $number = $("#number");
const n = localStorage.getItem("n");
$number.text(n || 100);
$button1.on("click", () => {
  let n = parseInt($number.text());
  n += 1;
  localStorage.setItem("n", n);
  $number.text(n);
});
$button2.on("click", () => {
  let n = parseInt($number.text());
  n -= 1;
  localStorage.setItem("n", n);
  $number.text(n);
});
$button3.on("click", () => {
  let n = parseInt($number.text());
  n *= 2;
  localStorage.setItem("n", n);
  $number.text(n);
});
$button4.on("click", () => {
  let n = parseInt($number.text());
  n /= 2;
  localStorage.setItem("n", n);
  $number.text(n);
});
```
这段代码中，我们眯着眼仔细观察，发现很多重复代码。如：let n = parseInt($number.text());localStorage.setItem("n", n);我们通过表驱动编程将其逐步的简化后
```javascript
events: {
    'click #add1': 'add',
    'click #minus1': 'minus',
    'click #mul2': 'mul',
    'click #divide2': 'div',
  },
//每个事件点击对应着数据变化的操作函数
  add() {
    m.update({n: m.data.n + 1})
  },
  minus() {
    m.update({n: m.data.n - 1})
  },
  mul() {
    m.update({n: m.data.n * 2})
  },
  div() {
    m.update({n: m.data.n / 2})
  },
  autoBindEvents() {
    for (let key in c.events) {
      const value = c[c.events[key]]
      const spaceIndex = key.indexOf(' ')
      const part1 = key.slice(0, spaceIndex)
      const part2 = key.slice(spaceIndex + 1)
      v.el.on(part1, part2, value)
    }
  }
}
export default c
```
通过哈希表将事件全部抽出来后代码简洁许多，且重复率也减少；这就是表驱动编程。
这种方法的好处：
提高了程序的可读性。一个消息如何处理，只要看一下驱动表就知道，非常明显。减少了重复代码。这种方法的代码量肯定比第一种少。为什么？因为它把一些重复的东西：switch分支处理进行了抽象，把其中公共的东西——根据三个元素查找处理方法抽象成了一个函数GetFunFromDriver外加一个驱动表。
程序有一个明显的主干。
降低了复杂度。通过把程序逻辑的复杂度转移到人类更容易处理的数据中来，从而达到控制复杂度的目标。


