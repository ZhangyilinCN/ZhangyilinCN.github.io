---
title: Vue列表动画
date: 2019-11-11 17:24:53
tags:
  - "Vue"
categories:
  - "Vue"
keywords:
description: "Vue列表动画"
toc: false
---

## 单一的使用<transition>标签来控制动画过渡
## 而使用v-for生成渲染出的则需要使用<transition-group>标签来控制
``` html
<transition-group appear tag="ul" >
    <li v-for="(item,i) in list" :key="item.id">{{item.id}}_______{{item.name}}
        <a href="javascript:;" @click="del(i)">移除</a>
    </li>
</transition-group>
```
**注意： 为`v-for`创建出来的元素设置动画，必须为每一个添加`：key`属性**

**此外还可以给`<transition-group>`添加`appear`属性：实现入场的动画过渡效果**

**使用`<transition-group>`时，会在审查元素中多渲染出`<span>`标签，为了遵循w3c，可以给予`tag='ul'`，来让此渲染成`ul标签`**

**应为是列表（多个）的动画，所以在css中多出了个`v-move` 属性；**

**`v-move` 表示元素在改变定位的过程中应用（例如删除上一个，下面的也会再次触发动画过渡）**

**如果要使用`v-move`时，一定要在`v-leave-active`中加上 `position：absolute`属性，**

**也可以在`<transition-group>`标签中 添加 `move-class="xxx"`（多用于第三方库，或提前写好的css动画样式）**

``` css
.v-move {
     transition: all 1.5s;
}
.v-leave-active {
     position: absolute;
}
```





