# JavaScript学习重点

### 函数

函数声明

```javascript
function demo() {}
```

命名函数表达式

```javascript
var test = function abc() {
// statments...
}
//test.name = abc
```

匿名函数表达式/函数表达式

```javascript
var demo = function () {
//statments...
}
//demo.name = demo
```

函数预编译

​		函数声明整体提升

​		变量    声明提升

​		函数会首先被提升，然后才是变量，并且后面出现的函数声明会覆盖前面的

1. 创建AO对象
2. 找形参和变量声明，将形参名和变量作为AO的属性名并赋值`undefined`
3. 将实参值和形参统一
4. 在函数体中找函数声明，并赋予函数体

构造函数内部原理

```javascript
function Student(){
//var this = {}
//this={
//name:"",
//sex:"",
//...
//}
this.name="name";
this.sex="male";
//return this
}

var stu = new Student()
```

词法作用域，作用域链是基于调用栈的，而不是代码中的作用域嵌套

```javascript
function foo(){
    console.log(a);//2
}

function bar(){
    var a = 3;
    foo()
}

var a = 2 
bar()
```



### 其他

1、replace函数的第二个个参数可以是回调函数

   该函数有多个可选参数

- 匹配到的字符串

- 如果正则使用了分组匹配就为多个，否则无此参数

  回调函数返回替换的值，如果没有返回，默认为undefined 

- 匹配字符串的对应索引位置

- 原始字符串

```javascript
function replacer(match, p1, p2, p3, offset, string) {
	console.log(match)
  	return [p1, p2, p3].join(' - ');
}
var newString = 'abc12345#$*%'.replace(/([^\d]*)(\d*)([^\w]*)/, replacer);
// newString的结果是 abc - 12345 - #$*%
//match是匹配到的字符串
```

### 模块机制

- import可以将一个模块中的一个或多个API导入代当前代作用域中，并分别绑定到一个变量上

- module会将整个模块的API导入并绑定到一个变量上

- node环境下使用module.exports导出模块,require('/path/to/moduleName')导入

- 一个模块就是一个文件。浏览器需要使用 `<script type="module">`
  以使`import/export`可以工作。
  模块（译注：相较于常规脚本）有几点差别：
- 默认是延迟解析的（deferred）。
  - Async 可用于内联脚本。
  - 要从另一个源（域/协议/端口）加载外部脚本，需要 CORS header。
  - 重复的外部脚本会被忽略
  
- 模块具有自己的本地顶级作用域，并可以通过 `import/export` 交换功能。

- 模块始终使用 `use strict`。

- 模块代码只执行一次。导出仅创建一次，然后会在导入之间共享。
```javascript
//bar.js
function hello(who){
	return `Let me introduce: ${who}`;
}
export hello;

//foo.js
import hello from 'bar';
var hungry = 'hippo';
function awesome(){
  console.log(hello(hungry).toUpperCase());
}
export awesome;

//baz.js
module foo from 'foo';
module bar from 'bar';
console.log(bar.hello('Something'));
console.log(foo.awessome());

// sum.js
module.exports = function(a, b) {
    return a + b
}

// index.js
var sum = require('./sum')
console.log(sum(1, 2))
```





### this

this实际上是在函数被调用时发生的绑定，它指向什么完全取决于函数在哪里被调用

```javascript
window.name = 'hello'

function A() {
    this.name = 123;
}

A.prototype.getA = function () {
    console.log(this);
    return this.name + 1;
}
/*
* 
A{
    name:123,
    __proto__:{
        getA:function(){
            console.log(this);
            return this.name + 1;
        },
        // other...
    },
}
*/

let a = new A();
let funcA = a.getA;
console.log(funcA())
console.log(new A().getA())
```

### 样式

```js
/*
* getStyle method:
* 1.use > para.style.property
* const para = document.getElementById('element');
* const style = para.style.property
* 2.use > getComputedStyle(element, [pseudoElt]);
* let theCSSprop = window.getComputedStyle(elem,null).getPropertyValue("height");
* setStyle method:
* element.style.property = value
*/
```

document.querySelector

如果要匹配的ID或选择器不符合 CSS 语法（比如不恰当地使用了冒号或者空格），你必须用反斜杠将这些字符转义。由于 JavaScript 中，反斜杠是转义字符，所以当你输入一个文本串时，你必须将它转义两次（一次是为 JavaScript 字符串转义，另一次是为 `querySelector` 转义）：

