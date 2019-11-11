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
---

**首先下载插件：[戳我跳转](https://github.com/wangfupeng1988/wangEditor/releases)**

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

## 插入网络图片的回调
``` javascript 
ed1.customConfig.linkImgCallback = function (url) { //可以在css中定义图片的大小
    console.log(url) // url 即插入图片的地址
}
```
---

## 插入链接的效验
``` javascript 
ed2.customConfig.linkCheck = function (text, link) {
     console.log(text) // 插入的文字
     console.log(link) // 插入的链接
     return true // 返回 true 表示校验成功
     // return '验证失败' // 返回字符串，即校验失败的提示信息
}
```
---

## 插入网络图片的效验
``` javascript 
ed3.customConfig.linkImgCheck = function (src) {
     console.log(src) // 图片的链接
     return true // 返回 true 表示校验成功
     // return '验证失败' // 返回字符串，即校验失败的提示信息
}
```
---

## 配置onfocus函数
``` javascript 
ed4.customConfig.οnfοcus=function () {  //文本框获焦执行此函数
     console.log('获焦触发的函数1');
}
 ed4.customConfig.οnblur=function () {  //文本框失焦执行此函数
    console.log('失焦触发的函数2');
}
```
---

## 配置字体与背景色
``` javascript 
ed5.customConfig.colors=[
     '#000000',
     '#ff0000',
     '#00ff00',
     '#0000ff',
]
```
---

## 配置字体
``` javascript 
ed6.customConfig.fontNames = [
     '宋体',
     '微软雅黑',
     'Arial',
     'Tahoma',
     'Verdana'
]
```
---

## 配置表情
``` javascript 
ed7.customConfig.emotions=[{
         title:'默认',
         type:'image',
         content:[{
                 src : "http://img.t.sinajs.cn/t35/style/images/common/face/ext/normal/7a/shenshou_thumb.gif",
                 alt : "[草泥马]"
             },
             {
                src : "http://img.t.sinajs.cn/t35/style/images/common/face/ext/normal/60/horse2_thumb.gif",
                 alt : "[神马]"
             }
         ]
     },
     {
         title:'emoji',
         type:'emoji',
         content:['☸','✈','〠','♚','☎']
     }
 ]
```
---


## 配置表情 从json文件中取
``` javascript 
var box=[];
for(var i=0;i<data.length;i++){
     var b={title:data[i].title,type:data[i].type,content: data[i].content}
     box.push(b)
}
ed7.customConfig.emotions=box
```
---

## 上传图片
``` javascript 
// 下面两个配置，使用其中一个即可显示“上传图片”的tab。但是两者不要同时使用！！！
ed8.customConfig.uploadImgShowBase64=true; //使用 base64 保存图片
ed8.customConfig.uploadImgServer='/upload'（url）;  //上传到服务器
ed8.customConfig.uploadImgMaxSize = 3 * 1024 * 1024 // 将图片大小限制为 3M
ed8.customConfig.uploadImgMaxLength = 5 //默认为 10000 张（即不限制），需要限制可自己配置
ed8.customConfig.uploadFileName = 'yourFileName'  //自定义 fileName
```
---


## 显示与隐藏网络图片上传
``` javascript 
ed9.customConfig.showLinkImg=false; //隐藏网络图片项
ed9.customConfig.uploadImgServer='/upload';  //上传到服务器
```
---
