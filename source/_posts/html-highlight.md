---
title: 前端处理关键词高亮
date: 2022-03-18 15:24:00
tags:
  - "Javascript"
categories:
  - "Javascript"
keywords:
description: "根据关键词把html段落中的词高标显示（支持多个关键词和html中有img标签兼容）"
toc: false
---

```javascript
/*
其中content为html内容，keyword为关键词（支持string和arr）
*/
htmlHighlightFn(content, keyword){
    if(content) {
        if(keyword){
            let commonUUId = 'htmlHighlight202203171112' //设置一个用于替换img标签的唯一标识
            let regex = /<img.*?(?:>|\/>)/g //img的正则
            let imgArr = content.match(regex) //把html中的所有img放到一个arr
            let replaceHtml = content.replace(regex,commonUUId) //把html中所有的img替换为UUID
            let mainHtml = replaceHtml.split(commonUUId) //把替换后的html变为arr（不使用str直接替换，是防止出现关键词过短和UUID其中内容相匹配的BUG）
            let returnContentArr = [] //操作后的arr
            let num = 0
            let htmlContent = ''
            if(Array.isArray(keyword)) { //如果关键词为数组（多个关键词）
                mainHtml.forEach(ele=>{
                    let beforeContent = ele
                    if(ele) {
                        keyword.forEach(item => {
                            let newContent = beforeContent.split(item)
                            let lastContent = newContent.join(`<span style='color:red'>${item}</span>`)
                            beforeContent = lastContent
                        })
                        returnContentArr.push(beforeContent)
                    }else {
                        returnContentArr.push('')
                    }
                })
            }else { //单个关键词
                mainHtml.forEach(ele=>{
                    let newContent = ele.split(keyword)
                    let lastContent = newContent.join(`<span style='color:red'>${keyword}</span>`)
                    returnContentArr.push(lastContent)
                })
            }
            returnContentArr.forEach((item,index)=>{
                //自己处理split的一些兼容
                if(index === 0 && !item) {
                    num=1
                }
                if(item) {
                    if(ImgArr) {
                        htmlContent += imgArr[index - num] + item
                    }else {
                        htmlContent += item
                    }
                }
            })
            return htmlContent
        }else {
            return content
        }
    }
}
```
