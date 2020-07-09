### Vue学习要点

#### 生命周期

- vue生命周期函数不能使用箭头函数

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

