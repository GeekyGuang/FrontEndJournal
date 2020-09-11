# webpack-1

### 查看webpack最新版本
```bash
npm info webpack
```
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1599384836673-f3e3f195-364e-4263-a95b-035d7e098c78.png#align=left&display=inline&height=69&margin=%5Bobject%20Object%5D&name=image.png&originHeight=102&originWidth=747&size=8947&status=done&style=none&width=505)
#### 全局安装
```bash
npm i -g webpack@4 webpack-cli@4
```
#### 局部安装
```bash
mkdir webpack-demo
cd webpack-demo
npm init -y
npm install webpack webpack-cli --save-dev
# 或者
yarn add webpack webpack-cli --save-dev
```
### 用webpack转译JS
安装完后查看版本
```bash
./node_modules/.bin/webpack --version
```
运行webpack
```bash
npx webpack    # 安装路径不能有空格
```
#### 去除警告
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1599399368996-c19c37c8-307a-4537-873c-3b9417748006.png#align=left&display=inline&height=61&margin=%5Bobject%20Object%5D&name=image.png&originHeight=121&originWidth=1542&size=28797&status=done&style=none&width=771)
在webpack-demo文件夹创建**webpack.config.js**文件，
写入内容, mode可以设为development或product
```javascript
module.exports = {
    mode: 'development'
  };
```
### 设置entry和output
```javascript
var path = require('path');

module.exports = {
  mode: 'development',
  entry: './src/index.js',    // 输入文件
  output: {
    // path: path.resolve(__dirname, 'dist'),  // 路径默认是dist
    filename: 'index.js'  // 输出文件名
  }
};
```
### HTTP缓存
缓存可以加快访问速度
通过Cache-Control设置max-age
如果index.html中的引用文件名变了，则下载新的文件
将output中的filename设置如下，则给文件名自动生成hash数字
```javascript
  output: {
    filename: '[name].[contenthash].js'
  }
```
每次运行，应先删掉dist文件
在package.json文件的scripts中添加build
linux和mac系统中&&可改为；
```javascript
  "scripts": {
    "build": "rm -rf dist && webpack",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```
```bash
yarn build
```
### 生成html文件
安装插件
```bash
yarn add html-webpack-plugin --dev
```
修改webpack.config.js
添加HtmlWebpackPlugin和plugins两行
参考：[https://github.com/jantimon/html-webpack-plugin#options](https://github.com/jantimon/html-webpack-plugin#options)
```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin')
var path = require('path');

module.exports = {
  mode: 'development',
  entry: './src/index.js',
  output: {
    // path: path.resolve(__dirname, 'dist'),
    filename: 'index.[contenthash].js'  // [name]可以修改
  },
  plugins: [
    new HtmlWebpackPlugin()
  ]
};
```
#### 用自己的模板生成html
```javascript
plugins: [
  new HtmlWebpackPlugin({
    title: 'Custom template',
    // Load a custom template (lodash by default)
    template: 'src/index.html'
  })
]
```
自定义index.html的title
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8"/>
    <title><%= htmlWebpackPlugin.options.title %></title>
  </head>
  <body>
  </body>
</html>
```
### 加载css文件
安装css-loader和style-loader
```bash
yarn add css-loader --dev
yarn add style-loader --dev
```
添加配置
```javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
    ],
  },
};
```
js文件里import css文件
build
### 使用 webpack-dev-server
安装
```bash
yarn add webpack-dev-server --dev
```
webpack.config.js添加
```javascript
 devServer: {
     contentBase: './dist',
   },
```
package.json添加scripts
```json
  "scripts": {
    "start": "webpack-dev-server --open",   // --open是自动打开浏览器，可去掉
  },
