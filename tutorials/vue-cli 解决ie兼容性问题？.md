# vue-cli 解决ie兼容性问题？

首先兼容ie只需要安装一个插件就好了`cnpm install babel-polyfill -S`)

* 使用方法，打开项目build文件夹下的`webpack.base.conf.js`文件，在里面配置如下。

```js
module.exports = {
	entry: {
		app: ['babel-polyfill', './src/main.js']
	}
}
```

然后在main.js中引入就好了。`import 'babel-polyfill'`

* 这样就解决兼容性问题了，但是这样并没有兼容axios的请求以及一些api，例如`Promise`解决上述问题就需要安装其他一些插件。

Step1，promise问题? axios不能直接兼容id

```sh
cnpm install es6-promise
```

使用方法:

```js
import promise from 'es6-promise';
promise.polyfill();
```

step2, URLSearchParams未定义的问题，原来是IE9不支持URLSearchParams。

解放方法：下载qs

```sh
cnpm install qs
```

然后在main.js中引入`import qs from 'qs';`