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



### 数据双向绑定

- v-model

  ```html
  <input v-model="message" type="text" name="" id="">
  <!-- v-model的原理：通过一个v-bind和一个v-on实现 -->
  <input type="text" :value="message" @input="message = $event.target.value">
  ```

- 和radio标签结合

  ```html
  <input v-model="sex" type="radio" name="sex" id="male" value="男">男
  <input v-modeL="sex" type="radio" name="sex" id="female" value="女">女
  <!-- v-model可以替代name属性 name作为key，实现radio的互斥 -->
  ```

- 与checkbox结合

  ```html
  <!-- 单选框：对应布尔类型 -->
  <label for="agree">
      <input type="checkbox" id="agree" v-model="isAgree">同意协议
  </label>
  <button :disabled="!isAgree">下一步</button>
  <h2>{{ message }}</h2>
  
  <!-- 多选框：对应数组 -->
  
  <input type="checkbox" id="" v-model="movies" value="星际穿越">星际穿越
  <input type="checkbox" id="" v-model="movies" value="星际联盟">星际联盟
  <input type="checkbox" id="" v-model="movies" value="盗梦空间">盗梦空间
  <input type="checkbox" id="" v-model="movies" value="死亡笔记">死亡笔记
  <h2>{{ movies }}</h2>
  
  <!-- 值绑定:值不是写死的，而是动态的获取和绑定 -->
  <label v-for="movie in originMovies" :for="movie">
      <input type="checkbox" v-model="movies" :id="movie" :value="movie">{{movie}}
  </label>
  ```

- 与select结合

  ```html
  <!-- 选择多个:绑定一个数组，添加到数组 -->
  <select name=""  v-model="fruits" multiple>
      <option value="apple">apple</option>
      <option value="banana">banana</option>
      <option value="tomato">tomato</option>
  </select>
  ```

- 修饰符

  ```html
  <div id="app">
      <!-- 1.lazy修饰符
          lazy修饰符可以让数据在失去焦点或者回车时才会更新
      -->
      <!-- <input type="text" v-model.lazy="message">
      <h2>{{message}}</h2> -->
  
      <!-- 2.number修饰符
          v-model默认绑定的数据类型是String
          number修饰符可以让在输入框中输入的内容自动转成数字类型
      -->
      <input type="number" v-model.number="age" >
      <h2>{{age}}-{{typeof age}}</h2>
      <!-- 2.trim修饰符
          trim修饰符可以让在输入框中输入的内容去掉左右的两边空格
      -->      
      <input type="text" v-model.trim="name">  
      <h2>{{name}}</h2>
  </div>
  ```

  



### 组件化开发

#### 注册组件的基本步骤

1. 创建组件构造器 --> Vue.extend()
2. 注册组件  --> Vue.component()
3. 使用组件

#### 基本使用

```js
// 全局注册
Vue.component('cpn', {
    template: `<div>组件</div>`,
    data() {
        return {
            name: `Senku`
        }
    }
})
// 局部注册
new Vue({
    //...
    components: {
        template: `<div>组件</div>`,
        // 组件的数据必须是一个函数,保持使用组件时的数据独立
        data() {
            return {
                name: `Senku`
            }
        },
        // 继续嵌套子组件
        components: {/**...*/}
    }
})
```

#### 模板分离

```html
<template id="cpn">
	<div>
        <h2>
            I'm Title
        </h2>
    </div>
</template>

<script>
	Vue.component('cpn', {
        template: '#cpn',
        
    })
</script>
```

#### 组件通信

```html
<!--  movies可以是一个字符串或者是父组件中绑定的值 -->
<cpn :cMovies="movies" :cmes="message"></cpn>
<script>
	Vue.component('cpn', {
        template: '#cpn',
        // 数组传入
        // props:['c-Movies']
        // 对象传入
        props: {
            cMovies: {
                // 类型限制
                type: Array,
                // 提供默认值
                default() { return [] }
            }
        }
    })
</script>
```

#### 组件通信-自定义事件

```html
<!-- 监听事件,不写参数默认传递子组件参数 -->
<cpn @btn-click="cpnClick"></cpn>

<template id="cpn">
    <div>
        <button @click="btnClick(item)" v-for="item in categories">{{item.name}}</button>
    </div>
</template>

<script>
    const cpn = {
        //...
        methods: {
            btnClick(item) {
                // 发射事件:自定义事件传递
                this.$emit('btn-click',item)
            }
        }
    }

    new Vue({
        //...
        components: {
            cpn,
        },
        methods: {
            // 接收事件
            cpnClick(item) {
                console.log('cpnClick',item)
            }
        }
    })
</script>
```

