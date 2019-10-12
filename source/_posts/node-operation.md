---
title: "节点的操作"
date: 2019-10-11 16:03:47
tags:
  - "Dom"
  - "Javascript"
categories:
  - "Javascript"
keywords:
description: "简单的记录下原生js节点的各个操作方式"
toc: false
---

- **appendChild(节点)-添加**

```javascript
let oul = document.getElementsByTagName("ul")[0];
let newOli = document.createElement("li");
oul.appendChild(newOli);
//在oul下的末尾添加一个newOli的节点
```

- **insertBefore(要插入的节点，参照点)-插入**

```javascript
let oul = document.getElementsByTagName("ul")[0];
let newOli = document.createElement("li");
oul.insertBefore(newOli, oul.children[2]);
//在oul下把newOli插入到第二个节点之前
```

- **replaceChild(要插入的节点，参照点)-替换**

```javascript
let oul = document.getElementsByTagName("ul")[0];
let newOli = document.createElement("li");
oul.replaceChild(newOli, oul.children[2]);
//在oul下用newOli替换掉第二个节点
```

- **removerChild(要删除的节点)-删除**

```javascript
let oul = document.getElementsByTagName("ul")[0];
oul.removeChild(oul.children[2]);
//在oul下删除第二个节点
```

- **cloneNode(flag)-复制**

```javascript
let oul = document.getElementsByTagName("ul")[0];
let newOli = oul.children[2].cloneNode(true);
let newOli1 = oul.children[2].cloneNode(false);
//复制oul下的第二个节点,true为深复制、false为浅复制
```
