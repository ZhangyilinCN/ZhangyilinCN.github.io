---
title: 中断axios请求的接口
date: 2022-03-19 15:24:00
tags:
  - "Vue"
categories:
  - "Vue"
keywords:
description: "在vue项目中，中断axios的接口请求"
toc: false
---

### 使用场景：一个 list，点击其中的 item 调去接口，在右侧展示接口内容。如果用户快速点击多个 item，则会请求多个接口，所以可以只用中断接口的方式，优化性能，使其在快速点击多个 item 的时候之后执行最后一个，中断上一个。

_`cancelToken` 在 `get` 请求时候是在第二个参数内写，`post` 为第三个参数内写_

```javascript
import axios from "axios";
export default {
  data() {
    return {
      xhrCancel: null, //用于存放执行的那个接口取消。类似于定时器的timer作用
    };
  },
  methoods: {
    //   get请求
    fn1() {
      if (this.xhrCancel) {
        //每次请求该接口前，先判断有没有改接口正在被执行，如果有就先中断上一个接口的请求
        this.xhrCancel();
        this.xhrCancel = null;
      }
      let CancelToken = axios.CancelToken;
      let params = {
        id: xxx,
        token: xxxx,
      };
      axios
        .get("http://xxxxx.com", {
          params,
          cancelToken: new CancelToken((c) => {
            this.xhrCancel = c;
          }),
        })
        .then(
          (res) => {
            //dosomething....
          },
          (err) => {
            //dosomething...
            //   中断后会走reject（）所以会走err中的代码
          }
        );
    },
    // post请求
    fn2() {
      if (this.xhrCancel) {
        //每次请求该接口前，先判断有没有改接口正在被执行，如果有就先中断上一个接口的请求
        this.xhrCancel();
        this.xhrCancel = null;
      }
      let CancelToken = axios.CancelToken;
      let params = {
        id: xxx,
        token: xxxx,
      };
      axios
        .post("http://xxxxx.com", params, {
          cancelToken: new CancelToken((c) => {
            this.xhrCancel = c;
          }),
        })
        .then(
          (res) => {
            //dosomething....
          },
          (err) => {
            //dosomething...
            //   中断后会走reject（）所以会走err中的代码
          }
        );
    },
  },
};
```
