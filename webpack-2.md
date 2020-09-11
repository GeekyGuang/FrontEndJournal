# webpack-2

### loader与plugin的区别
- loader是加载器，plugin是插件
- loader主要用来加载一个一个的文件，比如可以加载js文件，把js转译成低版本浏览器支持的js，也可以加载css文件，把css加载成页面上的style标签，也可以加载图片文件，对图片进行优化
- plugin用来加强webpack功能，比如有个插件叫HtmlWebpackPlugin，用来生成一个html文件，还有miniCssExtractPlugin，用来抽取css的代码生成一个css文件
### 引入SCSS
node-sass已经过时，改用dart-sass
css文件后缀改成.scss就是合法的scss文件, 用$声明变量
搜索：webpack scss loader


安装
```bash
yarn add sass-loader dart-sass --dev
```
添加配置
```javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.s[ac]ss$/i,
        use: [
          'style-loader',
          'css-loader',
          {
            loader: 'sass-loader',
            options: {
              // Prefer `dart-sass`
              implementation: require('dart-sass'),
            },
          },
        ],
      },
    ],
  },
};
```
### 引入less
将css后缀改为less
语法用@声明变量
```less
@color: red;
body {
    background: @color;
}
```
安装
```bash
yarn add less-loader less --dev
```
添加配置
```javascript
module.exports = {
    ...
    module: {
        rules: [{
            test: /\.less$/,
            use: [{
                loader: "style-loader" // creates style nodes from JS strings
            }, {
                loader: "css-loader" // translates CSS into CommonJS
            }, {
                loader: "less-loader" // compiles Less to CSS
            }]
        }]
    }
};
```
或者
```javascript
module.exports = {
    ...
    module: {
        rules: [{
            test: /\.less$/,
            loader: ["style-loader","css-loader","less-loader"]
        }]
    }
};
```
### 引入stylus
后缀为.styl
```css
c = red;
body {
    background: c;
}
```
安装
```bash
yarn add stylus-loader stylus --dev
```
配置
```javascript
{
  test: /\.styl$/,
    loader: ["style-loader","css-loader","stylus-loader"]
}
```
### file-loader引入图片
安装
```bash
yarn add file-loader --dev
```
添加配置
```javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.(png|jpg|gif)$/,
        use: [
          {
            loader: 'file-loader',
            options: {}
          }
        ]
      }
    ]
  }
}
```
js导入图片
```javascript
import png from './1.png'   // 将文件导入成路径

const div = document.getElementById('app')
div.innerHTML = `
  <img src="${png}">
`
```
### 懒加载
不得不加载时才加载(按需加载)
新建一个lazy.js文件
```javascript
export default function lasy(){
    console.log("我是一个懒加载模块")
}
```
在另一个js文件里使用懒加载
懒加载会得到一个promise，成功时执行什么，失败时执行什么
```javascript
const button = document.createElement('button')
button.innerText = '懒加载'
button.onclick = ()=>{
    const promise = import('./lazy.js')
    promise.then((module)=>{
        const fn = module.default
        fn()
    },()=>{})
}
div.appendChild(button)
```
### 上传到github
先yarn build
把源代码上传到master分支，排除dist和node_module文件夹


新建gh-pages分支
```bash
git branch gh-pages
```
切换到gh-pages分支
```bash
git checkout gh-pages
```
删除文件，只留下dist, node_module，.gitignore
将dist文件夹里的文件移到根目录
```bash
mv dist/* ./
```
提交到github: gst  ga .  gc  gp报错
```bash
git push --set-upstream origin gh-pages
```
到github设置github pages
#### 用脚本一键上传
返回master分支
```bash
git checkout master
```
新建deploy.sh
```bash
yarn build &&
git checkout gh-pages &&
rm -rf *.html *.js *.css *.png &&
mv dist/* ./ &&
rm -rf dist;
git add . &&
git commit -m "update" &&
git push &&
git checkout -  # 回到上一个分支
```
在master执行
```bash
sh ./deploy.sh
```
### 上传到gitee
新建origin
```bash
git remote add gitee git@gitee.com:XG_GX/webpack-demo.git   # 把origin改成了gitee
```
查看源
```bash
 git remote -v
```
将gh-pages分支上传到gitee的master
```bash
git push gitee gh-pages:master
```


