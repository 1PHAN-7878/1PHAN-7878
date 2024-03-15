---
title: 学习记录之vue
date: 2024-03-11 21:12:52
tags: 前端
---

# 入门

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.bootcdn.net/ajax/libs/vue/2.7.0/vue.js"></script>
    <title>Document</title>
</head>
<body>
    <div id="container">
        
        <h1>{{message}}</h1>
    </div>
    
    <script>
        new Vue({
            el: "#container",
            data: {
                message: "aaa"
            }
        });
    </script>
</body>
</html>
```

一个 `<h1>` 标题元素，其中的文本内容通过 Vue 实例的 `message` 属性动态绑定。

- `el: "#container"`：指定 Vue 实例的挂载点，即将 Vue 实例绑定到具有 `id` 为 `container` 的 `<div>` 元素上。
- `data: { message: "aaa" }`：定义了 Vue 实例的数据对象，其中包含一个名为 `message` 的属性，其初始值为 `"aaa"`。
- 当 Vue 实例挂载到页面后，`{{message}}` 中的 `message` 将会被替换为数据对象中 `message` 属性的值，即显示为 `"aaa"`。

## 数据绑定

1. **插值表达式（Interpolation）：**

   - 插值表达式是 Vue.js 中最基本的数据绑定方式，它使用双大括号 `{{ }}` 将表达式包裹在 HTML 标签中。例如，`{{ message }}` 将会被替换为 Vue 实例中 `message` 属性的值。

   - 插值表达式可以直接放置在 HTML 元素的文本内容、属性值、以及某些标签的特定属性内。

   - 例如：

     ```html
     Copy code<div>
       <p>{{ message }}</p>
       <input type="text" v-model="message">
     </div>
     ```

   - 在这个例子中，`{{ message }}` 将会被替换为 Vue 实例中 `message` 属性的值，并显示在 `<p>` 元素中。同时，`<input>` 元素的 `value` 属性将会与 `message` 属性保持同步。

2. **指令（Directives）：**

   - 指令是以 `v-` 开头的特殊属性，它们提供了对 DOM 元素进行动态绑定的能力。指令的主要目的是响应式地将 Vue 实例中的数据绑定到 DOM 元素上。

   - Vue.js 提供了一系列内置指令，如 `v-bind`、`v-on`、`v-model` 等。

   - `v-bind` 指令用于动态地绑定 HTML 属性，`v-on` 指令用于绑定事件处理器，`v-model` 指令用于实现双向数据绑定等。

   - 例如：

     ```html
     htmlCopy code<div>
       <p v-bind:title="message">Hover me</p>
       <button v-on:click="changeMessage">Change Message</button>
       <input type="text" v-model="message">
     </div>
     ```

   - 在这个例子中，`v-bind:title="message"` 将会动态地将 `<p>` 元素的 `title` 属性绑定到 Vue 实例中 `message` 属性的值上。`v-on:click="changeMessage"` 将会在按钮被点击时调用 Vue 实例中的 `changeMessage` 方法。`v-model="message"` 则实现了输入框的双向数据绑定，保持输入框中的值与 Vue 实例中 `message` 属性的值同步。

例子：

```html
<input type="text" v-model:value="name">
<input type="text" v-bind:value="name2">
```

相当于会从data中获取数据，v-model会保持同步。

# 事件处理

## 基本使用

+ v-on:xxx或者 @xxx绑定事件。

+ 事件回调在methods对象中，最终显示在vm上。
+ methods配置的函数不要用箭头函数。
+ 例如`@click="func"`与`@click="func($event)"`相同，但是后者可以传参

```vue
<button @click="showInfo2($event, 1)">show一下</button>
<script>
        new Vue({
            el: "#container",
            data: {
                message: "aaa",
                name: "123",
                name2: "456"
            },
            methods: {
                showInfo1(event){
                    console.log(event);
                    alert("this is info1");
                },
                showInfo2(event, num){
                    console.log(event);
                    console.log(num);
                    alert("this is info1");
                }
            }
            
        });
    </script>
```

# 属性

## 计算属性

在Vue组件中定义计算属性。你可以在`computed`对象中定义一个或多个计算属性，每个属性的键是属性的名称，值是一个函数，用于计算属性的值。

```JavaScript
Vue.component('example-component', {
  data() {
    return {
      // 数据
      message: 'Hello',
      // 其他数据...
    }
  },
  computed: {
    // 计算属性
    reversedMessage() {
      // 这里计算并返回基于message的反转字符串
      return this.message.split('').reverse().join('');
    }
  }
});
```

在模板中使用计算属性。你可以像使用普通的数据属性一样在模板中使用计算属性。

```html
<template>
  <div>
    <p>原始消息: {{ message }}</p>
    <p>反转消息: {{ reversedMessage }}</p>
  </div>
</template>
```

## 监视属性

在Vue.js中，你可以使用`watch`选项来监视Vue实例中的数据变化，并在数据发生变化时执行相应的操作。`watch`选项可以监听数据的变化，并在数据发生变化时执行自定义的回调函数。

```javascript
watch: {
    // 监视message属性的变化
    message(newValue, oldValue) {
      // 在message属性发生变化时执行的操作
      console.log('message属性发生了变化:', oldValue, '->', newValue);
    }
  }
```

在上面的示例中，我们定义了一个`watch`选项，其中包含一个名为`message`的属性。当`message`属性的值发生变化时，Vue将自动调用指定的回调函数，并传入两个参数：新值(`newValue`)和旧值(`oldValue`)。你可以在回调函数中执行任何你需要的操作，例如更新其他数据、发送请求或者执行其他逻辑。

你也可以监视对象的变化，甚至是对象内部的某个属性的变化。例如：

```javascript
data() {
    return {
      user: {
        name: 'John',
        age: 30
      }
    }
  },
  watch: {
    'user.age': function(newValue, oldValue) {
      // 在user.age属性发生变化时执行的操作
      console.log('user.age属性发生了变化:', oldValue, '->', newValue);
    }
  }
```

# 绑定样式

## class

+ 传递对象

  ```html
  <div :class="{divClass: divistrue}"></div>
  ```

  上面的语法表示 `active` 这个 class 存在与否将取决于数据 property `isActive` 的 [truthiness](https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy)。

+ 绑定的数据对象不必内联定义在模板里：

  ```html
  <div :class="divClassObj">哈哈</div>
  ```

  ```javascript
  	data: {
                  divClassObj:{
                      divClass: true,
                  },
                  message: "aaa",
                  name: 123,
                  name2: "456",
                  divistrue: true,
              },
  ```

  通过Object内部的true和false来决定是否启用类。

+ 我们也可以在这里绑定一个返回对象的[计算属性](https://v2.cn.vuejs.org/v2/guide/computed.html)。这是一个常用且强大的模式

  ```html
  <div :class="divClassObjComputed"></div>
  ```

  计算属性里面返回的是一个类的对象包含true以及false

  ```javascript
  	divClassObjComputed: function() {
                      return {divClass : 1 === 1}
                  }
  ```

## style

+ 通过对象进行定义

+ 注意这里面的data并不可以乱写，而是css，value作为字符串

  ```html
  <div :style="styleObj">这是一段文字</div>
  ```

  ```javascript
  data: {
                  divClassObj:{
                      divClass: true,
                  },
                  styleObj:{
                      color: "blue",
                  },
                  divistrue: true,
              },
  ```

  

# 条件渲染

`v-if` 指令用于条件性地渲染一块内容。这块内容只会在指令的表达式返回 truthy 值的时候被渲染。

也可以用 `v-else` 添加一个“else 块”
