# Vue

[TOC]

### Vue学习要点

> Vue (读音 /vjuː/，类似于 **view**) 是一套用于构建用户界面的**渐进式框架**。

高级功能

- 解耦视图和数据
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
- created（常常用作请求数据）（*组件被创建后回调*）
- beforeMount 
- mounted （*当template挂载到DOM时回调*）
- beforeUpdate
- updated （*当界面刷新的时回调*）
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
  
  

#### 修改webpack配置

- 通过`vue ui`命令交互式配置
- 通过创建`vue.webpack.js`编写配置
- `resolve`解析，其中的`extensions：['.js','.css','.vue']`可以在`import`时不写文件的后缀名



### Vue-router

1. 后端渲染
   - 在后端已经动态渲染好的页面返回给浏览器
2. 前端渲染
   - 即前后端分离，后端只提供API数据，前端将数据渲染到页面中
3. SPA页面(单页面富应用)
   - 在前后端分离的基础上加了一层前端路由
4. 前端路由的核心
   - 改变URL，但是页面不进行整体的刷新
   - `location.hash = 'loc'`
   - `history.pushState({},'','loc')`
   - `history.go(number)` 
5. index.js

```js
// 配置路由相关的信息
import VueRouter from 'vue-router'
import Vue from 'vue'
import Home from '../components/Home.vue'
import About from '../components/About.vue'

// 1.通过Vue.use(插件) 安装插件
Vue.use(VueRouter)

// 2.创建VueRouter对象,必须为routes！！！
const routes = [
  // 默认路径重定向
  // 一个对象是一个route
  {
    path: '/',
    redirect: '/home'
  },
  {
    path: '/home',
    component: Home
  },
  {
    path: '/about',
    component: About
  }
]
const router = new VueRouter({
  routes,
  // 将默认的hash模式更改为history
  mode: 'history',
  // 修改默认的router-link-active为active
  linkActiveClass: 'active'
})

// 3.将router对象传入到Vue实例
export default router
```

6. App.vue

```vue
<template>
  <div id="app">
    <router-view></router-view>
    <!-- 
      to属性用于指定的跳转路径
      tag属性用于指定的标签
      replace属性
      active-class属性用于更改active-class类名
    -->
    <!-- <router-link to="/home" replace tag="button" active-class="active">首页</router-link>< -->
    <!-- <router-link to="/about" replace tag="button">关于</router-link> -->

    <button @click="homeClick">首页</button>
    <button @click="aboutClick">关于</button>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  methods: {
    // 代码跳转
    homeClick() {
      this.$router.push('/home')
      // this.$router.replace('/home')
      console.log('click');
    },
    aboutClick() {
      this.$router.push('/about')
    }
  }
}

</script>

<style>
.router-link-active{
  color:red;
}

.active{
  color:red;
}
</style>
```

7. 动态路由

```js
// index.js
{
  // :userid 绑定,在组件中使用this.$route.params.userid
  path: '/user/:userid',
  component: User
}
// app.vue
<router-link :to="'/user/' + user">用户</router-link>

  data() {
    return {
      user: 'lisi'
    }
  },
  
// user.vue
  computed: {
    userId() {
      // 获取参数
      return this.$route.params.userid
    }
  }
```

8. 路由的懒加载

   - 主要的作用：将路由对应的组件打包成一个个的js代码块
   - 只有在这个路由被访问到的时候才加载对应的组件
   - 懒加载必须使用 `import`不能使用`require`
   - 懒加载的方式：

   ```js
   const Home = () => import('../component/Home')
   const About = () => import('../component/About')
   
   const routes = [
     {
       path: '/home',
       component: Home
     },
     {
       path: '/about',
       component: About
     }
   ]
   ```

   - 嵌套路由

   index.js

   ```js
   const HomeNews = () => import('../components/HomeNews.vue')
   const HomeMessages = () => import('../components/HomeMessages.vue')
   
   const routes = [
     //...
     {
       path: '/home',
       component: Home,
       // 使用children数组定义嵌套路由
       children: [
         // 设置嵌套路由的默认路径
         {
           path: '',
           component: HomeNews
         },
         {
           path: 'news',
           component: HomeNews
         },
         {
           path: 'messages',
           component: HomeMessages
         }
       ]
     }
   ]
   ```

   Home.vue

   ```vue
   <template>
     <div>
       <h2>我是Home</h2>
       <p>Home Content</p>
       <router-link to="/home/news">新闻</router-link>
       <router-link to="/home/messages">消息</router-link>
       <router-view></router-view>
     </div>
   </template>
   ```

