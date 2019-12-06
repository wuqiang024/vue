# 混入(mixins)的理解和使用
混入就是在一个公共的实例中写入公共的数据或者方法，这样的话vue会自动注入组件中。
全局混入会注入到每一个组件的实例中。
单页面引入的混入会注入到引用的组件中。
混入的对象也就是mixins中可以写入的内容包含任意组件选项。

## step1，首先说下单页面引入

* 在你的项目components新建一个mixins.js文件，里面内容如下

```js
const mixins = {
	data() {
		return {
			isNoData: false,
			isShowLoading: true
		}
	}
}

export default mixins;
```

* 在你要引入的页面中注册这个mixins

```js
import mixins from '@/components/mixins.js'
export default {
	mixins: [mixins]
}
```

## step2，全局注入混入
第一种方法：在你的项目的components新建一个mixins.js文件，里面内容如下

```js
const mixins = {
	data() {
		return {}
	}
}

export default mixins;
```

在main.js中全局注册该mixins,特别注意，注意，注意是Vue.mixin(mixins)；而不是Vue.use(mixins)。

```js
import mixins from '@/components/mixins.js'
Vue.mixin(mixins);
```

这样第一种方法，就全局注入到每一个spa实例中了。

第二种方法，也是官网介绍的

```js
Vue.mixin({
	data() {
		return {}
	}
})
```