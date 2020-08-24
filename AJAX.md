# AJAX

用JS发请求和收响应，这就是AJAX的全部内容。


浏览器提供了一个XMLHttpRequest构造函数
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1598148805940-84d0c567-76a4-4404-b7e7-b3880ca7db44.png#align=left&display=inline&height=99&margin=%5Bobject%20Object%5D&name=image.png&originHeight=150&originWidth=573&size=16675&status=done&style=none&width=377)
### 准备一个server.js
### [server.js](https://www.yuque.com/attachments/yuque/0/2020/js/1753813/1598149042614-4ef4956d-9e91-4da7-a412-8f24f2b882f7.js?_lake_card=%7B%22status%22%3A%22done%22%2C%22source%22%3A%22transfer%22%2C%22src%22%3A%22https%3A%2F%2Fwww.yuque.com%2Fattachments%2Fyuque%2F0%2F2020%2Fjs%2F1753813%2F1598149042614-4ef4956d-9e91-4da7-a412-8f24f2b882f7.js%22%2C%22name%22%3A%22server.js%22%2C%22ext%22%3A%22js%22%2C%22size%22%3A3351%2C%22id%22%3A%22AJiO3%22%2C%22card%22%3A%22file%22%7D)
安装node-dev
```bash
yarn global add node-dev
```
使用node-dev
(好处：会自动重启)
```bash
node-dev server.js 8888
```
### 添加index.html/main.js路由
```javascript

  if(path === '/index.html'){
    response.statusCode = 200
    response.setHeader('Content-Type', 'text/html;charset=utf-8')
    response.write(`
    <!DOCTYPE html>
    <html>
    <head>
      <title>ajax</title>
    </head>
    <body>AJAX demo
      <script src="/main.js"></script>
    </body>
    </html>
    `)
    response.end()
  }else if(path === '/main.js'){
    response.statusCode = 200
    response.setHeader('Content-Type', 'text/javascript;charset=utf-8')
    response.write(`
    console.log("我是JS")
    `)
    response.end()
  }else{
    response.statusCode = 404
    response.setHeader('Content-Type', 'text/html;charset=utf-8')
    response.write(`你输入的路径不存在对应的内容`)
    response.end()
  }
```
#### 改成读取文件
```javascript
// 略
    response.setHeader('Content-Type', 'text/html;charset=utf-8')
    const string = fs.readFileSync('public/index.html')
    response.write(string)
// 略
    response.setHeader('Content-Type', 'text/javascript;charset=utf-8')
    const string = fs.readFileSync('public/main.js')
    response.write(string)
// 略
```
### 挑战1：加载CSS
```html
<!DOCTYPE html>
<html>
<head>
  <title>ajax</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>AJAX demo 2</h1>
  <script src="/main.js"></script>
</body>
</html>
```
```javascript
if(path === '/style.css'){
    response.statusCode = 200
    response.setHeader('Content-Type', 'text/css;charset=utf-8')
    const string = fs.readFileSync('public/style.css')
    response.write(string)
    response.end()
  }
```
#### 用ajax实现
```javascript
// 1. 创建HttpRequest()对象
const request = new XMLHttpRequest()
// 2. 调用对象的open方法，只传2个参数
request.open('GET', '/style.css')
// 3. 监听onload和onerror事件
request.onload = ()=>{
  console.log(request.response)
  // 创建style节点
  const style = document.createElement("style")
  // 填写返回的内容
  style.innerHTML = request.response
  // 插到head里
  document.head.appendChild(style)
}
request.onerror = () =>{
  console.log("失败了")
}

// 4. 调用send方法，发送请求
request.send()
```
### 挑战2： 加载JS
```javascript
  const request = new XMLHttpRequest()
  request.open('GET', '/2.js')
  request.onload = ()=>{
      console.log(request.response)
      const script = document.createElement('script')
      script.innerHTML = request.response
      document.body.appendChild(script)
  }
  request.onerror = ()=>{}
  request.send()
```
### 挑战3： 加载HTML
```javascript
    const request = new XMLHttpRequest()
    request.open('GET', '/3.html')
    request.onload = ()=>{
        console.log(request.response)
        const div = document.createElement('div')
        div.innerHTML = request.response
        document.body.appendChild(div)
    }
    request.onerror = ()=>{}
    request.send()
```
### **onreadstatechange**
onerror没有很好的匹配ajax，因为先发明
改用**onreadstatechange**
#### XMLHttpRequest.readyState
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1598172569896-67087d5f-8b68-4eb7-81b0-061b106dafd8.png#align=left&display=inline&height=249&margin=%5Bobject%20Object%5D&name=image.png&originHeight=397&originWidth=988&size=51818&status=done&style=none&width=620)
#### XMLHttpRequest.status
响应分为五类：信息响应(`100`–`199`)，成功响应(`200`–`299`)，重定向(`300`–`399`)，客户端错误(`400`–`499`)和服务器错误 (`500`–`599`)。
```javascript
    const request = new XMLHttpRequest()
    request.open('GET', '3.htm')   // readyState === 1
    request.onreadystatechange = ()=>{
        if(request.readyState === 4) {
            // 4表示done，但不知道成功还是失败
            if (request.status >= 200 && request.status < 300) {
                const div = document.createElement('div')
                div.innerHTML = request.response
                document.body.appendChild(div)
            } else{
                alert("html加载失败")
            }
        }
    }
    request.send()  // readyState === 2
```
### 挑战4：加载XML
XML (Extensible Markup Language) 可扩展标记语言
```xml
<?xml version="1.0" encoding="UTF-8"?>
<message>
    <warning>
         Hello World
    </warning>
</message>
```
responseXML返回dom
```javascript
    const request = new XMLHttpRequest()
    request.open('GET', '/4.xml')
    request.onreadystatechange = ()=>{
        if(request.readyState === 4) {
            if (request.status >= 200 && request.status < 300) {
                // console.log(request.responseXML)  // 返回的是一个DOM
                const dom = request.responseXML
                const text = dom.getElementsByTagName('warning')[0].textContent.trim()
                console.log(text)
            } else{
                alert("xml加载失败")
            }
        }
    }
    request.send()
```
### 挑战5：加载JSON
JavaScript Object Notation
JSON是一门标记语言，与HTML, XML, Markdown一样，用来展示数据
中文官网：[http://www.json.org.cn/index.htm](http://www.json.org.cn/index.htm)


JSON支持的类型：

- string
- number
- bool
- null
- object
- array



```javascript
/* server.js 添加路由 */
if(path === '/5.json'){
    response.statusCode = 200
    response.setHeader('Content-Type', 'text/json;charset=utf-8')  // 也可以用application/json
    const string = fs.readFileSync('public/5.json')
    response.write(string)
    response.end()
  }
```


```javascript
getJSON.onclick = () => {
    const request = new XMLHttpRequest()
    request.open('GET', '/5.json')
    request.onreadystatechange = ()=>{
        if(request.readyState === 4 && request.status === 200){
            console.log(request.response)
            const obj = JSON.parse(request.response)
            console.log(obj)
            sayHi.textContent = "Hello " + obj.name 
        }     
    }
    request.send()
}
```
window.JSON 对象
JSON.parse()  解析JSON字符串
JSON.stringify() 转成JSON字符串
```javascript
JSON.parse('{"name":"rose"}')  
JSON.stringify({name:"rose", age:18})

try{
  let myName = JSON.parse(`{'name':"rose"}`)
}catch(error){
  console.log(error)
}
```
### 综合：加载分页
默认加载page1
```javascript
if(path === '/index.html'){
    response.statusCode = 200
    response.setHeader('Content-Type', 'text/html;charset=utf-8')
    let string = fs.readFileSync('public/index.html').toString()
    const page1 = fs.readFileSync('db/page1.json')
    const array = JSON.parse(page1)
    const result = array.map(item => `<li>${item.id}</li>`).join('')
    string = string.replace(`{{page1}}`,`<ul id="multiPages">${result}</ul>`)
    response.write(string)
    response.end()
  }
```
ajax请求page2
```javascript
let n = 1

getPage.onclick = ()=>{
    const request = new XMLHttpRequest()
    request.open('GET', `/page${n+1}.json`)   // 注意，第二个参数是server.js里的路由path
    request.onreadystatechange = ()=>{
        if(request.readyState === 4 && request.status === 200) {
            const array = JSON.parse(request.response)
            array.forEach(item => {
                const li = document.createElement('li')
                li.textContent = item.id 
                multiPages.appendChild(li)
            })
            n+=1
        }
    }
    request.send()
}
```


