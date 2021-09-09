---
title: element滑块小功能
date: 2021-09-09 09:17:23
tags:
tags:
  - 'ElementUi'
  - 'Vue'
categories:
  - 'ElementUi'
keywords:
description: '使用多个滑块完成预警范围值的调节'
toc: false
---

![warringSliderexp.png](https://i.loli.net/2021/09/09/xSWPm49UqIK3dDy.png)

```html
<template>
  <div class="warring_slider_wrap">
    <div class="warring_slider_title">预警值</div>
    <div class="warring_slider_main">
      <div class="warring_slider_list_wrap">
        <div class="warring_slider_list">
          <div class="warring_slider_item warring_slider_item1" ref="sliderWid">
            <div
              class="tooltip"
              ref="tooltip1"
              :style="yujingTooltipLeftFn(warringValue1, 0, warringValue2 - 1)"
            >
              {{ warringValue1 }}
            </div>
            <el-slider
              v-model="warringValue1"
              :max="warringValue2 - 1"
              :show-tooltip="false"
            ></el-slider>
          </div>
          <div class="warring_slider_item warring_slider_item2">
            <div
              class="tooltip"
              ref="tooltip2"
              :style="
                yujingTooltipLeftFn(
                  warringValue2,
                  warringValue1 + 1,
                  warringValue3 - 1
                )
              "
            >
              {{ warringValue2 }}
            </div>
            <el-slider
              v-model="warringValue2"
              :min="warringValue1 + 1"
              :max="warringValue3 - 1"
              :show-tooltip="false"
            ></el-slider>
          </div>
          <div class="warring_slider_item warring_slider_item3">
            <div
              class="tooltip"
              ref="tooltip3"
              :style="
                yujingTooltipLeftFn(
                  warringValue3,
                  warringValue2 + 1,
                  warringValue4 - 1
                )
              "
            >
              {{ warringValue3 }}
            </div>
            <el-slider
              v-model="warringValue3"
              :min="warringValue2 + 1"
              :max="warringValue4 - 1"
              :show-tooltip="false"
            ></el-slider>
          </div>
          <div class="warring_slider_item4">
            <div class="tooltip" ref="tooltip4">{{ warringValue4 }}</div>
            <div class="slider_cir"></div>
          </div>
        </div>
        <div class="warring_bottom_list">
          <div
            class="warring_bottom_item"
            :style="{ width: warringBtmItem1 + 'px' }"
          >
            一般
          </div>
          <div
            class="warring_bottom_item"
            :style="{ width: warringBtmItem2 + 'px' }"
          >
            异常
          </div>
          <div
            class="warring_bottom_item"
            :style="{ width: warringBtmItem3 + 'px' }"
          >
            突发
          </div>
          <div
            class="warring_bottom_item"
            :style="{ width: warringBtmItem4 + 'px' }"
          >
            危险
          </div>
          <div class="warring_bottom_item_other">严重</div>
        </div>
      </div>
      <div class="warring_slider_input">
        <span>严重</span>
        <el-input-number
          v-model="warringValue4"
          label="严重预警值"
          :min="warringValue3 + 1"
          :max="1000"
        ></el-input-number>
      </div>
    </div>
  </div>
</template>
```

```js
<script>
export default {
  data() {
    return {
      warringValue1: 25,
      warringValue2: 60,
      warringValue3: 80,
      warringValue4: 100,
      warringBtmItem1: 0,
      warringBtmItem2: 0,
      warringBtmItem3: 0,
      warringBtmItem4: 0,
    };
  },
  methods: {
    // 预警值的tooltip-left判断
    yujingTooltipLeftFn(current, min, max) {
      let num = max - min;
      let leftNum = ((current - min) / num) * 100 + "%";
      this.yujingBtmtextFn();
      return { left: leftNum };
    },
    // 预警底部提示文字的位置
    yujingBtmtextFn() {
      this.$nextTick(() => {
        let sliderWid = this.$refs.sliderWid.clientWidth;
        let tooltip1 = this.$refs.tooltip1.offsetLeft;
        this.warringBtmItem1 = tooltip1;
        let tooltip2 = this.$refs.tooltip2.offsetLeft;
        this.warringBtmItem2 = sliderWid - this.warringBtmItem1 + tooltip2;
        let tooltip3 = this.$refs.tooltip3.offsetLeft;
        this.warringBtmItem3 =
          sliderWid -
          this.warringBtmItem1 +
          (sliderWid - this.warringBtmItem2) +
          tooltip3;
        let tooltip4 = this.$refs.tooltip4.offsetLeft;
        this.warringBtmItem4 =
          sliderWid -
          this.warringBtmItem1 +
          (sliderWid - this.warringBtmItem2) +
          (sliderWid - this.warringBtmItem3) +
          tooltip4;
      });
    },
  },
};
</script>
```

```css
<style scoped lang="scss">
  .warring_slider_wrap {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 14px 0;
    .warring_slider_title {
      font-size: 16px;
      margin-bottom: 30px;
    }
    .warring_slider_main {
      display: flex;
      .warring_slider_list_wrap {
        flex: 0 0 auto;
        display: flex;
        flex-direction: column;
        .warring_slider_list {
          box-sizing: border-box;
          padding: 0 10px;
          display: flex;
          .warring_slider_item {
            flex: 0 0 150px;
            width: 150px;
            padding-top: 30px;
            position: relative;
            .tooltip {
              position: absolute;
              padding: 0 4px;
              color: #fff;
              white-space: nowrap;
              min-width: 30px;
              text-align: center;
              border-radius: 4px;
              transform: translateX(-50%);
              top: 0;
              font-size: 12px;
              &::after {
                width: 0;
                content: "";
                height: 0;
                position: absolute;
                bottom: -12px;
                left: 50%;
                transform: translateX(-50%);
                border-width: 6px;
                border-style: solid;
                border-top-color: #000;
                border-bottom-color: transparent;
                border-left-color: transparent;
                border-right-color: transparent;
              }
            }
            &.warring_slider_item1 {
              ::v-deep .el-slider {
                .el-slider__runway {
                  border-radius: 6px 0 0 6px;
                  .el-slider__button-wrapper {
                    .el-slider__button {
                      border-color: #28d760;
                    }
                  }
                }
              }
              .tooltip {
                background-color: #28d760;
                &::after {
                  border-top-color: #28d760;
                }
              }
            }
            &.warring_slider_item2 {
              ::v-deep .el-slider {
                .el-slider__runway {
                  .el-slider__button-wrapper {
                    .el-slider__button {
                      border-color: #eb9b01;
                    }
                  }
                }
              }
              .tooltip {
                background-color: #eb9b01;
                &::after {
                  border-top-color: #eb9b01;
                }
              }
            }
            &.warring_slider_item3 {
              ::v-deep .el-slider {
                .el-slider__runway {
                  .el-slider__button-wrapper {
                    .el-slider__button {
                      border-color: #f55923;
                    }
                  }
                }
              }
              .tooltip {
                background-color: #f55923;
                &::after {
                  border-top-color: #f55923;
                }
              }
            }
            ::v-deep .el-slider {
              .el-slider__runway {
                height: 12px;
                margin: 10px 0;
                border-radius: 0;
                .el-slider__bar {
                  height: 12px;
                  background-color: transparent;
                }
                .el-slider__button-wrapper {
                  top: -12px;
                }
              }
            }
          }
          .warring_slider_item4 {
            flex: 0 0 auto;
            padding-top: 30px;
            position: relative;
            .tooltip {
              position: absolute;
              padding: 0 4px;
              color: #fff;
              background-color: #900c0c;
              white-space: nowrap;
              min-width: 30px;
              text-align: center;
              border-radius: 4px;
              left: 50%;
              transform: translateX(-50%);
              top: 0;
              font-size: 12px;
              &::after {
                width: 0;
                content: "";
                height: 0;
                position: absolute;
                bottom: -12px;
                left: 50%;
                transform: translateX(-50%);
                border-width: 6px;
                border-style: solid;
                border-top-color: #900c0c;
                border-bottom-color: transparent;
                border-left-color: transparent;
                border-right-color: transparent;
              }
            }
            .slider_cir {
              height: 12px;
              background-color: #e4e7ed;
              width: 16px;
              margin-top: 10px;
              border-radius: 0 6px 6px 0;
              position: relative;
              &::after {
                position: absolute;
                content: "";
                width: 16px;
                height: 16px;
                box-sizing: border-box;
                border: 2px solid #900c0c;
                background-color: #fff;
                border-radius: 50%;
                top: -2px;
                left: 0;
              }
            }
          }
        }
        .warring_bottom_list {
          width: 100%;
          height: 18px;
          font-size: 12px;
          box-sizing: border-box;
          padding: 0 10px;
          color: #999;
          position: relative;
          display: flex;
          align-items: center;
          .warring_bottom_item {
            text-align: center;
          }
          .warring_bottom_item_other {
            position: absolute;
            width: 30px;
            right: 0;
          }
        }
      }
      .warring_slider_input {
        flex: 0 0 auto;
        margin-left: 14px;
        display: flex;
        padding-bottom: 22px;
        align-items: flex-end;
        & > span {
          margin-right: 6px;
          line-height: 26px;
        }
        ::v-deep .el-input-number {
          width: 100px;
          line-height: 25px;
          .el-input-number__decrease,
          .el-input-number__increase {
            width: 25px;
          }
          .el-input {
            .el-input__inner {
              padding: 0 25px;
              height: 27px;
              line-height: 27px;
            }
          }
        }
      }
    }
  }
</style>
```
