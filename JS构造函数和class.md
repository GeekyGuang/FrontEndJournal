# JS构造函数和class

### 构造函数
```javascript
function Person(name, age) {
  this.name = name
  this.age = age
}

Person.prototype.sayHi = function(){
  console.log("My name is " + this.name)   // 用this不能用箭头函数
}

person1 = new Person('jack', 19)
person.sayHi()
```
函数自带prototype
ptototype自带constructor, 且是函数自身
生成的对象的__proto__里也有constructor，即其构造函数的prototype里的constructor


原型公式：
对象.__proto__=== 其构造函数.prototype

要看一个对象是由谁构造出来的就看他的__proto__里的constructor
对象.__proto__.constructor  === 其构造函数.prototype.constructor


![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596286192768-bed2f83e-55cc-4c0c-890f-aab559f36e4e.png#align=left&display=inline&height=343&margin=%5Bobject%20Object%5D&name=image.png&originHeight=343&originWidth=1206&size=37197&status=done&style=none&width=1206)


### 终极一问

- window由谁构造？Window

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596287760815-03ca122a-a6cd-44f6-8606-1edf447aaf77.png#align=left&display=inline&height=52&margin=%5Bobject%20Object%5D&name=image.png&originHeight=103&originWidth=653&size=11890&status=done&style=none&width=326.5)

- window.Object由谁构造？Function

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596287797481-517c205c-e20f-4559-afcf-558c9fccbcac.png#align=left&display=inline&height=51&margin=%5Bobject%20Object%5D&name=image.png&originHeight=101&originWidth=672&size=13266&status=done&style=none&width=336)

- window.Function由谁构造？Function

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596287867020-e6300996-5090-4614-82d3-51553624a504.png#align=left&display=inline&height=48&margin=%5Bobject%20Object%5D&name=image.png&originHeight=96&originWidth=741&size=13268&status=done&style=none&width=370.5)
所有函数都是window.Function构造的，
浏览器构造了Function，然后指定它的构造者是自己


### class
```javascript
class Person{  // 不要括号
  constructor(name, age) {    // 注意参数传给constructor
    this.name = name
    this.age = age
  }
  sayHi(){
    console.log("My name is " + this.name)   
  }
}

person1 = new Person('jack', 19)
person.sayHi()
```






