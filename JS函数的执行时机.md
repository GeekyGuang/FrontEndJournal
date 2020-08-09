# JS函数的执行时机

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596462298386-3abfbb97-ed80-4808-a333-668e08a3d2ea.png#align=left&display=inline&height=233&margin=%5Bobject%20Object%5D&name=image.png&originHeight=289&originWidth=431&size=16627&status=done&style=none&width=347)
上述代码打出6个6，与setTimeout(fn, time)的执行机制有关，setTimeout会将fn函数放入**任务队列**，等待主程序执行完毕(**函数调用栈为空**)后再调出任务队列中的fn函数执行，for循环每执行一次，就有一个fn进入了任务队列，等for循环执行完毕，i的值为6，这里的 i 是一个全局变量，每个fn里的 i 的值最终都是6，所以打出了5个6。


如果想要打出0，1，2，3，4，5，那么需要一种方法，每次for循环，都保存一个i的值传给fn，且不再改变
### 方法一
将let声明放到for的括号里面，每次for循环里的 i 都处于独立的块级作用域
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596462232553-22000cda-434f-484f-8af2-e6de5349ecba.png#align=left&display=inline&height=339&margin=%5Bobject%20Object%5D&name=image.png&originHeight=470&originWidth=659&size=21357&status=done&style=none&width=475)
### 方法二
使用**立即执行函数**传递参数，使得fn里的 i 变成局部变量
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1596462510663-3871d3ec-24ea-4598-9e49-f1088d581545.png#align=left&display=inline&height=448&margin=%5Bobject%20Object%5D&name=image.png&originHeight=564&originWidth=697&size=28120&status=done&style=none&width=554)