```
运行
```bash
yarn start
# 或者
npm run start
```
**yarn start不会生成dist文件夹，而是直接在内存里**
### 生成CSS文件
安装mini-css-extract-plugin
```bash
yarn add mini-css-extract-plugin --dev
```
webpack.config.js添加
```javascript
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
  plugins: [
    new MiniCssExtractPlugin({
      // Options similar to the same options in webpackOptions.output
      // all options are optional
      filename: '[name].[contenthash].css',
      chunkFilename: '[id].[contenthash].css',
      ignoreOrder: false, // Enable to remove warnings about conflicting order
    }),
  ],
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          {
            loader: MiniCssExtractPlugin.loader,
            options: {
              // you can specify a publicPath here
              // by default it uses publicPath in webpackOptions.output
              publicPath: '../',
              hmr: process.env.NODE_ENV === 'development',
            },
          },
          'css-loader',
        ],
      },
    ],
  },
};
```
### development和production用不同配置
webpack.config.js
```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin')
const path = require('path');

module.exports = {
  mode: 'development',
  entry: './src/index.js',
  output: {
    // path: path.resolve(__dirname, 'dist'),
    filename: '[name].[contenthash].js'
  },
  plugins: [
    new HtmlWebpackPlugin({
      title: 'Custom template',
      // Load a custom template (lodash by default)
      template: 'src/index.html'
    })
  ],
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader']
      },
    ],
  },
  devServer: {
    contentBase: './dist',
  }
};


```
webpack.config.prod.js
```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin')
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const path = require('path');

module.exports = {
  mode: 'production',
  entry: './src/index.js',
  output: {
    // path: path.resolve(__dirname, 'dist'),
    filename: '[name].[contenthash].js'
  },
  plugins: [
    new HtmlWebpackPlugin({
      title: 'Custom template',
      // Load a custom template (lodash by default)
      template: 'src/index.html'
    }),
    new MiniCssExtractPlugin({
      // Options similar to the same options in webpackOptions.output
      // all options are optional
      filename: '[name].[contenthash].css',
      chunkFilename: '[id].[contenthash].css',
      ignoreOrder: false, // Enable to remove warnings about conflicting order
    }),
  ],
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          {
            loader: MiniCssExtractPlugin.loader,
            options: {
              // you can specify a publicPath here
              // by default it uses publicPath in webpackOptions.output
              publicPath: '../',
              hmr: process.env.NODE_ENV === 'production',
            },
          },
          'css-loader',
        ],
      },
    ],
  },
  devServer: {
    contentBase: './dist',
  }
};
```
package.json
start默认配置文件，build指定配置文件为prod
```json
"scripts": {
    "start": "webpack-dev-server",
    "build": "rm -rf dist && webpack --config webpack.config.prod.js", 
  },
```
#### 使用继承
webpack.config.base.js
```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin')
const path = require('path');

module.exports = {
  mode: 'development',
  entry: './src/index.js',
  output: {
    // path: path.resolve(__dirname, 'dist'),
    filename: '[name].[contenthash].js'
  },
  plugins: [
    new HtmlWebpackPlugin({
      title: 'Custom template',
      // Load a custom template (lodash by default)
      template: 'src/index.html'
    })
  ],
};
```
webpack.config.js
```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin')
const path = require('path');
const base = require('./webpack.config.base')   // 引入共有属性

module.exports = {
  ...base,  // 解构
  mode: 'development',
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader']
      },
    ],
  },
  devtool: "inline-source-map",
  devServer: {
    contentBase: './dist',
  }
};
```
webpack.config.prod.js
```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin')
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const path = require('path');
const base = require('./webpack.config.base')

module.exports = {
  ...base,
  mode: 'production',
  plugins: [
    ...base.plugins,
    new MiniCssExtractPlugin({
      // Options similar to the same options in webpackOptions.output
      // all options are optional
      filename: '[name].[contenthash].css',
      chunkFilename: '[id].[contenthash].css',
      ignoreOrder: false, // Enable to remove warnings about conflicting order
    }),
  ],
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          {
            loader: MiniCssExtractPlugin.loader,
            options: {
              // you can specify a publicPath here
              // by default it uses publicPath in webpackOptions.output
              publicPath: '../',
              hmr: process.env.NODE_ENV === 'production',
            },
          },
          'css-loader',
        ],
      },
    ],
  }
};
```
也可以使用merge方法，自行搜索
### 总结
webpack 的作用包括：

1. 将一个或多个 JS 文件打包成对应的文件
1. 将一个或多个 CSS 文件打包成对应的文件
1. 压缩代码
1. 将高版本的 JS转译成低版本的 JS



