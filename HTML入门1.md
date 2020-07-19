# HTML入门1

### 起手式
新建index.html文件后，输入 ! 后敲Tab键
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595076662852-9411bff9-9ef7-48d7-bb12-f362b1619a0e.png#align=left&display=inline&height=248&margin=%5Bobject%20Object%5D&name=image.png&originHeight=496&originWidth=1272&size=65251&status=done&style=none&width=636)
head和body标签一般不缩进


### 章节标签
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595083299916-7a929e94-6421-457c-aaa5-40d6b55e2ab3.png#align=left&display=inline&height=390&margin=%5Bobject%20Object%5D&name=image.png&originHeight=780&originWidth=969&size=93912&status=done&style=none&width=484.5)

| h1~h6 | 标题 | 一个页面一般只有一个h1 |
| --- | --- | --- |
| section | 章节 |  |
| article | 文章 | 比section语义更强 |
| p | 段落 |  |
| header | 头部 |  |
| footer | 底部 |  |
| main | 主要部分 |  |
| aside | 旁支部分 |  |
| div | 划分division | 无语义 |

### 全局属性


选择器 [class="xxx"] {border:1px solid red;}  // 必须匹配一个标签全部的class


contenteditable  // 让内容可编辑
```html
<div id="xxx" contenteditable>
```
让style可见的方法：
将style放body里，display:block;


hidden属性与display:none;有区别
```html
<div id="xxx" hidden>
```
不到万不得已，不要用id，id重复不会报错


js可以直接用id调用（不到万不得已不要用）
id名不能与window的全局属性同名
xxx.style.border = "1px solid green"；


css 优先级 js > 属性style > style标签 > link


tabindex 设置按tab键选中的顺序，tabindex=0是最后一个，-1是不选中


titile属性 鼠标悬浮显示内容
### 默认样式
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595084450706-8985021c-efa3-401d-87c7-1eeb3b342bae.png#align=left&display=inline&height=230&margin=%5Bobject%20Object%5D&name=image.png&originHeight=296&originWidth=494&size=25760&status=done&style=none&width=384)
清除默认样式
```css
* {margin: 0;padding: 0;box-sizing: border-box;}
*::before, *::after {box-sizing: border-box;}
a {color: inherit;text-decoration: none;}
input, button {font-family: inherit;}
ol, ul {list-style: none;}
table {border-collapse: collapse;border-spacing: 0;}
```
### 内容标签
| ol + li | ordered list + list item |  |
| --- | --- | --- |
| ul + li | unordered list + list item |  |
| dl + dt + dd | description list + term + data |  |
| hr | horizontal rule 水平分割线 |  |
| br | break |  |
| a | anchor |  |
| em | emphasis斜体 | 语气上的强调 |
| strong | 加粗 | 内容上的强调 |
| pre | preview | 显示空格和回车，不合并 |
| code | 代码 |  |
| q | quote 内联引用 | 会加上引号 |
| blockquote | 块级引用 |  |

html多个连续空格或回车都只会合并为一个空格
pre 标签可以保留空格和回车
code 标签字体默认是等宽的
用pre包住code，则可正常显示缩进和换行
```html
  <pre>
   <code>
     var a = 1;
     console.log(a);
   </code>
  </pre>
```








