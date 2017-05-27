# Vue-Todolist
*  this is a Todolist. by @TimRChen

![关注TimRChen](https://raw.githubusercontent.com/TimRChen/photoRepo/master/Vue-Todlist/2017_01.gif)

## Demand
*   可以在最上面的input里，使用回车来添加任务
*   在中间的任务列表里，由checkbox来控制任务的状态
*   已完成的任务有一个line-through的样式
*   当鼠标移到每一个任务时，都会出现删除按钮提供删除
*   在底部有一个全选按钮，用于控制所有的任务状态
*   还有已完成与总数的显示
*   可以清空已完成的任务

## Dev Log

### 0.0.2 v
*   完成需求所有功能

### 0.0.1 v
*   更新vue-todo样式
*   增加动态添加todo功能


## format
*   Eslint控制空格缩进为2个空格

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev || npm start

# build for production with minification
npm run build
```

## 模板语法

*   你的站点上动态渲染的任意 HTML 可能会非常危险，因为它很容易导致 XSS 攻击。请只对可信内容使用 HTML 插值，**绝不要**对用户提供的内容插值。

*   Vue 2.x 中，过滤器只能在 mustache 绑定和 `v-bind` 表达式（从 2.1.0 开始支持）中使用，因为过滤器设计目的就是用于文本转换。为了在其他指令中实现更复杂的数据变换，你应该使用计算属性。

## 计算属性

### 计算属性

#### 模板内的表达式是非常便利的，但是它们实际上只用于简单的运算。在模板中放入太多的逻辑会让模板过重且难以维护。例如：
```js
<div id="example">
  {{ message.split('').reverse().join('') }}
</div>
```
#### 在这种情况下，模板不再简单和清晰。在意识到这是反向显示 message 之前，你不得不再次确认第二遍。当你想要在模板中多次反向显示 message 的时候，问题会变得更糟糕。
#### 这就是对于任何复杂逻辑，你都应当使用**计算属性**的原因。

#### **计算缓存** vs **Methods**
*   我们可以将同一函数定义为一个 method 而不是一个计算属性。对于最终的结果，两种方式确实是相同的。然而，不同的是**计算属性是基于它们的依赖进行缓存的**。计算属性只有在它的相关依赖发生改变时才会重新求值。这就意味着只要 `message` 还没有发生改变，多次访问 `reversedMessage` 计算属性会立即返回之前的计算结果，而不必再次执行函数。


*   我们为什么需要缓存？假设我们有一个性能开销比较大的的计算属性 A ，它需要遍历一个极大的数组和做大量的计算。然后我们可能有其他的计算属性依赖于 A 。如果没有缓存，我们将不可避免的多次执行 A 的 getter！如果你不希望有缓存，请用 method 替代。

#### **Computed属性** vs **Watched属性**

*   Vue 确实提供了一种更通用的方式来观察和响应 Vue 实例上的数据变动：watch 属性。当你有一些数据需要随着其它数据变动而变动时，你很容易滥用 watch——特别是如果你之前使用过 AngularJS。然而，**通常更好的想法是使用 computed 属性而不是命令式的 watch 回调**。细想一下这个例子：
```html
<div id="demo">{{ fullName }}</div>
```
```js
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar',
    fullName: 'Foo Bar'
  },
  watch: {
    firstName: function (val) {
      this.fullName = val + ' ' + this.lastName
    },
    lastName: function (val) {
      this.fullName = this.firstName + ' ' + val
    }
  }
})
```
上面代码是命令式的和重复的。将它与 computed 属性的版本进行比较：
```js
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName: function () {
      return this.firstName + ' ' + this.lastName
    }
  }
})
```
好得多了，不是吗？

#### **计算setter**
计算属性默认只有 getter ，不过在需要时你也可以提供一个 setter ：
```js
// ...
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
// ...
```
现在在运行 vm.fullName = 'John Doe' 时， setter 会被调用， vm.firstName 和 vm.lastName也相应地会被更新。

### 观察 Watchers
#### 虽然计算属性在大多数情况下更合适，但有时也需要一个自定义的 watcher 。这是为什么 Vue 提供一个更通用的方法通过 watch 选项，来响应数据的变化。当你想要在数据变化响应时，**执行异步操作或开销较大的操作**，这是很有用的。

使用 watch 选项允许我们**执行异步操作（访问一个 API）**，限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。这是计算属性无法做到的。


## 生命周期图示
![关注TimRChen](https://raw.githubusercontent.com/TimRChen/photoRepo/master/Vue-Study/lifecycle.png)