# timrchen

> vue item

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

## 生命周期图示
![关注TimRChen](https://raw.githubusercontent.com/TimRChen/photoRepo/master/Vue-Study/lifecycle.png)


## 模板语法

*   你的站点上动态渲染的任意 HTML 可能会非常危险，因为它很容易导致 XSS 攻击。请只对可信内容使用 HTML 插值，**绝不要**对用户提供的内容插值。

*   Vue 2.x 中，过滤器只能在 mustache 绑定和 `v-bind` 表达式（从 2.1.0 开始支持）中使用，因为过滤器设计目的就是用于文本转换。为了在其他指令中实现更复杂的数据变换，你应该使用计算属性。

## 计算属性

#### 模板内的表达式是非常便利的，但是它们实际上只用于简单的运算。在模板中放入太多的逻辑会让模板过重且难以维护。例如：
```js
<div id="example">
  {{ message.split('').reverse().join('') }}
</div>
```
#### 在这种情况下，模板不再简单和清晰。在意识到这是反向显示 message 之前，你不得不再次确认第二遍。当你想要在模板中多次反向显示 message 的时候，问题会变得更糟糕。
#### 这就是对于任何复杂逻辑，你都应当使用**计算属性**的原因。