#### 组件访问

- 访问子组件实例或元素

  ```html
  <cpn ref="cpn"></cpn>
  <scirpt>
      // 1.$children
      console.log(this.$children);
      this.$children[0].showMessage();
      // 2.$.refs 常用获取组件方式
      console.log(this.$refs.cpn.name);
  </scirpt>
  ```

- 访问父组件或根组件
  - this.$parent
  - this.$root

### 插槽

- 基本使用

  ```html
  <div id="app">
      <cpn></cpn>
      <!-- <cpn><button>按钮</button></cpn> -->
      <cpn><span>span</span></cpn>
      <cpn><i>i</i></cpn>
      <!-- 当有多个元素时 将会一起替换slot -->
      <cpn>
          <div>div</div>
          <span>span</span>
      </cpn>
  </div>
  
  <template id="cpn">
      <div>
          <h2>我是组件</h2>
          <!-- 默认值插入 -->
          <slot><button>按钮</button></slot>
      </div>
  </template>
  
  ```

- 具名插槽

  ```html
  <div id="app">
      <cpn>
          <!-- 告诉插槽需要替换哪一个 -->
          <span slot="center">标题</span>
      </cpn>
  </div>
  
  <template id="cpn">
      <div>
          <!-- 给插槽命名 -->
          <slot name="left"><span>左边</span></slot>
          <slot name="center"><span>中间</span></slot>
          <slot name="right"><span>右边</span></slot>
      </div>
  </template>
  ```

- 插槽的作用域

  ```html
  <div id="app">
      <cpn></cpn>
      <!-- 父组替换插槽的标签，但是内容由子组件来提供 -->
      <cpn>
          <!-- 获取子组件的pLanguages -->
          <template slot-scope="slot">
              <!-- <span v-for="item in slot.data">  {{item}}-  </span> -->
              <span>{{ slot.data.join(' - ') }}</span>
          </template>
      </cpn>
  </div>
  
  <template id="cpn">
      <div>
          <!-- 绑定data -->
          <slot :data="pLanguages">
              <ul>
                  <li v-for="item in pLanguages">{{item}}</li>
              </ul>
          </slot>
      </div>
  </template>
  ```

  



### Webpack

- gunt/gulp的核心是task
- 什么时候用gunt/gulp
  - 工程模块依赖非常简单，甚至没有用到模块化的概念
  - 只需要简单的合并、压缩，就使用gunt/gulp即可
  - 但是如果整个项目使用了模块化管理，而且相互依赖非常强，我们就可以使用更加强大的webpack
- gunt/gulp和webpack有什么不同？
  - gunt/gulp更加强调的是前端流程的自动化，模块化不是他它的核心
  - webpack更加强调模块化开发管理，而文件压缩合并、与处理等功能，是他附带的功能。

- loader和plugin区别
  - loader主要用于转换某些类型的模块,它是一个转换器
  - plugin是插件,它是对webpack本身的扩展,是一个扩展器

### Vue CLI

> 使用Vue.js开发大型应用时,我们需要考虑代码目录结构,项目结构部署,热加载,代码单元测试等.

> 如果手动完成这个工作,效率比较低效,
>
> 使用vue-cli可以快速搭建Vue开发环境以及对应的webpack配置

#### Vue CLI的使用

```bash
#安装
npm install -g @vue/cli
#拉取2.x版本模板(旧版本)
npm install -g @vue/cli-init
#Vue CLI2 初始化项目
vue init webpack my-project
#Vue CLI3 初始化项目
vue create my-project
```



### runtime-compiler和runtime-only

- Compiler

  > template (parse) -> AST (compiler) -> render -> virtual DOM -> UI

- Only

  > render -> virtual DOM -> UI

- render函数

  ```js
  new Vue({
    el: '#app',
    // components: { App },
    // template: '<App/>'
    render: function (createElement) {
      // 1.createElement('标签', {标签的属性}, [标签的内容])
      // return createElement('h2', {class: 'box'}, ['Hello,World'])
      // 2.传入组件对象
      return createElement(App)
    }
  })
  ```

  .vue文件中的template是由谁处理的?

  vue-template-compiler