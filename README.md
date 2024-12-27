# [demo](https://wait-fish.github.io/fish-crontab/dist/)

![](public/demo.png)

# 引用

基于 https://github.com/small-stone/vCrontab 的项目进行的二次开发，符合自己的项目需求

# FishCrontab

vue 的 cron 组件，支持解析/反解析 cron 表达式，生成最近五次的符合条件时间，依赖 vue2 和 element-ui

在原版基础上新增是否显示最近五次的符合条件时间
修改隐藏某个项的逻辑
修改了重置的逻辑

# 依赖
+ Vue 2.0.0+
+ element-ui 2.0.0+

## 安装方式

```
npm install fish-crontab
```

## 引入方式

```javascript
//前置配置
import Vue from 'vue'
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css'
Vue.use(ElementUI);

//全局引入
import FishCrontab from "fish-crontab";
Vue.use(FishCrontab); //使用方式：<vcrontab></vcrontab>

//单独引入
import FishCrontab from "fish-crontab";
export default {
  components: { FishCrontab },
};
```

## 代码示例

```javascript
<template>
    <div id="app">
        <div class="box">
            <el-input v-model="input" placeholder class="inp"></el-input>
            <el-button type="primary" @click="showDialog">生成 cron</el-button>
        </div>
        <el-dialog title="生成 cron" :visible.sync="showCron">
            <FishCrontab @hide="showCron=false" @fill="crontabFill" :expression="expression"></FishCrontab>
        </el-dialog>
    </div>
</template>

<script>
import FishCrontab from 'fish-crontab'
export default {
    components: { FishCrontab },
    data() {
        return {
            input: "",
            expression: "",
            showCron: false
        };
    },
    methods: {
        crontabFill(value) {
            //确定后回传的值
            this.input = value;
        },
        showDialog() {
            this.expression = this.input;//传入的 cron 表达式，可以反解析到 UI 上
            this.showCron = true;
        }
    }
};
</script>
```

## 参数

- expression
  传入的 cron 表达式，可以反解析到 UI 上

- hideComponent
  需要隐藏的组件数组，依次为`['second','min','hour','day','month','week','year']`

- fiveTimes
  是否显示最近五次执行时间 默认为`false`

## 方法

- fill
  点击确定时，把选择好的值返回。

- hide
  关闭组件时的回调
