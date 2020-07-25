# position定位

static 默认值
relative 未脱离文档流
absolute 脱离文档流
fixed 脱离文档流，相对视口
sitcky 粘滞 兼容性不好


z-index默认值是auto
写z-index:9999的都是菜逼


position: absolute;要有一个祖先元素position:relative;
white-space: nowrap; // 文字内容不准换行


absolute是相对祖先元素中最近的定位元素(非static)定位
有些浏览器不写top/left位置会错乱
善用left: 100% 
left: 50% 和负margin
transform: translateX(-50%);


position: fixed; // 相对视口(用户的可见区域)
父元素是transform则不是相对视口定位
移动端不要用fixed


position: sticky; 粘滞定位 兼容性不好
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595548045324-9e0c1e5e-db82-498d-bc18-81e4231ecf1c.png#align=left&display=inline&height=379&margin=%5Bobject%20Object%5D&name=image.png&originHeight=759&originWidth=1239&size=512832&status=done&style=none&width=619.5)




层叠上下文 （独立的小世界）
[https://developer.cdn.mozilla.net/zh-CN/docs/Web/Guide/CSS/Understanding_z_index/The_stacking_context](https://developer.cdn.mozilla.net/zh-CN/docs/Web/Guide/CSS/Understanding_z_index/The_stacking_context)


![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595552103192-325ea996-52db-4829-8f5b-8e782c1ace58.png#align=left&display=inline&height=410&margin=%5Bobject%20Object%5D&name=image.png&originHeight=410&originWidth=511&size=15522&status=done&style=none&width=511)


opacity: 0.5;   // 不透明度， 影响当前元素内的所有元素
负z-index逃不出层叠上下文




