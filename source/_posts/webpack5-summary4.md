---
title: webpack5小结-4
date: 2020-10-26 16:56:41
tags:
  - 'node'
  - 'webpack'
categories:
  - 'webpack'
keywords:
description: 'webpack5-开发环境详解-js文件的处理'
---

## js 语法规范检查

**由于项目可能是团队开发,代码风格各异,所以需要引入 eslint 来规范**

1. 首先下载 `npm i eslint-loader eslint -D`
2. 我们这里使用的是`airbnb`,所以还需要下载`npm i eslint-config-airbnb-base eslint-plugin-import -D`
3. 下载完之后要先在`package.json`中进行配置使用

   ```json
   {
     "name": "webpack-wrapper",
     "version": "1.0.0",
     "description": "",
     "main": "webpack.config.js",
     "scripts": {
       "test": "echo \"Error: no test specified\" && exit 1"
     },
     "keywords": [],
     "author": "",
     "license": "ISC",
     "devDependencies": {
       "css-loader": "^5.0.0",
       "eslint": "^7.12.1",
       "eslint-config-airbnb-base": "^14.2.0",
       "eslint-loader": "^4.0.2",
       "eslint-plugin-import": "^2.22.1",
       "html-webpack-plugin": "^4.5.0",
       "style-loader": "^2.0.0",
       "webpack": "^5.2.0",
       "webpack-cli": "^4.1.0"
     },
     "eslintConfig": {
       "extends": "airbnb-base"
     }
   }
   ```

4. 最后在`webpack.config.js`中引入即可

   ```js
   const { resolve } = require('path')
   const HtmlWebpackPlugin = require('html-webpack-plugin')

   module.exports = {
     entry: './src/index.js',
     output: {
       filename: 'main.js',
       path: resolve(__dirname, 'build'),
     },
     mode: 'development',
     module: {
       rules: [
         {
           test: /\.css$/,
           use: ['style-loader', 'css-loader'],
         },
         //注意：只检查自己写的源代码,第三方的库是不用检查的
         {
           test: /\.js$/,
           exclude: /node_modulse/, //不检测依赖中的js
           loader: 'eslint-loader',
           options: {
             fix: true,
           },
         },
       ],
     },
     plugins: [
       new HtmlWebpackPlugin({
         template: './src/index.html',
       }),
     ],
   }
   ```

---

## js 语法兼容处理

**由于`@babel/polyfill`的过时和`webpack5`的到来,这里我们根据`webpack5`来进行 js 的兼容配置**

1. 下载所需要的所有依赖`npm i babel-loader @babel/core @babel/preset-env core-js -D`
2. 在根目录下新建`.babelrc`文件来配置`babel`项

   ```json
   {
     "presets": [
       [
         "@babel/preset-env",
         {
           "useBuiltIns": "usage",
           //usage-会根据你配置(browserslist)的浏览器兼容,来实现按需添加
           "corejs": 3 //这里是对corejs的版本引用的告知
         }
       ]
     ],
     "plugins": []
   }
   ```

3. 在`package.json`中新增`browserslist`配置项

   ```json
   {
     "name": "222",
     "version": "1.0.0",
     "description": "",
     "main": "index.js",
     "scripts": {
       "test": "echo \"Error: no test specified\" && exit 1"
     },
     "keywords": [],
     "author": "",
     "license": "ISC",
     "devDependencies": {
       "@babel/core": "^7.12.3",
       "@babel/preset-env": "^7.12.1",
       "babel-loader": "^8.1.0",
       "core-js": "^3.6.5",
       "html-webpack-plugin": "^4.5.0",
       "webpack": "^5.3.0",
       "webpack-cli": "^4.1.0"
     },
     "browserslist": {
       "development": ["last 3 version", "> 1%", "not ie <= 8"],
       "production": [">0.2%", "not dead", "not op_mini all"]
     }
   }
   ```

4. 在`webpack.config.js`中进行配置引用

   ```js
   const HtmlWebpackPlugin = require('html-webpack-plugin')
   const { resolve } = require('path')
   process.env.NODE_ENV = 'development'

   module.exports = {
     entry: './src/index.js',
     output: {
       filename: 'main.js',
       path: resolve(__dirname, 'build'),
     },
     mode: 'development',
     module: {
       rules: [{ test: /\.js$/, use: 'babel-loader' }],
     },
     plugins: [
       new HtmlWebpackPlugin({
         template: './src/index.html',
       }),
     ],
   }
   ```
