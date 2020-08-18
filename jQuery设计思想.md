# jQuery设计思想

### 1. 获取元素
#### (1) 用CSS选择器
```javascript
$(document) //选择整个文档对象
$('#myId')  // 选择ID为myId的网页元素
$('div.myClass')  // 选择class为myClass的div元素
$('input[name=first]')  // 选择name属性等于first的input元素
```
#### (2) 用jQuery特有表达式
```javascript
$('a:first') //选择网页中第一个a元素
$('tr:odd') //选择表格的奇数行
$('#myForm :input') // 选择表单中的input元素
$('div:visible') //选择可见的div元素
$('div:gt(2)') // 选择所有的div元素，除了前三个
$('div:animated') // 选择当前处于动画状态的div元素
```
### 2. 链式操作
jQuery最令人称道、最方便的特点。在于每一步的jQuery操作，返回的都是一个jQuery对象，所以不同操作可以连在一起。
```javascript
$('div').find('h3').eq(2).html('Hello').end().eq(0).html('World');

// 分解如下
$('div') //找到div元素
  .find('h3') //选择其中的h3元素
  .eq(2) //选择第3个h3元素
  .html('Hello') //将它的内容改为Hello
  .end() //退回到选中所有的h3元素的那一步
  .eq(0) //选中第一个h3元素
  .html('World'); //将它的内容改为World
```
### 3. 创建元素
创建新元素的方法非常简单，只要把新元素直接传入jQuery的构造函数就行了
```javascript
$('<p>Hello</p>');
$('<li class="new">new list item</li>');
$('ul').append('<li>list item</li>');
```
### 4. 移动元素
jQuery提供两组方法，来操作元素在网页中的位置移动。一组方法是直接移动该元素，另一组方法是移动其他元素，使得目标元素达到我们想要的位置。
假如选中一个div元素，要把它移动到p元素后面
第一种方法：.insertAfter() 把div元素移动到p元素后面
```javascript
$('div').insertAfter($('p'));
```
第二种方法：.after() 把p元素加到div元素前面
```javascript
$('p').after($('div'));
```
这两种方法的**区别**：第一种方法返回div元素，第二种方法返回p元素。
使用这种模式的操作方法，一共有四对：
```javascript
.insertAfter()和.after()  // 在现存元素的外部，从后面插入元素
.insertBefore()和.before()  // 在现存元素的外部，从前面插入元素
.appendTo()和.append()  // 在现存元素的内部，从后面插入元素
.prependTo()和.prepend()  // 在现存元素的内部，从前面插入元素
```
### 5. 修改元素属性
jQuery使用同一个函数，来完成取值（getter）和赋值（setter），即"取值器"与"赋值器"合一。到底是取值还是赋值，由函数的参数决定。
```javascript
$('h1').html(); //html()没有参数，表示取出h1的值
$('h1').html('Hello'); //html()有参数Hello，表示对h1进行赋值
```
常见的取值和赋值函数如下：
```javascript
.html() 取出或设置html内容
.text() 取出或设置text内容
.attr() 取出或设置某个属性的值
.width() 取出或设置某个元素的宽度
.height() 取出或设置某个元素的高度
.val() 取出某个表单元素的值
```
### 6. 引入jQuery
#### (1) 下载jQuery
下载地址： [jquery.com](http://jquery.com/download/)
Production version：用于实际的网站中，已被精简和压缩。
Development version：用于测试和开发（未压缩，是可读的代码）。
#### (2) 在公网上引用jQuery
引用代码如下：
```
<script src="https://cdn.staticfile.org/jquery/1.10.2/jquery.min.js">
```
或：
```
<script src="https://apps.bdimg.com/libs/jquery/2.1.4/jquery.min.js">
```
或：
```
<script src="https://upcdn.b0.upaiyun.com/libs/jquery/jquery-2.0.2.min.js">
```
或：
```
<script src="https://lib.sinaapp.com/js/jquery/2.0.2/jquery-2.0.2.min.js">
```


