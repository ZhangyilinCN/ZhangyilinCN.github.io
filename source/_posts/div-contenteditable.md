---
title: "在可编辑div中进行粘贴功能"
date: 2022-11-18 18:12:13
tags:
  - "Javascript"
  - "Html"
categories:
  - "Javascript"
keywords:
description: "在可编辑 div 中粘贴-实现粘贴本地图片、qq微信等在线截图和粘贴去除标签的纯文字功能"
toc: false
---

```html
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

```javascript
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
    let isJieTu = null;
    const selection = window.getSelection();
    let paste = "";
    if (window.clipboardData && window.clipboardData.setData) {
        // IE
        paste = window.clipboardData.getData("text");
    } else {
        paste = (event.originalEvent || event).clipboardData.getData("text/plain") || "";
    }
    selection.deleteFromDocument();
    if (items && items.length) {
        let filterItem = items;
        // 检索剪切板items
        for (let i = 0; i < filterItem.length; i++) {
            if (filterItem[i].type.indexOf("image") !== -1) {
                /*  let file是个file文件，如果后端需要blob的话记得转换
                    let blob = new Blob([file], { type: 'image/png' || 'application/*' }); */
                file = filterItem[i].getAsFile();
                //  判断是不是截图还是本地文件，截图的话这个为null，本地的话是个对象
                isJieTu = filterItem[i].webkitGetAsEntry();
                if (!isJieTu) {
                    event.preventDefault();
                    const reader = new FileReader();
                    let that = this;
                    reader.onload = (function () {
                        return function (e) {
                            let fileFlag = that.blobUrlToFlieArr.some(
                                (ele) => {
                                    return ele.name == e.target.result;
                                }
                            ); //防止重复多次粘贴一个图片
                            if (!fileFlag) {
                                that.blobUrlToFlieArr = [
                                    ...that.blobUrlToFlieArr,
                                    { name: e.target.result, file },
                                ];
                            }
                            let imageDomStr = `<img  data-info='diaImWeb' src=${e.target.result} class='pasteImgs' />`;
                            let fragment = selection
                                .getRangeAt(0)
                                .createContextualFragment(imageDomStr);
                            selection
                                .getRangeAt(0)
                                .insertNode(fragment.lastChild);
                        };
                    })();
                    reader.readAsDataURL(file);
                } else {
                    /*  URL.createObjectURL(file) 这里是暂存的blob地址，并不是真正的地址，
                        要把file参数上传给后端，获取网络地址，再用于显示
                        URL.createObjectURL(file) 出来的blob地址，
                        在不用的时候（如发送后，页面离开时）记得URL.revokeObjectURL(item.name);
                        释放掉，避免相应的内存损耗 */
                    fileURL = URL.createObjectURL(file);
                    /*  this.blobUrlToFlieArr是用来储存粘贴的图片的，
                        因为不可能粘贴到输入框就上传到服务器，所以暂存起来，
                        等点击发送按钮的时候，用输入框的内容和this.blobUrlToFlieArr做筛选，
                        把还存在去输入框中的图片再做上传 */
                    this.blobUrlToFlieArr = [ ...this.blobUrlToFlieArr , { name: fileURL, file }];
                    let imgDomStr = `<img  data-info='diaImWeb' src=${fileURL} class='pasteImgs' />`
                    let fragment = selection.getRangeAt(0).createContextualFragment(imgDomStr);
                    selection.getRangeAt(0).insertNode(fragment.lastChild);
                }
            } else {
                //去除粘贴的文本的html样式-在编辑框中之显示相应纯文本
                if (filterItem[i].type.indexOf("text/html") !== -1) {
                    /* selection.getRangeAt(0).insertNode(document.createTextNode(paste));
                    这个也行只不过会有选中效果 */
                    paste = paste.replace(/</g, "&lt").replace(/>/g, "&gt");
                    paste = paste.replace(/\r\n/g, "<br>");
                    document.execCommand("insertHTML", false, paste);
                } else {
                    event.preventDefault();
                }
            }
        }
    }
}
```