---
title: el-table错位问题
date: 2024-07-26 17:20:19
tags:
  - "ElementUi"
  - "Vue"
categories:
  - "ElementUi"
keywords:
description: "解决flex布局下，左侧栏展开收起，右侧的table错位问题"
toc: false
---

```css
.el-table__header,
  .el-table__body,
  .el-table__footer {
    width: 100% !important;
  }
  .el-table__header colgroup col[name="gutter"] {
    width: 8px !important;  //这个宽度要设置为你自定义table-滚动条的宽度
  }
```
