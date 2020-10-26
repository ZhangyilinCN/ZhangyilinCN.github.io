---
title: webpack5小结-3
date: 2020-10-26 10:22:54
tags:
  - 'node'
  - 'webpack'
categories:
  - 'webpack'
keywords:
description: 'webpack5-开发环境详解-样式文件的处理'
---

## 开发模式个生产模式的区别

![webpack-003.png](https://i.loli.net/2020/10/26/7LIN1Xkg8Y6VJWx.png)

---

## 对样式文件的分离处理

**由于打包时，会让 css 整合到 js 中，造成 js 文件过大，出现闪屏现象，所以我们要对 css 进行打包分离**

1. 首先下载`npm i mini-css-extract-plugin -D`这个插件
2. 其次在`webpack.config.js`中进行注入引用,并取代原来的`style-loader`
3. 配置`mini-css`

**注意：因为 css 中可能会有背景图的使用，而打包后，背景图的路径会出现错误，所以一定要配置`MiniCssExtractPlugin.loader--options--publicPath`，这里的路径那些要根据`url-loader--options--outputPath`的导出路径来填写**

```js
const { resolve } = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const MiniCssExtractPlugin = require('mini-css-extract-plugin') //引入

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: resolve(__dirname, 'build'),
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          // 'style-loader', //创建style标签,将样式放入
          //这个loader取代style-loader,作用:提取js中的css成单独文件
          {
            loader: MiniCssExtractPlugin.loader,
            options: {
              publicPath: '../', //注意这里
            },
          },
          'css-loader', //将css文件整合到js中
        ],
      },
      {
        test: /\.(png|jpg|gif)$/,
        loader: 'url-loader',
        options: {
          limit: 8 * 1024,
          name: '[hash:10].[ext]',
          outputPath: 'imgs',
        },
      },
    ],
  },
  mode: 'development',
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
    }),
    new MiniCssExtractPlugin({
      filename: 'css/public.css', //对输出的css文件进行重命名
    }),
  ],
}
```

---

## 对样式文件的兼容处理

**由于浏览器内核版本多种多样，所以还有要对样式文件做兼容处理**

1. 首先下载`npm i postcss-loader postcss-preset-env -D`
2. 在`package.json`和`webpack.config.js`进行配置

- `webpack.config.js`中的配置

  ```js
  const { resolve } = require('path')
  const HtmlWebpackPlugin = require('html-webpack-plugin')
  const MiniCssExtractPlugin = require('mini-css-extract-plugin')

  //因为兼容的环境切换时不看webpack.config.js中的mode设置的,所以需要设置node的环境变量
  process.env.NODE_ENV = 'production' //设置是生产(production)还是开发(development)

  module.exports = {
    entry: './src/index.js',
    output: {
      filename: 'main.js',
      path: resolve(__dirname, 'build'),
    },
    module: {
      rules: [
        {
          test: /\.css$/,
          use: [
            {
              loader: MiniCssExtractPlugin.loader,
              options: {
                publicPath: '../',
              },
            },
            'css-loader',
            {
              loader: 'postcss-loader',
              options: {
                postcssOptions: {
                  plugins: ['postcss-preset-env'],
                  /*如果还需要对此进行设置,可写为
                  plugins: [['postcss-preset-env',{options:xxx}]] */
                },
              },
            },
          ],
        },
        {
          test: /\.(png|jpg|gif)$/,
          loader: 'url-loader',
          options: {
            limit: 8 * 1024,
            name: '[hash:10].[ext]',
            outputPath: 'imgs',
          },
        },
      ],
    },
    mode: 'development',
    plugins: [
      new HtmlWebpackPlugin({
        template: './src/index.html',
      }),
      new MiniCssExtractPlugin({
        filename: 'css/public.css',
      }),
    ],
  }
  ```

- `package.json`中的配置

  ```json
  {
    "name": "webpack-wrapper",
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
      "css-loader": "^5.0.0",
      "file-loader": "^6.1.1",
      "html-webpack-plugin": "^4.5.0",
      "mini-css-extract-plugin": "^1.2.0",
      "postcss-loader": "^4.0.4",
      "postcss-preset-env": "^6.7.0",
      "style-loader": "^2.0.0",
      "url-loader": "^4.1.1",
      "webpack": "^5.2.0",
      "webpack-cli": "^4.1.0",
      "webpack-dev-server": "^3.11.0"
    },
    "browserslist": {
      "development": [
        //开发环境
        "last 1 chrome version", //兼容最近的一个chrome版本
        "last 1 firefox version",
        "last 1 safari version"
      ],
      "production": [
        //生成环境(默认)
        //其中的配置写法也可以github--browserslist查询
        ">0.2%", //兼容大于99.8%的浏览器
        "not dead", //不要已经死了的浏览器
        "not op_mini all" //不要所有的op_mini浏览器
      ]
    }
  }
  ```

---

## 对样式文件的压缩处理

**插件`npm i optimize-css-assets-webpack-plugin -D`,之后进行配置**

```js
const { resolve } = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const MiniCssExtractPlugin = require('mini-css-extract-plugin')
const optimizeCssAssetsWebpackPlugin = require('optimize-css-assets-webpack-plugin')

process.env.NODE_ENV = 'production'

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: resolve(__dirname, 'build'),
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          {
            loader: MiniCssExtractPlugin.loader,
            options: {
              publicPath: '../',
            },
          },
          'css-loader',
          {
            loader: 'postcss-loader',
            options: {
              postcssOptions: {
                plugins: ['postcss-preset-env'],
              },
            },
          },
        ],
      },
      {
        test: /\.(png|jpg|gif)$/,
        loader: 'url-loader',
        options: {
          limit: 8 * 1024,
          name: '[hash:10].[ext]',
          outputPath: 'imgs',
        },
      },
    ],
  },
  mode: 'development',
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
    }),
    new MiniCssExtractPlugin({
      filename: 'css/public.css',
    }),
    new optimizeCssAssetsWebpackPlugin(), //压缩css
  ],
}
```
