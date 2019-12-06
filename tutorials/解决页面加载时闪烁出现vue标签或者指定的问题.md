# 解决页面加载时闪烁出现vue标签或者指定的问题
## 前沿
在项目开发中，经常会遇到当数据加载时vue的一些标签出现闪烁，然后等数据加载完后消失，这时候就要用到官网中提到的v-cloak来解决。

首先说一下经常遇到的情况。

step1: 加载时遇到{{ value.name }}闪烁，是因为你在渲染时候这么写的`<p>{{ value.name }}</p>`
step2: 加载时遇到一个空的盒子里面什么都没有，这是因为你在渲染时候这么写的`<p v-html='value.name'></p>`

## 解决办法
那么，v-cloak要放在什么位置呢，是不是每个需要渲染数据的标签都要添加这个指令，经过试验发现，v-cloak并不需要添加到每个标签，只要在el挂载的标签上添加就可以，这是最简单有效的方法。

```sh
<div class="#app" v-cloak>
	<p>{{ value.name }}</p>
</div>
```

然后在css里添加

```sh
[v-cloak] {
	display: none;
}
```

这样就可以防止页面闪烁了。
但是有时候可能不会起作用，可能原因有二:

一，v-cloak的display属性被层级更高的给覆盖了，所以要提高层级。

```sh
[v-cloak] {
	display: none !important
}
```

二，样式放在了@import引入的css中，v-cloak的这个样式放在@import引入的css文件中不起作用，可以放在link引入的css文件里或者内联样式中。

## 其他解决方案
如果用cloak无法解决，可以尝试下在el元素上加上如下代码

```sh
style="display: none;" :style="{display: 'block'}"
```

此时当vue还为完全加载完时不会显示，等到加载完时`:style`会起作用。