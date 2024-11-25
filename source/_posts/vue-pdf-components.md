---
title: vue-pdf组件
date: 2024-11-25 15:52:47
tags:
  - "Vue-cli"
  - "插件"
categories:
  - "插件"
keywords:
description: "基于vue-pdf封装的带有缩略图目录、放大、分页功能的组件"
toc: false
---

## 基于vue-pdf@4.3.0 ， 自带缩略图目录，放大缩小，分页跳页功能，浏览 pdf 的组件

### 直接引用使用

```html
<!-- 引用使用，pdfURL为file文件，url地址 都可以  -->
<common-pdf :pdfURL="xxxx" />
```

****
****

```html
<div class="pdf_wrap">
  <div class="pdf_top_btns">
    <div class="mulu_item" @click="onPushMuluFlagFn">
      <div
        class="icon"
        :class="muluShowFlag ? 'el-icon-s-fold' : 'el-icon-s-unfold'"
      ></div>
    </div>
    <div class="fangda_wrap">
      <div @click="scaleD" class="fangdajin_item">
        <i class="el-icon-zoom-in"></i>
      </div>
      <div @click="scaleX" class="fangdajin_item">
        <i class="el-icon-zoom-out"></i>
      </div>
    </div>
    <div class="fenye_wrap">
      <div
        @click="changePdfPage(0)"
        class="turn"
        :class="{ grey: currentPage === 1 }"
      >
        <i class="el-icon-caret-left"></i>
      </div>
      <div class="ml10_text">
        <div>第</div>
        <el-input
          v-model="pageNumber"
          class="page-number"
          @input="pageChange"
        ></el-input>
        <div>页</div>
      </div>
      <div
        @click="changePdfPage(1)"
        class="turn"
        :class="{ grey: currentPage === pageCount }"
      >
        <i class="el-icon-caret-right"></i>
      </div>
      <div class="ml10_yema">{{ currentPage }} / {{ pageCount }}</div>
    </div>
  </div>
  <div class="pdf_mulu_wrap" :class="!muluShowFlag && 'hide_class'">
    <div class="mulu_list" v-loading="muluLoading">
      <div
        class="mulu_item"
        v-for="item in numPages"
        :key="item"
        @click="onChangePdfPageFn(item)"
      >
        <pdf :src="imgUrl" :page="item" />
      </div>
    </div>
    <div class="mulu_icon" @click="onPushMuluFlagFn">
      <div class="icon el-icon-d-arrow-left"></div>
    </div>
  </div>
  <div class="pdf_content_main">
    <pdf
      :page="currentPage"
      @num-pages="pageCount = $event"
      @page-loaded="currentPage = $event"
      @loaded="loadPdfHandler"
      ref="pdfWrapper"
      :src="pdfURL"
    ></pdf>
  </div>
</div>
```

```javascript
import pdf from "vue-pdf";
import CMapReaderFactory from "vue-pdf/src/CMapReaderFactory.js";
export default {
  components: {
    pdf,
  },
  props: {
    pdfURL: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      muluShowFlag: false,
      thumbnails: null,
      currentPage: 0,
      pageCount: 0,
      pageNumber: 1,
      scale: 1, //放大系数
      imgUrl: null,
      numPages: null,
      muluLoading: false,
    };
  },
  mounted() {
    this.$nextTick(() => {
      this.getNumPages(this.pdfURL);
    });
  },
  methods: {
    onChangePdfPageFn(itemPage) {
      this.currentPage = itemPage;
      this.pageNumber = itemPage;
    },
    getNumPages(url) {
      this.muluLoading = true;
      this.imgUrl = pdf.createLoadingTask({ url, CMapReaderFactory });
      this.imgUrl.promise
        .then((pdf) => {
          this.numPages = pdf.numPages;
          this.muluLoading = false;
        })
        .catch((err) => {
          console.error("pdf加载失败");
        });
    },
    onPushMuluFlagFn() {
      let flag = this.muluShowFlag;
      this.muluShowFlag = !flag;
    },
    // 初始化pdf
    loadPdfHandler() {
      this.currentPage = 1;
      this.pageNumber = 1;
    },
    //放大
    scaleD() {
      this.scale += 0.1;
      this.$refs.pdfWrapper.$el.style.transform = "scale(" + this.scale + ")";
      this.$refs.pdfWrapper.$el.style.transformOrigin = "top center";
    },
    //缩小
    scaleX() {
      if (this.scale === 1) {
        return;
      }
      this.scale += -0.1;
      this.$refs.pdfWrapper.$el.style.transform = "scale(" + this.scale + ")";
    },
    // 分页上、下一页事件
    changePdfPage(val) {
      if (val === 0 && this.currentPage > 1) {
        this.currentPage--;
        this.pageNumber = this.currentPage;
      }
      if (val === 1 && this.currentPage < this.pageCount) {
        this.currentPage++;
        this.pageNumber = this.currentPage;
      }
    },
    //跳转页面
    pageChange() {
      if (
        Number(this.pageNumber) > 0 &&
        Number(this.pageNumber) <= this.pageCount
      ) {
        this.currentPage = Number(this.pageNumber);
      } else {
        this.currentPage = 1;
        this.pageNumber = 1;
      }
    },
  },
};
```

