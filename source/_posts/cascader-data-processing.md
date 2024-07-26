---
title: Cascader级联选择器的value处理
date: 2024-07-26 17:29:31
tags:
  - "Javascript"
  - "React"
  - "ElementUi"
categories:
  - "Javascript"
keywords:
description: "后端只返回子id,前端处理获取父id,拼接成数组用于级联选择器的展示"
toc: false
---

## Cascader 级联选择器的 value 处理

**_后端只返回子 id,前端处理获取父 id,拼接成数组用于级联选择器的展示_**

```js
const findParentsId = (treeData, id) => {
  if (treeData.length == 0) return;
  for (let i = 0; i < treeData.length; i++) {
    if (treeData[i].value == id) {
      return [];
    } else {
      if (treeData[i].children) {
        let res = findParentsId(treeData[i].children, id);
        if (res !== undefined) {
          return res.concat(treeData[i].value).reverse();
        }
      }
    }
  }
};
const orgChildIdFindParent = (childId, orgList = []) => {
  console.log(childId, orgList);
  const result = findParentsId(orgList, childId)?.concat(childId);
  return result || [];
};
const arr = orgChildIdFindParent("1001(子元素id)", "optionsArr(options数组)"); // ['1','100','1001']
```