9. 参数传递的方式

   - 通过`params`

     ```vue
     <!-- 在子组件取出对象 {userid:"lisi"}-->
     <h2>{{ $route.params }}</h2>
     
     <script>
         //父组件参数传递
         export default {
         	//...
             methods: {
                 userClick(){
                     this.$router.push('/user/' + this.user)
                 }
             }
         }
     </script>
     ```

   - 通过`query`

     ```vue
     <!-- 在子组件取出 父组件传递的`query` 对象 -->
     <h2>{{ $route.query }}</h2>
     
     <script>
         //父组件参数传递
         export default {
         	//...
             data(){
               return {
                   profile: {
                       path: '/profile',
                       query: {
                           name: 'Senku',
                           age: 22,
                           height: '1.88'
                       }
                   }
               }
           }
           methods: {
               profileClick(){
                   //传递query对象
                   this.$router.push(this.profile)
               }
           }
       }
     </script>
     ```

   10. `$router`和`$route`的区别

   - `$router`为VueRouter实例，想要导航到不同的URL，则使用`$router.push`方法
   - `$route`为当前router跳转对象里面可以获取name、path、query、params等

   11. 导航守卫

       监听路由的跳转`router.beforeEach`方法

       - `to`：即将要进入的目标的路由对象
       - `from`：当前导航即将要离开的路由对象
       - `next`：调用该方法后，才能进入下一个钩子

       ```js
       const routes = [
         {
           path: '/',
           component: Home,
           // 可以在route对象定义meta对象存储元数据
           meta: {
             title: '首页'
           }
         }
       ]
       // 全局前置钩子
       router.beforeEach((to, from, next) => {
         // to是一个route对象,
         document.title = to.matched[0].meta.title
         console.log(to);
         // next是一个函数,必须调用
         next()
       })
       
       // 全局后置钩子 
       router.afterEach((to, from) => {
         console.log('------');
       })
       
       ```

   12. keep-alive遇见vue-router

       记录组件的状态

       `keep-alive`-->`actived||deactived`（以keep-alive为前提的hook）

       `keep-alive`有以下两个属性

       - `include`：字符串或正则表达式，只有匹配的组件会被缓存
       - `exclude`：字符串或正则表达式，任何匹配的组件都不会被缓存

       App.vue

       ```vue
       <keep-alive>
       	<router-view/>
       </keep-alive>
       ```

       Home.vue

       ```vue
       <script>
         export default {
           data() {
             return {
               // 记录状态并赋默认值
               path: '/home/news'
             }
           },
           // 以下两个方法只有该组件被保持了状态，即使用了keep-alive时才是有效的
           activated() {
             this.$router.push(this.path)
           },
           deactivated() {
             this.$router.push(this.path)
           },
           // 组件内的守卫
           beforeRouteLeave (to, from, next) {
             this.path = from.path
             next()
        }
         }
       </script>
       ```
   
   13. 修改页面路由重复点击报错
   
       ```js
       const originalPush = VueRouter.prototype.push
          VueRouter.prototype.push = function push(location) {
          return originalPush.call(this, location).catch(err => err)
       }
       ```

### Vuex

Vuex是一个专为`Vue.js`应用程序开发的状态管理模式

#### Vuex的使用

1. 安装`vuex` ：`npm i vuex --save`

2. 在Src下创建`store`文件夹，`index.js`文件

   ```js
   import Vuex from 'vuex'
   import Vue from 'vue'
   
   // 1. 安装插件
   Vue.use(Vuex)
   
   // 2. 创建对象
   export default new Vuex.Store({
     // 保存全局状态
     state: {
       couter: 1000
     },
     // 对状态进行操作
     mutations: {
       increment(state) {
         state.couter++
       },
       decrement(state) {
         state.couter--
       }
     },
     // 常用于异步操作需进行actions，然后传入mutations转化为同步操作
     actions: {
   
     },
     getters: {
   
     },
     modules: {
   
     }
   })
   ```

