---
title: '可编辑div中实现粘贴功能'
date: 2022-11-18 17:49:36
tags:
  - "Dom"
  - "Javascript"
  - "Demo"
  - 'Html'
  categories:
  - "Javascript"
  keywords:
description: "在可编辑div中粘贴-实现粘贴本地图片和粘贴去除标签的纯文字功能"
toc: false
---


``` html
<div
    class="textarea"
    contenteditable="true"
    placeholder="请输入消息"
    ref="imChatText"
    @focus="changeContentValue"
    @input="changeContentValue"
    @blur="chatTextBlur"
    @paste="onNewsPaste"
></div>

```

``` javascript
changeContentValue() {
    // 更新值
    this.chatText = this.$refs.imChatText.innerHTML;
},
// 输入框的失去焦点事件, 解决微信中的bug
chatTextBlur() {
    window.scroll(0, 0);
},
onNewsPaste(event) {
    let items = event.clipboardData && event.clipboardData.items;
    let file = null;
    let fileURL = null;
    const selection = window.getSelection();
    let paste = "";
    if (window.clipboardData && window.clipboardData.setData) {
        // IE
        paste = window.clipboardData.getData("text");
    } else {
        paste =
            (event.originalEvent || event).clipboardData.getData(
                "text/plain"
            ) || "";
    }
    selection.deleteFromDocument();
    if (items && items.length) {
    let filterItem = items;
    // 检索剪切板items
    for (let i = 0; i < filterItem.length; i++) {
        if (filterItem[i].type.indexOf("image") !== -1) {
            file = filterItem[i].getAsFile();
             //let file是个file文件，如果后端需要blob的话记得转换let blob = new Blob([file], { type: 'image/png' || 'application/*' });
            if (file.name == "image.png") {
                //如果是截屏的直接粘贴就跳过
                event.preventDefault();
            } else {
                 //URL.createObjectURL(file) 这里是暂存的blob地址，并不是真正的地址，要把file参数上传给后端，获取网络地址，再用于显示
                 //URL.createObjectURL(file) 出来的blob地址，在不用的时候（如发送后，页面离开时）记得URL.revokeObjectURL(item.name);释放掉，避免相应的内存损耗，
                fileURL = URL.createObjectURL(file);
                this.blobUrlToFlieArr = [
                    ...this.blobUrlToFlieArr,
                    { name: fileURL, file },
                ]; // 这边是把粘贴的图片都存到一个对象中，等点击上传按钮的时候再把和页面所匹配的name的图片上传
                let fragment = selection
                    .getRangeAt(0)
                    .createContextualFragment(
                        `<img  data-info='diaImWeb' src=${fileURL} class='pasteImgs' />`
                    ); //这里的显示只针对与编辑框中的本地查看
                selection
                    .getRangeAt(0)
                    .insertNode(fragment.lastChild);
                }
            } else {
                // 去除粘贴的html的标签
                if (filterItem[i].type.indexOf("text/html") !== -1) {
                    // selection
                    //     .getRangeAt(0)
                    //     .insertNode(document.createTextNode(paste)); //这个也可以不过会有选中效果
                    paste = paste
                        .replace(/</g, "&lt")
                        .replace(/>/g, "&gt");
                    paste = paste.replace(/\r\n/g, "<br>");
                    document.execCommand("insertHTML", false, paste);
                } else {
                    event.preventDefault();
                }
            }
        }
    }
},
```

