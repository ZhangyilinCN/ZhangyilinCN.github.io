---
title: vue的特殊修饰符
date: 2020-01-15 18:20:24
tags:
  - 'Vue'
categories:
  - 'Vue'
keywords:
description: 'vue的特殊修饰符'
toc: false
---

## 表单修饰符

### `.lazy'`

``` html
<input type="text" v-model.lazy="test" />
<span>{{ test }}</span>
```
**当在`input`修改`test`时，并不会立刻更新视图，使`span`更新，而是在`input`失焦的时候，才会更新，`span`中的内容才会更改**

---

### `.trim`
``` html
<input type="text" v-model.trim="test" />
```

**过滤`test`中的首位空格，也就是说在`input`中修改内容，一直按空格的话并不会更新`test`的值，也不会更新视图层。**
**但需要注意的是：`只过滤首尾空格，中间的空格是不会过滤的`**

---

### `.number`

``` html
<input type="text" v-model.number="test" />
```
**如果你`先输入数字`，那它就会限制你输入的`只能是数字`，输入其他的话不会更改`test`的值，并且在失焦的时候会`去除其他的非数字项`**
**如果你先输入字符串，那它就相当于没有加`.numbe`**

---
## 修饰符-简化的语法糖

### `.sync`

**当子组件修改父组件中的data的值时的语法糖写法**

- 常用方法
    - 父组件
    ``` html
    <div class="demo">
        <p>我是父组件中的demo:{{ demo }}</p>
        <aa :demo="demo" @changeDemo="changeDemo" />
    </div>
    ```
    ``` js
    import aa from './temp1'
    export default {
        data() {
            return {
            demo: '111'
            }
        },
        components: {
            aa
        },
        methods: {
            changeDemo(val) {
            this.demo = val
            }
        }
    }
    ```
    - 子组件
    ``` html
    <div class="div">
        <p>我是子组件</p>
        <p>我是父组件中的demo--{{ demo }}</p>
        <div class="btn" @click="changeFn">改变父组件的值</div>
    </div>
    ```
    ``` js
    export default {
        data() {
            return {}
        },
        props: ['demo'],
        methods: {
            changeFn() {
            this.$emit('changeDemo', '被修改了')
            }
        }
    }
    ```
---
- `.sync` 语法糖模式
    - 父组件
    ``` html
    <div class="demo">
        <p>我是父组件中的demo:{{ demo }}</p>
        <aa :demo.sync='demo' />
    </div>
    ```
    ``` js
    import aa from './temp1'
    export default {
        data() {
            return {
            demo: '111'
            }
        },
        components: {
            aa
        },
    }
    ```
    - 子组件
    ``` html
    <div class="div">
        <p>我是子组件</p>
        <p>我是父组件中的demo--{{ demo }}</p>
        <div class="btn" @click="changeFn">改变父组件的值</div>
    </div>
    ```
    ``` js
    export default {
        data() {
            return {}
        },
        props: ['demo'],
        methods: {
            changeFn() {
            this.$emit('update:demo', '被修改了')
            }
        }
    }
    ```

**`.sync`只能后边接值，不能接表达式，如`:title.sync='test+1'(这种是错误的)`**
**子组件中`this.$emit('update:props','参数')`的调用写法**

---











