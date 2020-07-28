#### 箭头函数

- 箭头函数没有 “this”

- 不能对箭头函数进行 `new` 操作，没有`new.target`

  > 不具有 `this` 自然也就意味着另一个限制：箭头函数不能用作构造器（constructor）。不能用 `new` 调用它们

- 箭头函数也没有 `arguments` 变量

- 箭头函数也没有`super`

- 没有原型对象

- 形式参数名称不能重复

**箭头函数 VS bind**

箭头函数 `=>` 和使用 `.bind(this)` 调用的常规函数之间有细微的差别：

- `.bind(this)` 创建了一个该函数的“绑定版本”。
- 箭头函数 `=>` 没有创建任何绑定。箭头函数只是没有 `this`。`this` 的查找与常规变量的搜索方式完全相同：在外部词法环境中查找。

```javascript
//ajax
var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState === 4 && this.status === 200) {
      console.log(this.responseText);
    }
  };
  xhttp.open("POST", "/api.json", true);
  xhttp.send();

//jQuery ajax
$.ajax('/').then(function(response){
    console.log(response)
})

//采用fetch调用json数据
fetch('/api.json')
  .then(function(response) {
  return response.json()
}).then(function(json) {
  console.log('parsed json', json)
}).catch(function(ex) {
  console.log('parsing failed', ex)
})

//使用箭头函数
fetch('/api.json')
  .then(response => response.json)
  .then(json => { console.log('parsed json', json)
  }).catch(ex => {
  console.log('parsing failed',ex)
})
```

#### 解构赋值

```javascript
const obj = { id: "007", name: "Conan", age: 28 };
const { name, age, id } = obj;
console.log(name);  //Conan
console.log(age);   //28
console.log(id);    //007
// 指定默认值
// 默认值生效的条件是，对象的属性值严格等于undefined。
// 等于null则不生效。

const { x = 3 } = { x: undefined };
console.log(x); //3

const { y = 3 } = { y: null };
console.log(y); //null

// 配合扩展运算符对Object进行解构
const {id, ..._obj} = obj;
console.log(id);   // 007
console.log(_obj); // { name: "Conan", age: 28 }
```

#### 扩展运算符

