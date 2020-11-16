---
title: webpack小结-2
date: 2020-10-22 17:22:53
tags:
  - 'node'
  - 'webpack'
categories:
  - 'webpack'
keywords:
description: 'webpack-各种资源的loader/plugins以及devServer的配置详解'
---

## webpack.config.js 用处

### 在根目录创建 webpack.config.js 进行 webpack 的配置

**作用：指示 webpack 干哪些活(当你运行 webpack 指令时,会加载里面的配置)**
**所有构件工具都是基于 node.js 平台运行的,模块化默认采用 common.js**

---

## 打包样式资源

**下载完 loader 之后,在 webpack.config.js 中的 module-rules 下进行配置即可**

- 解析 css 资源

  `npm i style-loader css-loader -D`

- 解析 less 资源

  `npm i less less-loader -D`

- 解析 scss 资源

  `npm i node-sass sass-loader -D`

```js
//resolve用来拼接绝对路径的方法
const { resolve } = require('path')

module.exports = {
  //webpack配置
  entry: './src/index.js', //入口起点
  output: {
    filename: 'main.js', //输出的文件名
    path: resolve(__dirname, 'build'), //输出的路径
    // __dirname node.js的变量,代表当前文件的目录绝对路径
  },
  //   loader配置：1.下载 2.使用(配置loader)
  module: {
    // 规则
    rules: [
      //详细的loader配置
      {
        test: /\.css$/, //正则表示比配哪些文件
        use: [
          //use数组中的loader执行顺序是：从右到左,从下到上一次执行
          'style-loader', //创建style标签,将js中的样式资源插入进去,添加到header中生效
          'css-loader', //将css文件变成common.js模块加载到js中,里面内容是样式字符串
        ],
      },
      {
        test: /\.less$/,
        use: [
          //数组内的loader顺序固定,从下往上，从后往前依次编译,且每个对象中的loader不共享,所以这个对象中需要3个loader,而不是less-loader这一个；
          'style-loader',
          'css-loader',
          'less-loader', //将less文件编译为css文件
        ],
      },
      {
        test: /\.scss$/,
        use: [
          'style-loader',
          'css-loader',
          'sass-loader', //将scss文件编译为css文件
        ],
      },
    ],
  },
  //   plugins配置
  plugins: [],
  //   指定打包模式
  mode: 'development', //开发模式(development)和生产模式(produciton)
}
```

---

## 打包 html 资源

1. 首先需要下载插件 `npm i html-webpack-plugin -D`
2. 之后要在`webpack.config.js`中,头部进行引用
3. 最后在`plugins`中进行配置

```js
const { resolve } = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: resolve(__dirname, 'build'),
  },
  module: {},
  plugins: [
    //   plugins配置 1.下载 2.引用 3.使用
    //html-webpack-plugin
    //功能：默认会创建一个空的HTML,自动引入打包的所有资源(js/css)
    new HtmlWebpackPlugin({
      //复制'./src/index.html'文件，并自动引入打包输出的所有资源(js/css)
      template: './src/index.html',
    }),
  ],
  mode: 'development',
}
```

---

## 打包图片资源

- 如果图片资源在 css 内,如`background-image`：

  1. 使用命令行下载 loader: `npm i url-loader file-loader -D`
  2. 在`webpack.config.js`中配置即可

- 如果图片资源在 html 内,如`img`,在还要额外下载 loader: `npm i html-loader -D`
  1. 注意：因为在 src 下的 html 中的 img 使用的是相对路径,所以打包后的 html 并找不到此路径下的文件资源,所以需要在`outout下为publicPath指定路径`

```js
const { resolve } = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: resolve(__dirname, 'build'),
    publicPath: './', //在这里指定公共路径
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          'style-loader',
          'css-loader',
        ],
      },
      {
        //处理图片资源
        test: /\.(jpg|png|gif)$/,
        loader: 'url-loader', //多个为数组,只写一个的话可以为loader:的字符串
        options: {
          /*图片大小小于8kb,就会被base64处理,一般为8-12kb
            优点:减少请求数量(减轻服务器压力)
            缺点:图片体积会更大(文件请求速度更慢)*/
          limit: 8 * 1024,
          /*给图片重命名,
            [hash:10]表示取图片的hash的前10位,
            [ext]表示取文件原来的扩展名
          */
          name: '[hash:10].[ext]',
        },
      },
      {
        test: /\.html$/, //处理html文件的img图片(负责引入img,从而能被url-loader进行处理)
        loader: 'html-loader',
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
    }),
  ],
  mode: 'development',
```

---

## 打包其他资源

**其他资源(除了 html/js/css 资源以外的资源)-不需要做任何处理，直接原封不动的输出出去就可以了的**

1. 首先使用`npm i file-loader -D`下载
2. 然后在`webpack.config.js`中配置即可

```js
const { resolve } = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

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
        use: ['style-loader', 'css-loader'],
      },
      {
        /*  test-为匹配,exclude-为排除
            exclude: /\.(css|js|html|jpg|png|gif|less...)$/ */
        test: /\.(eot|svg|ttf|woff|woff2)/,
        loader: 'file-loader',
        options: {
          name: '[hash:10].[ext]', //使打包后的文件名短一些
        },
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
    }),
  ],
  mode: 'development',
}
```

---

## 本地服务器 devServer

**使用`npm i webpack-dev-server -D`下载,之后在进行配置**
**开发服务器 devServe-用来自动化(自动编译,自动打开浏览器，自动刷新浏览器....)**
**特点：只会在内存中编译打包,不会有任何输出,防止了每次修改后都要重新打包编译才能看到效果**
**启动 devServe 指令为: `npx webpack-dev-server`/webpack5 以上为`npx webpack serve`**

```js
const { resolve } = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

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
        use: ['style-loader', 'css-loader'],
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
    }),
  ],
  mode: 'development',
  devServer: {
    contentBase: resolve(__dirname, 'build'), //项目构建后的路径
    compress: true, //启动gzip压缩
    port: 3000, //端口号
    open: true, //自动打开浏览器
  },
}
```

---

## 分类打包输出

**每次打包输出都会在 build 文件夹下生成许多文件,为了打包后的文件清晰,我们可以在配置中的`module-rules-options-outputPath`来指定打包后的文件夹**

```js
const { resolve } = require('path')
const HtmlWebpackPlugins = require('html-webpack-plugin')

module.exports = {
  entry: './src/js/index.js',
  output: {
    filename: 'js/main.js',
    path: resolve(__dirname, 'build'),
    publicPath: './',
  },
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: ['style-loader', 'css-loader', 'sass-loader'],
      },
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader'],
      },
      {
        test: /\.(png|jpg|gif)$/,
        loader: 'url-loader',
        options: {
          limit: 8 * 1024,
          name: '[hash:10].[ext]',
          outputPath: 'imgs', //这里的outputPath设置,便是设置此类文件打包后所去往的去处
        },
      },
      {
        test: /\.html$/,
        loader: 'html-loader',
      },
      {
        test: /\.(eot|woff|woff2|ttf|svg)$/,
        loader: 'file-loader',
        options: {
          name: '[hash:10].[ext]',
          outputPath: 'fonts',
        },
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugins({
      template: './src/index.html',
    }),
  ],
  mode: 'development',
  devServer: {
    contentBase: resolve(__dirname, 'build'),
    compress: true,
    open: true,
    port: 3000,
  },
}
```