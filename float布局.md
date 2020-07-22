# float布局

### float 布局步骤
1. 给子元素加width和float
1. 父元素加clearfix



示例：[http://js.jirengu.com/tiluv/1/edit?html,css,output](http://js.jirengu.com/tiluv/1/edit?html,css,output)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595394875292-cb29c402-cd04-497f-9111-640ccf4a4330.png#align=left&display=inline&height=725&margin=%5Bobject%20Object%5D&name=image.png&originHeight=725&originWidth=1920&size=125673&status=done&style=none&width=1920)


最后一个子元素可以不给宽度，只给 max-width: 100%;
float布局用于IE，不用于手机，不要做响应式


IE6/7有双倍margin的bug
```css
margin-left: 10px;
_margin-left: 5px;  /* 修复bug */
```
或者
```css
margin-left: 10px;
display: inline-block;  /* 修复bug */
```


### 做个导航
[http://js.jirengu.com/yofanojetu/1/edit?html,css,output](http://js.jirengu.com/yofanojetu/1/edit?html,css,output)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595396087805-2bd3ccb3-1d86-49fc-904b-cab882093a5b.png#align=left&display=inline&height=535&margin=%5Bobject%20Object%5D&name=image.png&originHeight=535&originWidth=1131&size=76524&status=done&style=none&width=1131)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595400023830-560e5130-a681-4e00-8413-fbca55baa44f.png#align=left&display=inline&height=835&margin=%5Bobject%20Object%5D&name=image.png&originHeight=835&originWidth=1059&size=111789&status=done&style=none&width=1059)
#### 添加内容区
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595407456029-9b590397-3d57-4297-9464-b3e3ed58f09d.png#align=left&display=inline&height=970&margin=%5Bobject%20Object%5D&name=image.png&originHeight=970&originWidth=1916&size=181316&status=done&style=none&width=1916)
#### 平均布局
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595410156467-ae5ced0f-2820-4e29-af10-905a660a0113.png#align=left&display=inline&height=938&margin=%5Bobject%20Object%5D&name=image.png&originHeight=938&originWidth=1920&size=211924&status=done&style=none&width=1920)
#### 用到的技巧

- div内的图片的border外面有背景色时，在img内添加 vertical-align:middle； 或 vertical-align:top；

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595404470110-c43f8e78-6995-4768-ba36-b8d092da73cd.png#align=left&display=inline&height=274&margin=%5Bobject%20Object%5D&name=image.png&originHeight=274&originWidth=587&size=28409&status=done&style=none&width=587)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595404504705-24489963-7bc2-4089-90f5-50390afde2b9.png#align=left&display=inline&height=331&margin=%5Bobject%20Object%5D&name=image.png&originHeight=331&originWidth=617&size=31748&status=done&style=none&width=617)

- div内是文字时，可以用 line-height 设置高度
- 要让父元素包住子元素，把父元素设置为 display:inline-block;

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595404648566-85aa308e-31f8-4625-8e7e-692d99653565.png#align=left&display=inline&height=318&margin=%5Bobject%20Object%5D&name=image.png&originHeight=318&originWidth=1008&size=33684&status=done&style=none&width=1008)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595404683052-f388f443-f5d1-4867-93b6-c8c630f61b6d.png#align=left&display=inline&height=284&margin=%5Bobject%20Object%5D&name=image.png&originHeight=284&originWidth=1010&size=34266&status=done&style=none&width=1010)


- 当 border 影响布局(固定宽度)时，改用 outline
```css
.content {
  outline: 1px solid red;  /* outline 不计入宽度 */
  width: 960px;   /* 固定宽度布局 */
}
```

- 让固定宽度的block元素居中
```css
margin-left: auto;
margin-right: auto;

margin: 0 auto; /* 可用，但当心覆盖上下margin */
```

- 平均布局用到负margin

参考：[https://www.yuque.com/qingrenyoutiandi/grlnzp/xn5cg7](https://www.yuque.com/qingrenyoutiandi/grlnzp/xn5cg7)

- 脱离文档流的元素margin不会合并
- 手机页面傻子采用float
- float用来应付IE足够了



#### emmet快捷输入
d:ib display:inline-block;
f:l float:left;
mb margin-bottom
ctrl + shift + L 格式化












