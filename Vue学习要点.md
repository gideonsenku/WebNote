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
    }
}
```

*计算属性和methods最本质的区别:*

*1.计算属性只有在其相关依赖发生改变时才会重新计算,大幅度提升了程序的执行效率,节省内存空间*

*2.methods无论其依赖的data数据是否改变,每一次调用都会重新计算*

*3.在实际使用场景中优先使用计算属性*

