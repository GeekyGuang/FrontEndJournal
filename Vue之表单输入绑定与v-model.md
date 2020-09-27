# Vue之表单输入绑定与v-model

> 你可以用 `v-model` 指令在表单 `<input>`、`<textarea>` 及 `<select>` 元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。尽管有些神奇，但 `v-model` 本质上不过是语法糖。它负责监听用户的输入事件以更新数据，并对一些极端场景进行一些特殊处理。

### label与input的配合
要实现点击label时也点击到input,
可以让label的for属性值与input的id相等
```html
<label for="apple">Do you like apple?</label>
<input type="checkbox" id="apple" name="fruits">

<label for="banana">Do you like banana?</label>
<input type="checkbox" id="banana" name="fruits">
```
也可以将 `<input>` 直接放在 `<label>` 里，此时则不需要 `for` 和 `id` 属性，因为关联已隐含存在：
```html
<label>Do you like apple?
  <input type="checkbox" id="apple" name="fruits">
</label>

<label>Do you like banana?
  <input type="checkbox" id="banana" name="fruits">
</label>
```
### 文本
```html
<template>
  <div>
    <label>姓名：
      <input type="text" v-model="message" placeholder="姓名">
    </label>
    <p>你的名字是：{{message}}</p>
  </div>
</template>
```
### 多行文本
```vue
<span>Multiline message is:</span>
<p style="white-space: pre-line;">{{ message }}</p>
<br>
<textarea v-model="message" placeholder="add multiple lines"></textarea>
```
### 复选框
#### 单个复选框
```vue
<label>
  <input type="checkbox" v-model="checked">{{checked}}
</label>
```
选中则为true，![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1599967049516-92283947-af1e-411c-a2ca-47f09f713eaf.png#align=left&display=inline&height=24&margin=%5Bobject%20Object%5D&name=image.png&originHeight=34&originWidth=84&size=707&status=done&style=none&width=59)
#### 多个复选框
绑定到一个数组
```vue
<p>{{hobby}}</p>
<label>
  抽烟<input type="checkbox" v-model="hobby" value="抽烟">
</label>
<label>
  喝酒<input type="checkbox" v-model="hobby" value="喝酒">
</label>
<label>
  烫头<input type="checkbox" v-model="hobby" value="烫头">
</label>
```
```vue
<script>
export default {
  data(){
    return{
      hobby:[]
    }
  }
}
</script>
```
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1599967549161-2b373e0b-82ec-4bc7-b183-9c1bf5132992.png#align=left&display=inline&height=93&margin=%5Bobject%20Object%5D&name=image.png&originHeight=121&originWidth=263&size=3962&status=done&style=none&width=203)
### 单选按钮
将上例中的 **checkbox **改成 **radio**, v-model可以绑定一个数组，也可以绑定一个字符串变量(推荐)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1599967747062-5a2020df-8215-4247-b60b-74981ad6489d.png#align=left&display=inline&height=77&margin=%5Bobject%20Object%5D&name=image.png&originHeight=111&originWidth=291&size=3411&status=done&style=none&width=201)
### 选择框
#### 单选框
```vue
<p>{{hobby}}</p>
<select name="hobby" v-model="hobby">
  <option disabled value="">--</option>
  <option>抽烟</option>
  <option>喝酒</option>
  <option>烫头</option>
</select>
```

- 每个 `<option>` 元素都应该有一个 `value` 属性，其中包含被选中时需要提交到服务器的数据值。如果不含 `value` 属性，则 `value` 值默认为元素中的文本。
- 一般情况下，可以在 `<option>` 元素中设置一个 `selected` 属性以将其设置为页面加载完成时默认选中的元素。
- 但是用**v-model**时， `selected` 属性失效，将option的value设置为与v-model绑定值相同，则默认选中。
- disabled属性使option不可被选择

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1599969571008-ca4f2f28-3765-4167-b402-50aece6ecbb6.png#align=left&display=inline&height=154&margin=%5Bobject%20Object%5D&name=image.png&originHeight=154&originWidth=151&size=4415&status=done&style=none&width=151)
#### 多选框
select添加multiple属性，v-model绑定数组
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1599970070232-02c115a9-73d0-43e7-bf27-3a484ef2de91.png#align=left&display=inline&height=124&margin=%5Bobject%20Object%5D&name=image.png&originHeight=175&originWidth=228&size=4244&status=done&style=none&width=161)
#### v-for动态渲染
```vue
<p>{{hobby}}</p>
<select name="hobby" v-model="hobby">
  <option disabled value="">--</option>
  <option v-for="item in array" :value="item.value" :key="item.value">
    {{ item.text }}
  </option>
</select>
```
### form提交
form里面加了button, 回车或点击按钮时会触发**submit**事件
```html
<form @submit.prevent="onSubmit">
  <label >
    name: <input v-model="user.name">
  </label>
  <label >
    password: <input type="password" v-model="user.password">
  </label>
  
  <button type="submit">确定</button>
  
</form>
```
### 修饰符
#### `.lazy`
在默认情况下，`v-model` 在每次 `input` 事件触发后将输入框的值与数据进行同步 (除了[上述](https://cn.vuejs.org/v2/guide/forms.html#vmodel-ime-tip)输入法组合文字时)。你可以添加 `lazy` 修饰符，从而转为在 `change` 事件_之后_进行同步：
```html
<!-- 在“change”时而非“input”时更新 -->
<input v-model.lazy="msg">
```


#### `.number`
如果想自动将用户的输入值转为数值类型，可以给 `v-model` 添加 `number` 修饰符：
```html
<input v-model.number="age" type="number">
```
这通常很有用，因为即使在 `type="number"` 时，HTML 输入元素的值也总会返回字符串。如果这个值无法被 `parseFloat()` 解析，则会返回原始的值。


#### `.trim`
如果要自动过滤用户输入的首尾空白字符，可以给 `v-model` 添加 `trim` 修饰符：
```html
<input v-model.trim="msg">
```
### v-model本质
v-model是v-bind:vlaue和v-on:input的语法糖
```html
<input type="text" :value="user.name"
       @input="user.name = $event.target.value">
```
当触发input事件时，**$event**是当前的事件对象，**$event.target.value**指向的是当前输入框的值。
