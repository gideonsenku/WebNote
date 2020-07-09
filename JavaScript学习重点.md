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

动态作用域，作用域链是基于栈的，而不是代码中的作用域嵌套

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

### 