```html
<div id="foo\bar"></div>
<div id="foo:bar"></div>

<script>
  console.log('#foo\bar')               // "#fooar"
  document.querySelector('#foo\bar')    // 不匹配任何元素

  console.log('#foo\\bar')              // "#foo\bar"
  console.log('#foo\\\\bar')            // "#foo\\bar"
  document.querySelector('#foo\\\\bar') // 匹配第一个div

  document.querySelector('#foo:bar')    // 不匹配任何元素
  document.querySelector('#foo\\:bar')  // 匹配第二个div
</script>
```

**查找第一个匹配 class属性的html元素**

这个例子中，会返回当前文档中第一个类名为 "`myclass`" 的元素：

```js
var el = document.querySelector(".myclass");
```

**一个更复杂的选择器**

*选择器也可以非常强大，如以下示例所示*.

这里, 一个class属性为"user-panel main"的div元素[``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/div)(`<div class="user-panel main">`)内包含一个name属性为"login"的input元素[``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input) (`<input name="login"/>`) ，如何选择，如下所示:

```js
var el = document.querySelector("div.user-panel.main input[name='login']");
```

### JSONP

##### 什么是JSONP

> `<script>`元素可以作为一种Ajax传输机制：只须设置`<script>`元素的src属性（假如它还没插入到document中，需要插入进去），然后浏览器就会发送HTTP请求下载src属性所指向的URL。
>
> 使用`<script>`元素进行Ajax传输的一个主要原因是：
>
> - 它不受同源策略的影响，因此可以使用它们从其他的服务器请求数据，
>
> - 第二个原因是包含JSON编码数据的响应体会解码。 

> 这种使用`<script>`元素作为Ajax传输的技术称为JSONP。

> 假设你已经写了一个服务，它处理GET请求并返回JSON编码的数据，同源文档可以在代码中使用XMLHttpRequest和JSON.parse()。假如在服务器上启用了CORS，在新的浏览器下，跨域的文档也可以使用XMLHttpRequest享受到该服务。
>
> 在不支持CORS的旧浏览器下，跨域文档只通过`<script>`元素访问这个服务。使用JSONP，JSON响应数据是合法的JavaScript代码，当它到达浏览器将执行它。

##### 二、原理分析

同源策略下，某个服务器是无法获取到服务器以外的数据，但是html里面的**`img,iframe和script等标签是个例外`**，这些标签可以通过src属性**请求到其他服务器上的数据**。而JSONP 就是通过script节点src调用跨域的请求。
 当我们向服务器提交一个JSONP的请求时，我们给服务传了一个特殊的参数，告诉服务端要对结果特殊处理一下。这样服务端返回的数据就会进行一点包装，客户端就可以处理。
 例如。服务端和客户端约定要传一个名为callback的参数来使用JSONP功能，比如请求的参数如下：

> [http://www.example.net/sample.aspx?callback=mycallback](https://link.jianshu.com?t=http://www.example.net/sample.aspx?callback=mycallback)

如果没有后面的callback参数，即不使用JSONP的模式，该服务的返回结果可能是一个单纯的json字符串,比如：`{foo:'bar'}`。但是如果使用JSONP模式，那么返回的是一个函数调用:`mycallback({foo:'bar'})`，这样我们在代码之中，定义一个名为mycallback的回调函数，就可以解决跨域问题了。

```html
<!DOCTYPE html> 
<html> 
<head> 
<meta charset="utf-8"> 
<script src="http://code.jquery.com/jquery-1.8.0.min.js"></script> 
<title></title> 
</head> 
<body> 
<div class="main">
    <form>
        <input type="text" id="keyWords" />
        <input type="button" id="search" value="百度一下" />
    </form>
    <ul id="result"></ul>
</div>
<script type="text/javascript"> 
function relatedWords(data){ 
    var _html=[]; 

    for(var i=0;i<data.s.length;i++){
        _html.push('<li>' + data.s[i] + '</li>');
    }

    $('#result').html(_html.join(''));
}; 

$(function(){ 
    $('#keyWords').keyup(function() { 
        var val = $(this).val(); 
        if (val.trim() == '') {
            return ;
        }

        $.ajax({ 
            url:'http://suggestion.baidu.com/su?wd='+val+'&json=1&p=3&req=2&cb=relatedWords', 
            dataType:'jsonp' 
        });
    }); 
}); 
</script> 
</body> 
</html>
 <!-- 
作者：_李雷
链接：https://www.jianshu.com/p/c45061494bba
来源：简书
--> 
```

