# webpack4 & React ( not create-react-app )
---
> 这是一个react和webpack4结合的自定义项目, 用到的包包括:
+ react
+ react-dom
+ babel-core
+ babel-loader
+ babel-preset-env
+ babel-preset-react
+ html-webpack-plugin
+ webpack
+ webpack-cli
+ webpack-dev-server

### 我的部署步骤:
1. 创建项目目录
```
  mkdir react_custom
  cd react_custom
```
2. 初始化npm, 自动生成`package.json`文件
```
  npm init -y
```
3. 下载项目生产依赖`react`包
```
  npm i -S react react-dom
```
4. 下载`webpack`包
```
  npm i -D webpack webpack-dev-server webpack-cli
```
5. 下载babel包
```
  npm i -D babel-core babel-loader babel-preset-env babel-preset-react html-plugin-webpack
```
6. 项目目录下创建`webpack.config.js`文件
```
  // webpack.config.js
  const path = require('path');
  const HtmlWebpackPlugin = require('html-webpack-plugin');

  module.exports = {
    // 入口文件
    entry: './src/index.js',
    // 输出位置
    output: {
      path: path.join(__dirname, '/dist'),
      filename: 'index_bundle.js'
    },
    module: {
      rules: [
        {
          test: /\.js$/,
          exclude: /node_modules/,
          use: {
            loader: 'babel-loader'
          }
        }
      ]
    },
    plugins: [
      new HtmlWebpackPlugin({
        template: './src/index.html'
      })
    ]
  }
```
7. 项目目录下创建`src`文件夹, `src`下创建`index.js`和`index.html`文件
```
  // index.js
  import React from 'react';
  import ReactDOM from 'react-dom';
  import App from './components/App';

  ReactDOM.render(<App />, document.getElementById('app'));
```
```
  // index.html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>My React App</title>
  </head>
  <body>
    <div id="app"></div>
  </body>
  </html>
```
8. `src`目录下创建`components`文件夹, `components`创建`App.js`文件
```
  // App.js
  import React, { Component } from 'react';

  class App extends Component {
    render () {
      return (
        <div>
          <h1>My React App</h1>
        </div>
      )
    }
  }

  export default App;
```
9. 修改package.json下的scripts属性
```
  "scripts": {
    "start": "webpack-dev-server --mode development --open --hot",
    "build": "webpack --mode production"
  }
```
10. 项目搭建完成, 运行`npm start`在生产环境运行, 运行`npm run build`生成`dist`文件夹


