# call, apply, bind

### call
`**call()**` 方法使用一个指定的 `this` 值和单独给出的一个或多个参数来调用一个函数。
```javascript
function f1(x, y) {
  console.log(this.name)
  console.log(x + y)
}

let obj = {name: "jack"}

f1.call(obj, 1, 2)
```
### apply
apply与call相似，区别就是`call()`方法接受的是**参数列表**，而`apply()`方法接受的是**一个参数数组**。
```javascript
function f1(x, y) {
  console.log(this.name)
  console.log(x + y)
}

let obj = {name: "jack"}

f1.apply(obj, [1, 2])
```
### bind
`**bind()**` 方法创建一个新的函数，在 `bind()` 被调用时，这个新函数的 `this` 被指定为 `bind()` 的第一个参数，而其余参数将作为新函数的参数，供调用时使用。
```javascript
const module = {
  x: 42,
  getX: function() {
    return this.x;
  }
};

const boundGetX = unboundGetX.bind(module);
console.log(boundGetX());
```


