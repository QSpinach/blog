---
tags: [Vue]
comments: true
toc: true
---



### 问题

#### 1、vue缓存页面使用

在路由文件中添加`meta` 

```js
{
    path: 'newslist',
    name: 'NewsList',
    meta: {keepAlive: true},
    component: () => import('@/pages/NewsList')
}
```

在router-view处添加

```vue
<keep-alive>
    <router-view v-if="$route.meta.keepAlive"></router-view>
</keep-alive>
<router-view v-if="!$route.meta.keepAlive"></router-view>
```

这样页面就只会加载一次然后缓存起来，再次访问不回刷新数据。

如果需要在另一个页面跳转过来刷新数据时，则需要使用`beforeRouteLeave` 关键是设置keepAlive

```vue
beforeRouteLeave(to, from, next) {
    // 设置下一个路由meta
    to.meta.keepAlive = false; // 让页面不缓存，重新请求数据
    console.log(to);
    next(); // 跳转页面
}
```

#### 2、页面刷新vuex被清空

同一页面，刷新后vuex被清空

- 试用localstorage存储

- 重新获取数据

  需要某些数据之前先判断一下数据是否存在，如果不存在重新获取。



#### 3、nextTick适当使用

> 延迟到下次dom更新循环之后执行延迟回调，在修改数据之后立即执行这个方法，获取最新的DOM。获取更新后的DOM言外之意就是什么操作需要用到了更新后的DOM而不能使用之前的DOM或者使用更新前的DOM或出问题，所以就衍生出了这个获取更新后的DOM的Vue方法。所以放在Vue.nextTick()回调函数中的执行的应该是会对DOM进行操作的 js代码.

- 你在Vue生命周期的created()钩子函数进行的DOM操作一定要放在Vue.nextTick()的回调函数中。

  原因：在执行created时并没有dom渲染，此时进行dom操作无效，将执行dom操作的js代码放入nextTick回调函数中，与其相对应的是mounted钩子函数。

- 在数据变化后要执行的某个操作，而这个操作需要使用随数据改变而改变的DOM结构的时候，这个操作都应该放进Vue.nextTick()的回调函数中。

  原因：vue是异步执行dom更新，一旦观察到数据变化，vue会开启一个队列，然后把在同一个事件循环 (event loop) 当中观察到数据变化的 watcher 推送进这个队列。如果这个watcher被触发多次，只会被推送到队列一次。这种缓冲行为可以有效的去掉重复数据造成的不必要的计算和DOm操作。而在下一个事件循环时，Vue会清空队列，并进行必要的DOM更新。

简而言之，等待DOM更新之后再进行操作。



#### 4、组件之间的调用方式

父子组件

- prop向下传递，事件向上传递
- 子组件添加ref属性，父组件可以获取到子组件的实例，不推荐使用
- 插槽slot 作用域插槽

非父子组件

- 使用状态管理

- 实例化一个公共vue实例

  必须要有公共的实例（可以是空的），才能使用 `$emit` 获取 `$on` 的数据参数，实现组件通信 



#### 5、计算属性设置值

> 计算属性是基于它们的依赖进行缓存的，一旦依赖发生变化，计算属性会重新计算

通过set方法触发它所依赖的变量，单纯的赋值，在取值的时候不会被改变



#### 6、vue文件中内联样式中有无scoped属性的差别

- 有scoped只在当前vue文件中可以使用这个样式
- 无scoped，会影响其他文件



#### 7、v-for v-key

为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一 key 属性。



#### 8、v-for v-if

当它们处于同一节点，v-for的优先级比v-if更高。



#### 9、组件、prop大小写不敏感，事件敏感

不同于组件和 prop，事件名不存在任何自动化的大小写转换。而是触发的事件名需要完全匹配监听这个事件所用的名称。

不同于组件和 prop，事件名不会被用作一个 JavaScript 变量名或属性名，所以就没有理由使用 camelCase 或 PascalCase 了。



#### 10、prop值的改变--不是立即

如果父组件中给子组件传递了一个prop的值，然后调用子组件的方法去获取该值，会发现值没有立即改变。

- 可以监听值的改变去调用相应子组件的方法
- 将子组件相关方法的调用放在nextTick里面



#### 11、对象中某属性值的监听

普通的`watch`中只能监听到某对象的变化才会调用，当想监听对象以及对象中属性的变化都调用函数时，可以使用`deep:true`

```javascript
data() {
　　return {
　　　　bet: {
　　　　　　pokerState: 53,
　　　　　　pokerHistory: 'local'
　　　　}   
    }
},
watch: {
　　bet: {
　　　　handler(newValue, oldValue) {
　　　　　　console.log(newValue)
　　　　},
　　　　deep: true
　　}
}
```



#### 12、this.$forceUpdate

强制刷新页面，触发页面重新渲染



#### 13、vue中的beforeRouteUpdate

在`xxx/detail/123`和`xxx/edit/123`都用了同一个组件，`beforeRouteUpdate`不生效，但是watch `$route`是生效的？

扩展： 可以考虑在路由定义处使用别名 alias

官方解释

```JavaScript
beforeRouteUpdate (to, from, next) {
    // 在当前路由改变，但是该组件被复用时调用
    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    // 可以访问组件实例 `this`
  },
```









