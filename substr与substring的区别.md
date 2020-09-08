# substr与substring的区别

只给一个参数时，都表示从该索引位置到末尾
```javascript
let message = "我爱北京天安门"
message.substr(2)
message.substring(2)
// 北京天安门
```
给两个参数时
substr第二个参数表示长度
substring第二个参数表示索引, 且截取不包括第二个索引
```javascript
let message = "我爱北京天安门"
message.substr(1,2) // "爱北"
message.substring(1,2)  // "爱"
```


