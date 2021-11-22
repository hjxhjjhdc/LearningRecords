## vue.nextTick和Vue.forceUpdate

### vue.nextTick

1、 在Vue生命周期的created()钩子函数进行的DOM操作一定要放在Vue.nextTick()的回调函数中。因为在created()钩子函数执行的时候DOM 其实并未进行任何渲染，而此时进行DOM操作无异于徒劳，所以此处一定要将DOM操作的js代码放进Vue.nextTick()的回调函数中。

2、在数据变化后要执行的某个操作，而这个操作需要使用随数据改变而改变的DOM结构的时候，这个操作都应该放进Vue.nextTick()的回调函数中。

### vue.forceUpdate

1、因为数据层次太多，render函数没有自动更新，需手动强制刷新。

2、当在data里没有显示的声明一个对象的属性，而是之后给该对象添加属性，这种情况vue是检测不到数据变化的，可以使用$forceUpdate()