```scss
.pdf_wrap {
  width: 100%;
  display: flex;
  flex-direction: column;
  position: relative;
  overflow: hidden;
  .pdf_top_btns {
    height: 80px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-bottom: 1px solid #ccc;
    .mulu_item {
      margin-right: 16px;
      .icon {
        font-size: 30px;
        font-weight: bold;
        color: #333;
        cursor: pointer;
        &:hover {
          color: #0068b6;
        }
      }
    }
    .fangda_wrap {
      display: flex;
      align-items: center;
      .fangdajin_item {
        border-radius: 6px;
        background-color: #eee;
        padding: 4px 20px;
        cursor: pointer;
        margin-right: 12px;
        i {
          font-size: 22px;
          font-weight: bold;
          color: #333;
          cursor: pointer;
        }
        &:hover {
          background-color: #0068b6;
          i {
            color: #fff;
          }
        }
      }
    }
    .fenye_wrap {
      display: flex;
      align-items: center;
      .turn {
        margin: 0 10px;
        i {
          font-size: 30px;
          font-weight: 700;
          color: #333;
          cursor: pointer;
        }
      }
      .ml10_text {
        display: flex;
        align-items: center;
        .page-number {
          width: 60px;
          margin: 0 10px;
          /deep/.el-input__inner {
            width: 100%;
            height: 34px;
            line-height: 34px;
            font-size: 20px;
            background: #eee;
            color: #333;
            padding: 0;
            text-align: center;
          }
        }
      }
      .ml10_yema {
        margin-left: 20px;
      }
    }
  }
  .pdf_mulu_wrap {
    position: absolute;
    width: 35%;
    height: 100%;
    top: 0;
    bottom: 0;
    left: 0;
    transition: all 0.4s linear;
    z-index: 2;
    &.hide_class {
      left: -40%;
    }
    .mulu_list {
      box-sizing: border-box;
      padding: 20px;
      width: 100%;
      height: 100%;
      overflow-y: auto;
      background-color: #ccc;
      .mulu_item {
        margin-bottom: 20px;
        &:last-child {
          margin-bottom: 0;
        }
      }
    }
    .mulu_icon {
      position: absolute;
      width: 24px;
      height: 100px;
      background-color: #aaa;
      top: 50%;
      border-radius: 0 12px 12px 0;
      transform: translateY(-50%);
      right: -20px;
      display: flex;
      align-items: center;
      cursor: pointer;
      justify-content: center;
      &:hover {
        opacity: 0.9;
      }
      .icon {
        font-size: 24px;
        font-weight: 700;
        color: #fff;
      }
    }
  }
  ::v-deep .pdf_content_main {
    width: 100%;
    height: auto;
    // & > span {
    //   width: 100% !important;
    //   height: 100% !important;
    //   display: flex !important;
    //   align-items: center;
    //   justify-content: center;
    //   canvas {
    //     width: inherit !important;
    //     height: 100% !important;
    //   }
    // }
  }
}
```
