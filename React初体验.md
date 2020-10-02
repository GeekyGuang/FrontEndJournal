# React初体验

### 安装create-react-app
```bash
yarn global add create-react-app
```
### 创建项目
```bash
create-react-app react-demo
```
```bash
cd react-demo
  yarn start
```
将无关的东西都删掉，只保留index.js，显示一个hi
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600079692946-77757c12-da2b-42a9-838f-8c522bb9dee8.png#align=left&display=inline&height=479&margin=%5Bobject%20Object%5D&name=image.png&originHeight=479&originWidth=1187&size=66840&status=done&style=none&width=1187)
### CDN方式引入React
先引入react，后引入react-dom
```html
<script src="https://cdn.bootcdn.net/ajax/libs/react/17.0.0-rc.1/umd/react.production.min.js"></script>
<script src="https://cdn.bootcdn.net/ajax/libs/react-dom/17.0.0-rc.1/umd/react-dom.production.min.js"></script>
```
查看是否引入成功, 注意首字母大写
```javascript
console.log(window.React);
console.log(window.React.createElement);
console.log(window.ReactDOM);
console.log(window.ReactDOM.render);
```
cjs和umd的区别
cjs全称CommonJS，是Node.js支持的模块规范
umd是统一模块定义，兼容各种模块规范(含浏览器)
理论上优先使用umd，同时支持Node.js和浏览器
最新的模块规范是使用import和export关键字


### 实现点击按钮 +1
```javascript
// 注意大小写
const React = window.React;
const ReactDom = window.ReactDOM;

const root = document.querySelector("#root");
let n = 0;

// 写成函数，只有执行函数时才会读取最新的n
const App = () =>
  React.createElement("div", { className: "red" }, [
    n,
    React.createElement(
      "button",
      {
        onClick: () => {
          n += 1;
          ReactDom.render(App(), root);
        }
      },
      "+1"
    )
  ]);

// 将App()生成的元素挂载到root
ReactDom.render(App(), root);
```
### 使用JSX
JSX时JS的扩展版，babel-loader解析
写JSX文件
```javascript
import React from 'react'
const App = ()=>{
  return (
    <div>hello</div>
  )
}

export default App
```
import并render
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App.js'
ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```
#### 注意事项

- `<div className="red">n</div>`被转译为`React.createElement('div', {className: 'red', "n"}`
- **标签里面所有JS代码(表达式)**都要用**`{}`**包起来
   - 如果要用变量n，就写`{n}`
   - 如果要用对象，就写`{{ name: 'rose' }}`
- 习惯在return后面加`()`，以免返回undefined
### 条件判断
```javascript
const n = 0

const App = ()=>{
  return (
    <div>
      // 在标签内，JS表达式要用{}包起来
      { n%2===0 ? <div>n是偶数</div> : <div>n是奇数</div> }
    </div>
  )
}
```
### for循环
```javascript
const App = ()=>{
  return (
    <Component numbers={['a','b','c']} />
  )
}

const Component = (props) => {
  return (
    <div>
      { 
        props.numbers.map((item, index)=>{
          return <div> {index}下标值为{item}</div>
        }) 
      }
    </div>

  )
}

```


