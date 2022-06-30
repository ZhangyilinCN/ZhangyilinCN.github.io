---
title: '解决el-Cascader级联选择器回显bug'
date: 2022-06-30 20:22:58
tags:
  - 'ElementUi'
  - 'Vue'
categories:
  - 'ElementUi'
keywords:
description: '解决第二次点击选择器没有初始化'
toc: false
---


``` javascript
resetCascaderFn() {
    if(this.$refs.myCascader){
        this.$refs.myCascader.$refs.panel.checkedValue = []
        this.$refs.myCascader.$refs.panel.clearCheckedNodes()
        this.$refs.myCascader.$refs.panel.activePath = []
        this.$refs.myCascader.$refs.panel.syncActivePath()
        // this.$refs.myCascader.$refs.panel.scrollInttoView()
        this.$refs.myCascader.$refs.input.$refs.input.setAttribute("aria-expanded",false)
        this.$refs.myCascader.$emit('visible-change',false)
        this.$refs.myCascader.$refs.panel.$emit('visible-change',false)
        this.$refs.myCascader.$emit('close')
    }
}
```

