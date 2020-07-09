### jQuery笔记

> jQuery is a fast, small, and feature-rich JavaScript library.

jQuery包含以下功能

- HTML元素选取
- HTML元素操作
- CSS操作
- HTML事件函数
- JavaScript特效和动画
- HTML DOM遍历和修改
- AJAX
- Utilities

##### 一、基础语法

``` javascript
$(function(){
  $(selector).action();//选择+行为
})

//example
$(function(){
  $(this).hide()//隐藏当前元素
})
```

### 二、选择器

```javascript
// $("p") 元素选择
// $("#id") id选择
// $(".class")  class选择

$("div.menu")  // 选取class为menu的div元素
$("p:first")  // 第一个<p>元素
$("h1, p") // 所有<h1>和所有<p>元素
$("div p") // 所有<div>元素后代的<p>元素
$("*")  // DOM的所有元素
$("this")  // 选取当前HTML元素
$("ul li:first")  //选取第一个<ul>元素的第一个<li>元素
$("ul li:first-child")  //选取每个<ul>元素的第一个<li>元素
$("[href]")	//选取带有href属性的元素
$("a[target='_blank']")	//选取所有target属性值=_blank的<a>元素
$("a[target!='_blank']")	//选取所有target属性值!=_blank的<a>元素
$(":button")	//选取所有type="button"的<input>元素和<button>元素
$("tr:even")	//选取偶数位置的<tr>元素
$("tr:odd")	//选取奇数位置的<tr>元素

$("attribute:value")	//选取值为value的property元素
```

### 三、隐藏和显示

```javascript
//语法
$(selector).hide(speed,callback);	//隐藏
$(selector).show(speed,callback);	//显示
$(selector).toggle(speed,callback);	//在隐藏和显示切换

//可选的 speed 参数规定隐藏/显示的速度，可以取以下值："slow"、"fast" 或毫秒。
//可选的 callback 参数是隐藏或显示完成后所执行的函数名称。
```

#### 四、淡入和淡出

```javaScript
$(selector).fadeIn(speed,callback);	//淡入已隐藏元素
$(selector).fadeOut(speed,callback);	//淡出可见元素
$(selector).fadeToggle(speed,callback);	//在淡入和淡出之间切换
$(selector).fadeTo(speed,callback);	//允许渐变为给定的不透明度（值介于 0 与 1 之间）
```

#### 五、滑动

```javascript
$(selector).slideDown(speed,callback);	//向下滑动元素
$(selector).slideUp(speed,callback);	//向上滑动元素
$(selector).slideToggle(speed,callback);	//切换
```

#### 六、动画和停止动画

```javascript
$(selector).animate({params},speed,callback);
//必需的 params 参数定义形成动画的 CSS 属性, 可操作多个属性, 
//可使用相对 +=、-=, 可使用预定义的show、hide、toggle

//默认情况下，所有 HTML 元素都有一个静态位置，且无法移动。
//如需对位置进行操作，要记得首先把元素的 CSS position 属性设置为 relative、fixed 或 absolute！

//默认地，jQuery 提供针对动画的队列功能。
//这意味着如果您在彼此之后编写多个 animate() 调用，jQuery 会创建包含这些方法调用的"内部"队列。然后逐一运行这些 animate 调用。
//Callback 函数在当前动画 100% 完成之后执行。
$("button").click(function(){
  var div=$("div");
  div.animate({height:'300px',opacity:'0.4'},"slow");
  div.animate({width:'300px',opacity:'0.8'},"slow");
  div.animate({height:'100px',opacity:'0.4'},"slow");
  div.animate({width:'100px',opacity:'0.8'},"slow");
});

$(selector).stop(stopAll,goToEnd);
//可选的 stopAll 参数规定是否应该清除动画队列。默认是 false，即仅停止活动的动画，允许任何排入队列的动画向后执行。
//可选的 goToEnd 参数规定是否立即完成当前动画。默认是 false。
//因此，默认地，stop() 会清除在被选元素上指定的当前动画。
```

#### 七、jQuery与HTML

##### 设置元素

```javascript
$(selector).text();	//设置或返回所选元素的文本内容
$(selector).html();	//设置或返回所选元素的内容（包括 HTML 标记）
$(selector).val();	//设置或返回表单字段的值
$(selector).attr("attr_name");	//用于获取属性值
$(selector).attr("attr_name","value");//用于设置属性值,可以设置多个
```

##### 添加元素

```javascript
$("p").append("追加文本");//append() 方法在被选元素的结尾插入内容（仍然该元素的内部）
$("p").prepend("在开头追加文本");//prepend() 方法在被选元素的开头插入内容

$("img").after("在后面添加文本");//after() 方法在被选元素之后插入内容。
$("img").before("在前面添加文本");//before() 方法在被选元素之前插入内容。
//可以添加若干个新元素,以上四个方法都适用
function appendText()
{
    var txt1="<p>文本</p>";              // 使用 HTML 标签创建文本
    var txt2=$("<p></p>").text("文本");  // 使用 jQuery 创建文本
    var txt3=document.createElement("p");
    txt3.innerHTML="文本";               // 使用 DOM 创建文本 text with DOM
    $("body").append(txt1,txt2,txt3);        // 追加新元素
}
```

##### 删除元素

```javascript
$("#div1").remove();//删除被选元素（及其子元素）
$("#div1").empty();//从被选元素中删除子元素
//jQuery remove()方法也可接受一个参数，允许您对被删元素进行过滤。该参数可以是任何jQuery选择器的语法。
$("p").remove(".italic");
```

##### CSS类

```javascript
$(selector).addClass();//向被选元素添加一个或多个类
$(selector).removeClass();//向被选元素移除一个或多个类
$(selector).toggleClass();//对被选元素进行添加/删除类的切换操作
$(selector).css();//设置或返回样式属性
.css("propertyname")//返回
.css("propertyname","value")//设置
```

##### 尺寸

```javascript
$(selector).width();//width() 方法设置或返回元素的宽度(不包括内边距、边框或外边距)
$(selector).height();//height() 方法设置或返回元素的高度(不包括内边距、边框或外边距)
$(selector).innerWidth();//innerWidth() 方法返回元素的宽度(包括内边距)
$(selector).innerHeight();//innerHeight() 方法返回元素的高度(包括内边距)
$(selector).outerWidth();//outerWidth() 方法返回元素的宽度(包括内边距和边框)
$(selector).outerHeight();//outerHeight() 方法返回元素的高度(包括内边距和边框)
```

#### 八、遍历

##### 祖先、后代

```javascript
$(selector).parent();//parent() 方法返回被选元素的直接父元素,该方法只会向上一级对 DOM 树进行遍历
$(selector).parents();//parents() 方法返回被选元素的所有祖先元素,它一路向上直到文档的根元素 (<html>)
$(selector).parentsUntil();//parentsUntil() 方法返回介于两个给定元素之间的所有祖先元素

$(selector).children();//children() 方法返回被选元素的所有直接子元素,该方法只会向下一级对 DOM 树进行遍历
$(selector).find();//find() 方法返回被选元素的后代元素，一路向下直到最后一个后代

//以上方法都可加参数指定
```

