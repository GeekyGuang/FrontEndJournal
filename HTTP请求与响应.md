# HTTP请求与响应

```javascript
if (path === "/") {
    response.statusCode = 200;
    response.setHeader("Content-Type", "text/html;charset=utf-8");
    response.write(`
      <!DOCTYPE html>
      <head>
      <link rel="stylesheet" href="/style.css">
      </head>
      <h1>哈哈哈</h1>
      `);
    response.end();
  } else if (path === "/style.css") {
    response.statusCode = 200;
    response.setHeader("Content-Type", "text/css;charset=utf-8");
    response.write(`h1{color: red;}`);
    response.end();
  } else {
    response.statusCode = 404;
    response.setHeader("Content-Type", "text/html;charset=utf-8");
    response.write("你访问的页面不存在");
    response.end();
  }
```
开启服务：node server.js 8888
发请求：
curl -v http://localhost:8888/
curl -v -X post http://localhost:8888/




