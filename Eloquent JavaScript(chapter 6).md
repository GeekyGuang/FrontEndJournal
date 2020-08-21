# Eloquent JavaScript(chapter 6)

### Encapsulation(封装)
Properties that are part of the interface are called **_public_**. The others, which outside code should not be touching, are called **_private_**.

Many languages provide a way to distinguish public and private properties and prevent outside code from accessing the private ones altogether.JavaScript, once again taking the minimalist approach, **does not**—not yet at least. 


It is also common to put an underscore (_) character at the start of property names to indicate that those properties are private.


Separating interface from implementation is a great idea. It is usually called _encapsulation_.
### Methods
Methods are nothing more than properties that hold function values. 
`object.method()`—the binding called **`this`** in its body automatically points at the object that it was called on.
```javascript
function speak(line) {
  console.log(`The ${this.type} rabbit says '${line}'`);
}
let whiteRabbit = {type: "white", speak};
let hungryRabbit = {type: "hungry", speak};

whiteRabbit.speak("Oh my ears and whiskers, " +
                  "how late it's getting!");
// → The white rabbit says 'Oh my ears and whiskers, how
//   late it's getting!'
hungryRabbit.speak("I could use a carrot right now.");
// → The hungry rabbit says 'I could use a carrot right now.'
```
 you can use a function’s **`call`** method, which takes the `this` value as its first argument and treats further arguments as normal parameters.
```javascript
speak.call(hungryRabbit, "Burp!");
// → The hungry rabbit says 'Burp!'
```
**Arrow functions **are different—they do not bind their own `this` but can see the `this` binding of the scope around them.
```javascript
function normalize() {
  console.log(this.coords.map(n => n / this.length));
}
normalize.call({coords: [0, 2, 3], length: 5});
// → [0, 0.4, 0.6]
```
### Prototypes
**Object.getPrototypeOf()**查看一个对象的__proto__
```javascript
console.log(Object.getPrototypeOf({}) ==
            Object.prototype);
// → true
console.log(Object.getPrototypeOf(Object.prototype));
// → null
```
You can use **`Object.create`** to create an object with a specific prototype.
```javascript
let protoRabbit = {
  speak(line) {
    console.log(`The ${this.type} rabbit says '${line}'`);
  }
};
let killerRabbit = Object.create(protoRabbit);
killerRabbit.type = "killer";
killerRabbit.speak("SKREEEE!");
// → The killer rabbit says 'SKREEEE!'



killerRabbit.__proto__ === protoRabbit
// true
protoRabbit.__proto__ === Object.prototype
// true
```
### Classes
A class defines the shape of a type of object—what methods and properties it has. Such an object is called an _instance_ of the class.
#### constructor function
```javascript
function makeRabbit(type) {
  let rabbit = Object.create(protoRabbit);
  rabbit.type = type;
  return rabbit;
}
```
JavaScript provides a way to make defining this type of function easier. If you put the keyword `new` in front of a function call, the function is treated as a constructor. This means that an object with the right prototype is automatically created, bound to `this` in the function, and returned at the end of the function.
```javascript
function Rabbit(type) {
  this.type = type;
}
Rabbit.prototype.speak = function(line) {
  console.log(`The ${this.type} rabbit says '${line}'`);
};

let weirdRabbit = new Rabbit("weird");


Rabbit.__proto__ === Function.prototype
// true
weirdRabbit.__proto__ === Rabbit.prototype
// true
```
So JavaScript classes are constructor functions with a prototype property. **until 2015.**
#### Class notation
```javascript
class Rabbit {
  constructor(type) {
    this.type = type;
  }
  
  /* 目前只能将method写到prototype，不能写property */
  speak(line) {
    console.log(`The ${this.type} rabbit says '${line}'`);
  }
}

let killerRabbit = new Rabbit("killer");
let blackRabbit = new Rabbit("black");
```
class也可以直接用于表达式
```javascript
let object = new class { getWord() { return "hello"; } };
console.log(object.getWord());
// → hello
```
### override 重写
```javascript
Rabbit.prototype.teeth = "small";
console.log(killerRabbit.teeth);
// → small
killerRabbit.teeth = "long, sharp, and bloody";
console.log(killerRabbit.teeth);
// → long, sharp, and bloody
console.log(blackRabbit.teeth);
// → small
console.log(Rabbit.prototype.teeth);
// → small
```
![](https://cdn.nlark.com/yuque/0/2020/svg/1753813/1597906282441-da262b3a-d4d3-4bc9-870f-2740d901f576.svg#align=left&display=inline&height=274&margin=%5Bobject%20Object%5D&originHeight=274&originWidth=621&size=0&status=done&style=none&width=621)
### maps
**in **操作符会访问Object的prototype的属性，用**hasOwnProperty**只访问对象本身属性
```javascript
console.log("toString" in {})
// true

console.log({x: 1}.hasOwnProperty("x"));
// → true
console.log({x: 1}.hasOwnProperty("toString"));
// → false
```
**map**
```javascript
let ages = new Map();
ages.set("Boris", 39);
ages.set("Liang", 22);
ages.set("Júlia", 62);

console.log(`Júlia is ${ages.get("Júlia")}`);
// → Júlia is 62
console.log("Is Jack's age known?", ages.has("Jack"));
// → Is Jack's age known? false
console.log(ages.has("toString"));
// → false
```
### Polymorphism 多态
When you call the `String` function (which converts a value to a string) on an object, it will call the `toString` method on that object to try to create a meaningful string from it. 
```javascript
Rabbit.prototype.toString = function() {
  return `a ${this.type} rabbit`;
};

console.log(String(blackRabbit));
// → a black rabbit
```
### Symbols
Unlike strings, newly created symbols are unique—you cannot create the same symbol twice.
```javascript
let sym = Symbol("name");
console.log(sym == Symbol("name"));
// → false
Rabbit.prototype[sym] = 55;
console.log(blackRabbit[sym]);
// → 55
```
```javascript
const toStringSymbol = Symbol("toString");
Array.prototype[toStringSymbol] = function() {
  return `${this.length} cm of blue yarn`;
};

console.log([1, 2].toString());
// → 1,2
console.log([1, 2][toStringSymbol]());
// → 2 cm of blue yarn
```
### instanceof
```javascript
console.log(
  new SymmetricMatrix(2) instanceof SymmetricMatrix);
// → true
console.log(new SymmetricMatrix(2) instanceof Matrix);
// → true
console.log(new Matrix(2, 2) instanceof SymmetricMatrix);
// → false
console.log([1] instanceof Array);
// → true
```


