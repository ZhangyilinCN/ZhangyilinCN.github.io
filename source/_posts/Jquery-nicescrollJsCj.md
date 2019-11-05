---
title: 滚动条插件(Jquery-nicescroll)
date: 2019-11-01 11:49:32
tags:
  - "滚动条"
  - "插件"
categories:
  - "插件"
keywords:
description: "滚动条插件(Jquery-nicescroll)"
toc: false
---

## 可以修改滚动条的样式的插件
### 下载地址为：[戳我跳转](https://github.com/inuyaksa/jquery.nicescroll)

---

``` css
.box {
    width: 400px;
    height: 500px;
    overflow: auto;
    border: 1px solid #000;
}
.box p {
    width: 100%;
    height: 100px;
    font-size: 24px;
    line-height: 100px;
    background: gold;
    margin-bottom: 20px;
}
```

``` html 
<div class="box">
    <p>111111111111111111</p>
    <p>2222222222222222222</p>
    <p>33333333333333333333</p>
    <p>444444444444444444444</p>
    <p>5555555555555555555555</p>
</div>
```

``` javascript
// 记得先引入Jquery.js和niscroll.js
$(".box").niceScroll(); // 默认的初始化
$(".box").niceScroll({cursorcolor: "#00F"}); //可修改配置参数的初始化
$(".box").getNiceScroll().hide(); //隐藏滚动条
$(".box").getNiceScroll().remove();   //删除此对象（滚动条）
$(".box").getNiceScroll().resize();  //检测滚动条是否重置大小（当窗口改变大小时）
$(".box").getNiceScroll(0).doScrollLeft(x, duration);  // Scroll X Axis 第一个是位置,第二个是时间(但是使用的时候没有效果...)
$(".box").getNiceScroll(0).doScrollTop(y,duration);  // Scroll Y Axis
```

---

## niscroll 的内置参数表

``` javascript
zindex: "auto",
cursoropacitymin: 0,  // 当滚动条是隐藏状态时改变透明度，值范围1到0
cursoropacitymax: 1,  // 当滚动条是显示状态时改变透明度，值范围1到0
cursorcolor: "#424242",  // 滚动条颜色，使用16进制颜色值
cursorwidth: "6px",  // 滚动条的宽度，单位：像素
cursorborder: "1px solid #fff",  // CSS 方式定义滚动条边框
cursorborderradius: "5px",  // 滚动条圆角（像素）
scrollspeed: 40,  // 滚动速度
mousescrollstep: 9 * 3,  // 鼠标滚动的滚动速度（像素）
touchbehavior: false,   // deprecated  激活拖拽滚动 （不赞成，不宜用）
emulatetouch: false,    // replacing touchbehavior  emulate（仿真）
hwacceleration: true,  // 激活硬件加速
usetransition: true,
boxzoom: false,  // 激活放大box的内容
dblclickzoom: true,  // （仅当 boxzoom=true 时有效）双击 box 时放大
gesturezoom: true,  // （仅 boxzoom=true 和触屏设备时有效）激活变焦当 out/in （两个手指外账或收缩）
grabcursorenabled: true,  // （仅当 透彻behavior=true）显示“抓住”图标 display "grab" icon
autohidemode: true,  // 隐藏滚动条的方式，可用的值：true|无滚动时隐藏，"cursor"|隐藏，false|不隐藏，"leave"|仅在指针离开内容时隐藏，"hidden"|一直隐藏，"scroll"|仅在滚动时显示
background: "",  // 轨道的背景颜色
iframeautoresize: true,  // 在加载事件时自动重置 iframe 大小
cursorminheight: 32,  // 设置滚动条的最小高度（像素）
preservenativescrolling: true,  // 你可以用鼠标滚动可滚动区域的滚动条和增加鼠标滚轮事件
railoffset: false,  // 可以使用 top/left 来修正位置
railhoffset: false, 
bouncescroll: true,  // （only hw accell）启用滚动跳跃的内容移动
spacebarenabled: true,  // 当按下空格时使页面向下滚动
railpadding: {  // 设置轨道的内间距
  top: 0,
  right: 0,
  left: 0,
  bottom: 0
},
disableoutline: true,  // 当选中一个使用 niceScroll 的 div 时，Chrome浏览器中禁用 outline 
horizrailenabled: true,  // niceScroll 可以管理水平滚动
railalign: "right",  // 对齐垂直轨道
railvalign: "bottom",  // 对齐水平轨道
enabletranslate3d: true,  // niceScroll 可以使用 CSS 变型来滚动内容
enablemousewheel: true,  // niceScroll 可以管理鼠标滚轮事件
enablekeyboard: true,  // niceScroll 可以管理键盘事件
smoothscroll: true,  // ease 动画滚动
sensitiverail: true,  // 单击轨道产生滚动
enablemouselockapi: true,  // 可以用鼠标锁定 API 标题（类似对象拖动）
// cursormaxheight:false,
cursorfixedheight: false,  // 修正光标的高度（像素）
directionlockdeadzone: 6,  // 设定死区，为激活方向锁定（像素）
hidecursordelay: 400,  // 设置滚动条淡出的延迟时间（毫秒）
nativeparentscrolling: true,  // 检测内容底部便于让父级滚动
enablescrollonselection: true,  // 当选择文本时激活内容自动滚动
overflowx: true,
overflowy: true,
cursordragspeed: 0.3,  // 设置拖拽的速度
rtlmode: "auto",  // DIV 的水平滚动从左边开始
cursordragontouch: false,  // 使用触屏模式来实现拖拽
oneaxismousemode: "auto",  // 当只用水平滚动时可以用鼠标来滚动，如果设为 false 则不支持水平滚动，如果设为 auto 支持双轴滚动
scriptpath: getScriptPath(),  // 为 boxmode 图片自定义路径
preventmultitouchscrolling: true,  // 防止多触点时间引发滚动
disablemutationobserver: false,
enableobserver: true,
scrollbarid: false
```


