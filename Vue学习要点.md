# Vue

[TOC]

### Vue学习要点

> Vue (读音 /vjuː/，类似于 **view**) 是一套用于构建用户界面的**渐进式框架**。

高级功能

- 解耦试图和数据
- 可复用的组件
- 前端路由技术（router）
- 状态管理（Vuex）
- 虚拟DOM

### Vue中的MVVM

##### 什么是MVVM？

- Model View View Model

##### Vue的MVVM

- View（DOM）--> ViewModel（Vue）--> Model（Plain JavaScript Objects）

#### 生命周期

- vue生命周期函数不能使用箭头函数
- beforeCreate
- created（常常用作请求数据）
- beforeMount
- mounted
- beforeUpdate
- updated
- beforeDestory
- destroyed

### 插值语法

#### v-once

> 该指令表示元素和组件只渲染一次，不好随着数据的改变而改变
>
> 该指令后面不需要跟任何表达式

```html
<h3 v-once>{{message}}</h3>
```

#### v-html

```html
<h2 v-html="url"></h2>
```

#### v-text（一般不用）

```html
<h2 v-html="message"></h2>
```

#### v-cloak

- 在某些情况下，我们的浏览器可能会直接显示出未编译的Mustache标签

```css
<style>
    [v-cloak] {
        display: none;
    }
</style>
<div id="app" v-cloak>
</div
```

#### v-pre

- 类似pre标签,原封不动的显示，不做解析处理

```html
<h3 v-pre>{{ message }}</h3>
```



#### Attribute Binding

```html
<img v-bind:scr="imgae"></img>
<img :scr="imgae"></img>
<a :href="href"></a>
<!-- else --> 
```

```javascript
var vm = new Vue({
  el:'#app',
  data:{
    imgae:'address'
    //else...
  }
});
```

- Data can be bound to HTML attributes
- `v-bind:src="expression"`
- Syntax is `v-bind:` or `:` for short.

### 计算属性

*do not excute functionm*

*`computed` property it's a Object*

*example:*

> *{{ fullName() }} //error method*

```js
// origin computed, ignore setter
// do not use array function
computed: {
  fullName: function() {
    return this.firstName + ' ' + this.lastName
  },
  // getter && setter function
  fullNames: {
   // setter不常用
   set: function (newValue) {
      console.log('------------');
      const names = newValue.split(' ');
      this.firstName = names[0];
      this.lastName = names[1];
   },
   get: function () {
     return this.firstName + ' ' + this.lastName
    }
  }
}


```

*计算属性和methods最本质的区别:*

*1.计算属性只有在其相关依赖发生改变时才会重新计算,大幅度提升了程序的执行效率,节省内存空间*

*2.methods无论其依赖的data数据是否改变,每一次调用都会重新计算*

*3.在实际使用场景中优先使用计算属性*

### 事件监听

- Syntax is `v-on:` or `@` for short

  - @event="fuctionName"

  - @click="do(args,$event)"

    > $event:*使用`$event`手动获取浏览器event对象*

- 修饰符

  - .stop：*阻止当前元素的冒泡行为*
  - .prevent：*阻止默认行为*
  - .enter：*监听某个键盘的键帽*
  - .once:*只触发一次回调*

### 条件判断

- `v-if`

  ```html
  <h2 v-if="false">{{ message }}</h2>
  <h2 v-if="true">{{ message }}</h2>
  <h2 v-if="isShow">{{ message }}</h2>
  <!--
  data: {
    message:'Hello',
    isShow: true
  }, 
  -->
  ```

  

- `v-else`

  ```html
  <div v-if="false">
      <h2> v-if </h2>
      <h2 v-if="true">{{ message }}</h2>
      <h2 v-if="isShow">{{ message }}</h2>
  </div>
  <div v-else>
      <h2> v-else </h2>
      <h2 v-if="true">{{ message }}</h2>
      <h2 v-if="isShow">{{ message }}</h2>
  </div>
  ```

  

- `v-else-if`

  ```html
  <h2 v-if="score>=90">优秀</h2>
  <h2 v-else-if="score>=80">良好</h2>
  <h2 v-else-if="score>=60">及格</h2>
  <h2 v-else>不及格</h2>
  ```

  ```html
  <span v-if="isUser">
      <!-- for属性用户点击聚焦到 input 输入框 -->
      <label for="username">账号</label>
      <input type="text" placeholder="用户账号" id="username">
  </span>
  <span v-else>
      <label for="email">邮箱</label>
      <input key="email" type="text" placeholder="用户邮箱" id="email">
  </span>
  <button @click="change">切换类型</button>
  ```

  

  如果我们在有输入内容的情况下，切换了类型，默认文字依然保留

  需求：切换时清除内容

  问题原因：

  > Vue在DOM渲染时，出于性能考虑，会尽可能的复用已经存在的元素

  解决方案：

  > 如果我们不希望Vue出现类似重复利用的问题，可以给对应的`input`添加`Key`

  > 需要保证`Key`不同

- `v-if`和`v-show`的区别

   v-if：条件为false时，包含v-if指令的元素，根本就不会存在DOM中

  v-show：条件为false时，增加行内样式` {display:none;}`

  开发时如何选择：

  当显示和隐藏之间切换频率很频繁时，使用`v-show`

  当只有一次切换时，使用`v-if`

### 循环遍历

- `v-for`

  ```html
  <!-- 在遍历对象的过程中，如果只是获取一个值，那么获取到的是Value -->
  <ul>
      <li v-for="val in info"> {{ val }} </li>
  </ul>
  <!-- 获取Key和Value -->
  <ul>
      <li v-for="(val, key) in info">{{ key }}-->{{ val }}</li>
  </ul>
  <!-- 获取Key和Value以及index -->
  <ul>
      <li v-for="(val, key, index) in info">{{ index }}-->{{ key }}-->{{ val }}</li>
  </ul>
  ```

- `:key`

  ```html
  <ul>
      <!-- :key要确保唯一性,注意：不使用index，无法确定数据的唯一性 -->
      <!-- key的作用主要是为了高效的更新虚拟DOM -->
      <li :key="letter" v-for="letter in letters">{{ letter }}</li>
  </ul>
  ```

- 哪些数组方法是响应式的（动态更新DOM）

  1. Array.push()：数组尾部插入元素（一个或多个）
  2. Array.pop()：数组尾部删除一个元素
  3. Array.shift()：数组首部删除一个元素
  4. Array.unshift()：数组首插入元素（一个或多个）
  5. Array.splice()：插入、删除、更新数组
  6. Vue.set()

  而通过下标索引值更新则不是响应式的

### 过滤器

过滤器：添加一个竖线 竖线前面的会作为参数传入过滤器

```html
<div id="app">
<h3>总价格{{totalPrice | filterPrice}}</h3>
</div>
<script>
let app = new Vue({
  el:'#app',
  data: {
    totalPrice: 129,
  },
  filters: {
    filterPrice(price) {
      return '￥'+price.toFixed(2)
    ht}
  }
})
</script>
```

