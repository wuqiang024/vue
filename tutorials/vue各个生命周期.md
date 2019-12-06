# vue各个生命周期
生命周期|阶段|描述
beforeCreated|创建前|vue实例的挂载元素$el和数据对象data都为undefined，还未初始化
created|创建后|vue实例的数据对象data有了，$el还没有
beforeMount|模板载入前|vue实例的$el和data都初始化了，但还是挂载之前为虚拟的dom节点，data.message还未替换
mounted|模板载入后|vue实例挂载完成,data.message成功渲染
beforeUpdate|组件更新前|组件更新前调用
updated|组件更新后|组件更新后调用
beforeDestory|组件销毁前|调用$destory方法后，立即执行beforeDestory
destoryed|组件销毁后|组件销毁后调用，此时只剩下dom空壳