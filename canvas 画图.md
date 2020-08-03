# canvas 画图

css属性
```css
height:100vh;  // 与可视区域高度相同
width:100vw;  // 与可视区域宽度相同
```
在div内画点
```html
    <div id="canvas"></div>
    <script>
      canvas.onclick = (e) => {
        console.log(e);
        let div = document.createElement("div");   // 创建元素
        // 设置样式
        div.style.position = "absolute";  
        div.style.left = e.clientX + "px";
        div.style.top = e.clientY + "px";
        div.style.width = "6px";
        div.style.height = "6px";
        div.style.marginLeft = "-3px";
        div.style.marginTop = "-3px";
        div.style.borderRadius = "50%";
        div.style.backgroundColor = "black";
        // 添加到父节点里
        canvas.appendChild(div);
      };
    </script>
```
JS操作DOM很慢，改用canvas


canvas是inline元素
canvas一开始就要设置好宽高，用CSS改会拉伸模糊


```html
<!DOCTYPE html>
<html lang="zh-CN">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>画板</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <canvas id="canvas"></canvas>
    <script>
      let canvas = document.getElementById("canvas");
      
      // 获取文档宽度和高度，设置canvas的html属性
      canvas.width = document.documentElement.clientWidth;
      canvas.height = document.documentElement.clientHeight;

      let ctx = canvas.getContext("2d");

      ctx.lineWidth = 6;  // 设置画线宽度
      ctx.lineCap = "round";  // 防止转折处断开

      let painting = false;
      let last = [0, 0];
      
      // 画线函数
      function drawLine(lastX, lastY, newX, newY) {
        ctx.beginPath();
        ctx.moveTo(lastX, lastY);
        ctx.lineTo(newX, newY);
        ctx.stroke();
      }
      
      // 检测是否支持触屏
      var isTouchDevice = "ontouchstart" in document.documentElement;

      if (isTouchDevice) {
        canvas.ontouchstart = (e) => {
          let x = e.touches[0].clientX;
          let y = e.touches[0].clientY;
          last = [x, y];
        };
        canvas.ontouchmove = (e) => {
          let x = e.touches[0].clientX;
          let y = e.touches[0].clientY;
          drawLine(last[0], last[1], x, y);
          last = [x, y];
        };
      } else {
        canvas.onmousedown = (e) => {
          painting = true;
          last = [e.clientX, e.clientY];
        };

        canvas.onmousemove = (e) => {
          if (painting === true) {
            drawLine(last[0], last[1], e.clientX, e.clientY);
            last = [e.clientX, e.clientY];
          }
        };

        canvas.onmouseup = () => {
          painting = false;
        };
      }
    </script>
  </body>
</html>

```










