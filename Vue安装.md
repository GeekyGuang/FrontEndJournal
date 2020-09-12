# Vue安装

MVC中的V是Vue的重点，M和C被简化
Vue目前(2.0之后)不是MVVM框架


### @vue/cli
安装
```bash
yarn global add @vue/cli
```
查看版本
```bash
vue --version
```
创建一个项目
```bash
vue create vue-demo-1
```
选择手动配置
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1599642532915-83c59b69-d421-4b70-b79d-c08df467dfe5.png#align=left&display=inline&height=114&margin=%5Bobject%20Object%5D&name=image.png&originHeight=201&originWidth=796&size=29803&status=done&style=none&width=451)
按方向键+空格选择，未截图的默认
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1599642987937-c8f41c5e-af10-40a1-8132-08caff7ec26b.png#align=left&display=inline&height=181&margin=%5Bobject%20Object%5D&name=image.png&originHeight=363&originWidth=632&size=57573&status=done&style=none&width=316)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1599643036965-b9f8c213-e6f0-4c32-acc9-9edab48fe9ed.png#align=left&display=inline&height=55&margin=%5Bobject%20Object%5D&name=image.png&originHeight=91&originWidth=511&size=13909&status=done&style=none&width=310)提交时才显示错误
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1599643079225-77a81ab2-ec3d-4384-a590-ab993e8022c3.png#align=left&display=inline&height=67&margin=%5Bobject%20Object%5D&name=image.png&originHeight=89&originWidth=387&size=9608&status=done&style=none&width=291)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1599643119411-f6ad1894-493e-4c25-92d7-7c895bcd1c7e.png#align=left&display=inline&height=23&margin=%5Bobject%20Object%5D&name=image.png&originHeight=46&originWidth=758&size=9235&status=done&style=none&width=379)大写表示默认，可直接回车
打开当前目录
```bash
start .
```
运行server
```bash
cd vue-demo-1
yarn serve
```
成功
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1599643517151-803405fb-ca41-4aff-bcb6-78d45941891e.png#align=left&display=inline&height=346&margin=%5Bobject%20Object%5D&name=image.png&originHeight=912&originWidth=1406&size=81991&status=done&style=none&width=534)
### 如何学习Vue?
将@vue/cli和Vue.js文档看完
[https://cli.vuejs.org/zh/guide/](https://cli.vuejs.org/zh/guide/)
[https://cn.vuejs.org/v2/guide/](https://cn.vuejs.org/v2/guide/)


### codeSandBox
[https://codesandbox.io/](https://codesandbox.io/)
不登录可以创建无限个项目


### SEO友好
搜索引擎优化
搜索引擎根据curl猜测页面内容
如果都是用js建div, curl就眼瞎
把title，description, keyword, h1, a写好
让curl得到页面信息
### 写出Vue需要什么水平？
定一个目标，实现它，你就达到了那个水平，而不是要先达到某个水平才去实现它，那你永远实现不了


SSR： server side render





