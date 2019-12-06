# <router-link>属性以及方法？

* `:to`相当于a标签中的'href'属性，后面跟跳转链接所用，会渲染成a标签--

```sh
<router-link :to="/home">Home</router-link>
<!-- 渲染结果 -->
<a href="/home">Home</a>
```

* `replace`属性，加上该属性页面切换不会留下历史记录。

```sh
<router-link :to="/Home" replace>Home</router-link>
```

* tag属性，具有tag属性的router-link会被渲染成相应的标签

```sh
<router-link :to="/Home" tag="li">Home</router-link>
<li>Home</li>
```

* `active-class`属性，设置链接激活时候的class属性：默认为router-link-active，所以如果没有设置，会被渲染为这个class，我们可以在router.js里配置这个属性。

```js
const router = new VueRouter({
	mode: 'hash',
	linkActiveClass: 'u-link--Active', // 这是链接激活时候的class
})
<router-link :to="/Home" active-class="u-link--Active">Home</router-link>
```

* `exact`属性，严格模式

```sh
// 这个链接只会在地址为 / 的时候被激活
<router-link to="/" exact>Home</router-link>
<router-link to="/user">User</router-link>
<router-link to="/user/userinfo">UserInfor</router-link>
// 如果不设置exact，则当路由到了/user/userinfo页面时，User也是被设置了router-link-active样式的
```

> router-link默认触发router.push(location)，如果设置的replace，则触发router.replace(location),这两者有什么区别？
router.push()导航跑到不同的URL，这个方法会向history栈添加一个新的记录，所以当用户点浏览器的后退按钮时，则回到之前的url。
router.replace()与router.push()作用一样，但是他不会往history添加记录，而是跟他的方法名一样替换掉当前的history记录。
router.go(n)，这个方法的参数是一个整数，意思是在history记录中前进或后退多少步。类似window.history.go(n)