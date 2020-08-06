# JS语法

### 表达式和语句
表达式一般都有值，语句可能有值可能没有
语句一般会改变环境(声明，赋值)
以上两句并不绝对


console.log的值是函数本身
console.log(3)的值是undefined
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596115802577-a6a13cdb-9291-4f0f-ac52-e163abafe3a1.png#align=left&display=inline&height=69&margin=%5Bobject%20Object%5D&name=image.png&originHeight=77&originWidth=216&size=2168&status=done&style=none&width=194)
return后面不能加回车
```javascript
var a = ()=>{ 
return
3}
a()
// undefined
var b = ()=>{
return 3
}
b()
// 3
```
### 标识符

1. 第一个字符可以是Unicode字符或$或_或汉字
1. 后面的字符还可以是数字



用汉字比用拼音好


### 注释
#### 不好的注释

- 把代码翻译成中文
- 过时的注释
- 发泄不满的注释
#### 好的注释

- 踩坑的注释
- 为什么代码写这么奇怪，遇到什么bug



### if...else

逗号表示这句话没完
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596116191901-d0e9b113-23ce-4da8-b493-a89aab6283b3.png#align=left&display=inline&height=206&margin=%5Bobject%20Object%5D&name=image.png&originHeight=216&originWidth=484&size=9472&status=done&style=none&width=461)
### while循环
```javascript
var a = 0.1
// 一个死循环
while (a !== 1) {
  console.log(a)
  a = a + 0.1
}
```
浮点数不精确
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596116567986-c566d1ef-3089-4875-940d-91f2fb792d36.png#align=left&display=inline&height=436&margin=%5Bobject%20Object%5D&name=image.png&originHeight=555&originWidth=313&size=16838&status=done&style=none&width=246)


### for循环
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596116836615-1ac994f4-ed62-40c9-b78a-fea064164655.png#align=left&display=inline&height=111&margin=%5Bobject%20Object%5D&name=image.png&originHeight=122&originWidth=341&size=4875&status=done&style=none&width=309)
setTimeout()函数导致过一会儿打出i (可将var改成let)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596117008502-2bdfeb1a-c187-454a-ae9a-1e40aa13c51b.png#align=left&display=inline&height=155&margin=%5Bobject%20Object%5D&name=image.png&originHeight=164&originWidth=324&size=4751&status=done&style=none&width=306)


### 短路逻辑
#### &&短路逻辑
A&&B 
A为真，表达式的值为B
A为假，表达式的值为A
fn && fn()


#### ||短路逻辑
A || B
A为真，表达式的值为A
A为假，表达式的值为B
A = A || B


### break vs continue
break退出整个循环
continue结束本次循环进入下一次循环


### label
```javascript
{
  a:1   // 标签a后面跟着表达式1
}
```




