3. Vuex核心概念

   1. State：单一状态树

   2. Getters：对数据进行操作后给其他组件时使用

      ```js
        getters: {
          powCouter(state) {
            return state.couter**2
          },
          // getters的参数传递
          more20Stu(state) {
            return state.students.filter(s => s.age > 20)
          },
          more20StuLength(state, getters) {
            return getters.more20Stu.length
          },
          moreAgeStu(state) {
            return age => state.students.filter(s => s.age > age)
          }
        },
      ```

   3. Mutation：

      1. 更新数据时，希望携带一些额外的参数，参数被称为`payload`

      ```js
        mutations: {
          increment(state) {
            state.couter++
          },
          decrement(state) {
            state.couter--
          },
          // 当组件调用$store.commit('increments',{
          //         count,
          //    })
          increments(state, payload) {
            state.couter += payload.count
          },
          incrementStu(state, stu) {
            state.students.push(stu)
          }
        },
      ```

      2.  Mutation 必须是同步函数

      3.  Mutation 需遵守 Vue 的响应规则

         - 最好提前在你的 store 中初始化好所有所需属性。

         - 当需要在对象上添加新属性时，你应该

         - 使用 `Vue.set(obj, 'newProp', 123)`, 或者

         - 以新对象替换老对象。例如，利用[对象展开运算符](https://github.com/tc39/proposal-object-rest-spread)我们可以这样写：

           ```js
           state.obj = { ...state.obj, newProp: 123 }
           ```

         - 在对象上删除属性时使用Vue.delete(obj, Key)

           ```js
            Vue.delete(state.info, 'age')
           ```

      4. Mutation 必须是同步函数，异步操作放在actions

      5. 组件中使用 `mapMutations` 辅助函数将组件中的 methods 映射为 `store.commit` 调用（需要在根节点注入 `store`）

         ```js
         import { mapMutations } from 'vuex'
         
         export default {
           // ...
           methods: {
             ...mapMutations([
               'increment', // 将 `this.increment()` 映射为 `this.$store.commit('increment')`
         
               // `mapMutations` 也支持载荷：
               'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.commit('incrementBy', amount)`
             ]),
             ...mapMutations({
               add: 'increment' // 将 `this.add()` 映射为 `this.$store.commit('increment')`
             })
           }
         }
         ```

         

   4. Action

      1. 所有异步操作放在此处处理

         ```js
         // store/index.js  
         actions: {
             [CHANGE](context,payload) {
               return new Promise((resolve, reject) => {
                 setTimeout(() => {
                   context.commit('changInfo')
                   console.log(payload);
                   resolve('I have changed')
                 }, 1000);
               })
             }
           }
         // App.vue
             changeInfo() {
               // 1. 同步操作直接`commit`
               // this.$store.commit('changInfo')
               // 2. 异步操作需要`dispatch`到`actions`
               this.$store
               .dispatch(CHANGE,"I'm payload message")
               .then(res => console.log(res))
             }
         ```

         

   5. Module
   
      1. 可以拥有属于自己的`state`、`mutations`等
      2. 但在组件中获取`state`的值时需要使用`$store.state.moduleName.name`
      3. 在`getters`中具有`rootState`可以获取根的`state`
   
      ```js
      export default {
        state: {
          name: 'zhangsan'
        },
        mutations: {
          updateName(state, payload) {
            state.name = payload
          }
        },
        actions: {
          asyncUpdateName(context, payload) {
            return new Promise((resolve, reject) => {
              setTimeout(() => {
                context.commit('updateName', payload)
                resolve('Name have changed')
              }, 1000);
            })
          }
        },
        getters: {
          fullName(state) {
            return state.name + '1111'
          },
          fullName1(state, getters) {
            return getters.fullName + '2222'
          },
          fullName2(state, getters, rootState) {
            return getters.fullName + rootState.couter
          },
        }
      }
      ```
   
   6. Vuex的项目结构
   
      ```
      ├── index.html
      ├── main.js
      ├── api
      │   └── ... # 抽取出API请求
      ├── components
      │   ├── App.vue
      │   └── ...
      └── store
          ├── index.js          # 我们组装模块并导出 store 的地方
          ├── actions.js        # 根级别的 action
          ├── mutations.js      # 根级别的 mutation
          └── modules
              ├── cart.js       # 购物车模块
              └── products.js   # 产品模块
      ```
   
   
