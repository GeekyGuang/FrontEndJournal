# 异步与Promise

### 什么是异步？
- 能直接拿到结果的是**同步**
- 不能直接拿到结果的是**异步**

**
异步拿到结果的方法

- **轮询**：隔一段时间问一次
- **回调**：写一个函数给浏览器调用，浏览器把结果作为参数传给该函数



异步不一定要用回调(可用轮询)，回调也不是只用于异步(可用于同步)，异步和回调是合作关系。
### 判断异步还是同步
如果一个函数的返回值处于

- setTimeout
- AJAX(即XMLHttpRequest)
- AddEventListener

这个三个东西内部，这个函数就是异步函数


AJAX可以设置为同步，但这样做会使请求期间页面卡住，所以不要用
request.open("get", "/5.json", **false**) 设置false则为同步，默认异步


#### 面试题
```javascript
const array = ['1', '2', '3'].map(parseInt)
console.log(array)

// [1, NaN, NaN]
```
map默认传3个参数(item, index ,array),和parseInt要求参数不同，所以不能简化，正确是
```javascript
const array = ['1', '2', '3'].map(item => parseInt(item))
console.log(array)
```




![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1598236329432-0f85a10d-93df-409e-9a59-2bdcd025eb52.png#align=left&display=inline&height=148&margin=%5Bobject%20Object%5D&name=image.png&originHeight=295&originWidth=1206&size=317361&status=done&style=none&width=603)
回调地狱
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1598236690807-029a2b97-7fe5-433b-b9c6-327d2c3f0285.png#align=left&display=inline&height=222&margin=%5Bobject%20Object%5D&name=image.png&originHeight=443&originWidth=1078&size=549591&status=done&style=none&width=539)


![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1598238048140-b1e80ba7-808e-4839-a2cd-18ff8eb21c5b.png#align=left&display=inline&height=74&margin=%5Bobject%20Object%5D&name=image.png&originHeight=148&originWidth=1187&size=189064&status=done&style=none&width=593.5)


![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1598239963900-33ba48bc-4634-4396-bae6-384316ea68d6.png#align=left&display=inline&height=196&margin=%5Bobject%20Object%5D&name=image.png&originHeight=291&originWidth=745&size=36001&status=done&style=none&width=501)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1598240027843-1743a205-b3a0-466b-a78c-a2a3346b7566.png#align=left&display=inline&height=130&margin=%5Bobject%20Object%5D&name=image.png&originHeight=165&originWidth=643&size=16364&status=done&style=none&width=505)




