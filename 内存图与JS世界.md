# 内存图与JS世界

Kernel(内核)


JS是单线程


DOM操作慢，跨线程


JS运行环境
API：window，setTimeout, document


window中的Object, Array都是构造函数

prototype与__proto__
```javascript
var b = {}
console.dir(b)  // 查看结构
b.__proto__ === Object.prototype  // true
b.__proto__.toString === Object.prototype.toString // true
b.__proto__.toString = "hello"
b.toString  // "hello"
Object.prototype.toString  // "hello"
var c = {}
c.toString  //"hello"

Array.prototype.__proto__ === Object.prototype // true
```


> prototype存储了对象的共有属性
> prototype在构造函数里
> __proto__在实例里
> prototype和__proto__指向同一个地址





自定义对象
```javascript
var Person = function(name, age) { this.name = name; this.age = age; }
Person.prototype.hello = function() {console.log("hello")};
var jack = new Person("jack", 19);
jack.hello()  // hello
```


![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596013171575-eab1906f-569f-4c27-bd0c-687a9cbe5dfc.png#align=left&display=inline&height=814&margin=%5Bobject%20Object%5D&name=image.png&originHeight=814&originWidth=890&size=378375&status=done&style=none&width=890)








