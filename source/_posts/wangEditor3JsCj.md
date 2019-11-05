---
title: wangEditor富文本
date: 2019-11-01 12:03:31
tags:
  - "富文本"
  - "插件"
categories:
  - "插件"
keywords:
description: "wangEditor富文本基本使用"
toc: false
---

# 首先下载插件：[戳我跳转](https://github.com/wangfupeng1988/wangEditor/releases)

## 传统创建
```html
<div id="editor"></div>
```
```javascript
var E = window.wangEditor;
var editor = new E("#editor");
editor.create();
```
---
## 分离创建 
``` html 
<div id="ed1" class="title"></div>
<div id="ed2">我是中间空的</div>
<div id="ed3" class="text"></div>
```
```javascript
var E2=window.wangEditor;
var ed=new E2('#ed1','#ed3');
ed.create();
ed.$textElem.attr('contenteditable', true); //开启与关闭文本框的编辑使用
```
---
## 初始化文字
``` javascript 
ed.txt.html('<p>我是JS添加的文字</p>') //使用js初始化添加文字
ed.txt.append('<p>我是js追加的文字</p>') //使用js追加的文字
ed.txt.clear(); //可以让文本框中内容清空
```
---
## 读取内容
``` javascript 
alert(ed4.txt.html()) //获取的是文本框中带有标签的内容
alert(ed4.txt.html()) //获取其中纯文本
```
---
## 读使用textarea,在文本框中输入，会同步到textarea中
``` javascript 
var E5=window.wangEditor;
var text=$('textarea');
var ed5=new E5('#ed5');
ed5.customConfig.οnchange=function (html) {
   text.val(html)
};
ed5.create();
text.val(ed5.txt.html())
```
---
## 自定义菜单项
``` javascript 
ed.customConfig.menus=[   //使用哪个写哪个就行
     'head',  // 标题
     'bold',  // 粗体
     'fontSize',  // 字号
     'fontName',  // 字体
     'italic',  // 斜体
     'underline',  // 下划线
     'strikeThrough',  // 删除线
     'foreColor',  // 文字颜色
     'backColor',  // 背景颜色
     'link',  // 插入链接
     'list',  // 列表
     'justify',  // 对齐方式
     'quote',  // 引用
     'emoticon',  // 表情
     'image',  // 插入图片
     'table',  // 表格
     'video',  // 插入视频
     'code',  // 插入代码
     'undo',  // 撤销
     'redo'  // 重复
 ]
```
---
## 定义debug模式
``` javascript 
var E2=window.wangEditor;
var ed2=new E2('#ed2');
// 实际开发中不建议直接定义为true或者false，可通过 url 参数进行干预：
// 通过 url 参数配置 debug 模式。url 中带有 wangeditor_debug_mode=1 才会开启 debug 模式
ed2.customConfig.debug = location.href.indexOf('wangeditor_debug_mode=1') > 0
ed2.create()
```
---
## 配置onchange函数
``` javascript 
var E3=window.wangEditor;
var ed3=new E3('#ed3');
ed3.customConfig.οnchange=function (html) {
     console.log(html);   //当文本框中的内容发生改变时，才会触发
}
// 自定义 onchange 触发的延迟时间，默认为 200 ms
// ed3.customConfig.onchangeTimeout = 1000 // 单位 ms
// ed3.create();
$('button').on('click',function () {
     ed3.txt.append('<p>111</p>')   //注意在js中添加的内容不会触发此函数行为，需要手动使用  ed3.change()
    ed3.change && ed3.change()
 })
```
---
## 配置编辑区的z-index 默认10000 注意次修改将同时修改菜单栏和文本框
``` javascript 
ed4.customConfig.zIndex=100;
```
---
## 自定义菜单项中的语言
``` javascript 
ed5.customConfig.lang = {
     '设置标题': 'title',
     '正文': 'p',
     '链接文字': 'link text',
     '链接': 'link',
     '上传图片': 'upload image',
     '上传': 'upload',
     '创建': 'init'
     // 还可自定添加更多
 }
// 以上代码中的链接文字要写在链接前面，
// 上传图片要写在上传前面，因为前者包含后者。
// 如果不这样做，可能会出现替换不全的问题，切记切记！
```
---


## 粘贴文本
``` javascript 
ed5.customConfig.lang = {
     '设置标题': 'title',
     '正文': 'p',
     '链接文字': 'link text',
     '链接': 'link',
     '上传图片': 'upload image',
     '上传': 'upload',
     '创建': 'init'
     // 还可自定添加更多
 }
// 以上代码中的链接文字要写在链接前面，
// 上传图片要写在上传前面，因为前者包含后者。
// 如果不这样做，可能会出现替换不全的问题，切记切记！
```
---

## 自定义菜单项中的语言
``` javascript 
ed5.customConfig.lang = {
     '设置标题': 'title',
     '正文': 'p',
     '链接文字': 'link text',
     '链接': 'link',
     '上传图片': 'upload image',
     '上传': 'upload',
     '创建': 'init'
     // 还可自定添加更多
 }
// 以上代码中的链接文字要写在链接前面，
// 上传图片要写在上传前面，因为前者包含后者。
// 如果不这样做，可能会出现替换不全的问题，切记切记！
```
---

## 自定义菜单项中的语言
``` javascript 
ed5.customConfig.lang = {
     '设置标题': 'title',
     '正文': 'p',
     '链接文字': 'link text',
     '链接': 'link',
     '上传图片': 'upload image',
     '上传': 'upload',
     '创建': 'init'
     // 还可自定添加更多
 }
// 以上代码中的链接文字要写在链接前面，
// 上传图片要写在上传前面，因为前者包含后者。
// 如果不这样做，可能会出现替换不全的问题，切记切记！
```
---

## 自定义菜单项中的语言
``` javascript 
ed5.customConfig.lang = {
     '设置标题': 'title',
     '正文': 'p',
     '链接文字': 'link text',
     '链接': 'link',
     '上传图片': 'upload image',
     '上传': 'upload',
     '创建': 'init'
     // 还可自定添加更多
 }
// 以上代码中的链接文字要写在链接前面，
// 上传图片要写在上传前面，因为前者包含后者。
// 如果不这样做，可能会出现替换不全的问题，切记切记！
```
---

## 自定义菜单项中的语言
``` javascript 
ed5.customConfig.lang = {
     '设置标题': 'title',
     '正文': 'p',
     '链接文字': 'link text',
     '链接': 'link',
     '上传图片': 'upload image',
     '上传': 'upload',
     '创建': 'init'
     // 还可自定添加更多
 }
// 以上代码中的链接文字要写在链接前面，
// 上传图片要写在上传前面，因为前者包含后者。
// 如果不这样做，可能会出现替换不全的问题，切记切记！
```
---
