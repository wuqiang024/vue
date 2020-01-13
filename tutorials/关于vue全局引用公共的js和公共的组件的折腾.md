# 关于vue全局引用公共的js和公共的组件的折腾

## step1，首先在components创建一个公共的目录,NoDatas目录里包含index.vue和index.js，index.vue用来写公共页面，index.js用来导出这个组件。

```js
<template>
<!-- NoDataWords 可以灵活控制每个页面显示的内容  -->
<!-- NoDataHeight 可以灵活控制每个页面的高度  -->
<!-- 如果你的页面都是统一的字体，统一的样式,那就直接在这写死就好了 -->
    <div class="NoDataAtAll W100"
         :style="{height: NoDataHeight }">{{NoDataWords}}</div>
</template>
<script>
export default {
  // 就是基本的父子组件传值
  props: ["NoDataHeight", "NoDataWords"],
  data() {
    return {};
  },
  methods: {}
};
</script>
<style lang="scss" scoped>
.NoDataAtAll {
  font-size: 14px;
  color: #909399;
}
</style>
```

## step2, 然后就是在index.js中注册该组件

```js
import NoDatas from './index.vue'
const noDataLists = {
	install: function(Vue) {
		Vue.component('noDataLists', noDatas)
	}
}
export default noDataLists
```

## step3, 在main.js中引入并使用该组件

```js
import noDataLists from '@/components/NoDatas/index'
Vue.use(noDataLists);
```

至此就可以了

# 再看看全局js是如何引用的

## step1，首先在components创建一个公共的js,然后直接在main.js中引入，需要注意的是引入之后不能直接使用，需要在Vue的原型链里注册，才可以使用

```js
export function FromDates(StringDate) {
	...
}
```

## step2, 然后在main.js中引入并注册

```js
import { FromDates } from './api/...'
Vue.prototype.$fromdate = FromDates;
// 在页面里就可以这样调用 this.$fromdate()
```