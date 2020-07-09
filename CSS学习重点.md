# CSS

## CSS选择器

```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
  <!-- 父子/直接子类选择器-->
  <div><span></span></div>
  <div class="demo">
    <p>
      <a href="javascript:void(0)">link</a>
    </p>
    <span>
    	<p></p>
    </span>
  </div>
  
  <!-- 并列选择器-->
  <div>1</div>
  <div class="demo">2</div>
  <p class="demo">3</p>
</body>
</html>
```

选择器表

|       名称       |     示例     |
| :--------------: | :----------: |
|    父子选择器    |   div a {}   |
| 直接子元素选择器 |  div > p {}  |
|    并列选择器    | div.class {} |
|    分组选择器    | p,span,div{} |
|    伪类选择器    |  a:hover{}   |

选择器权重表

|       名称        |   权重   |
| :---------------: | :------: |
|    !important     | Infinity |
| 行间样式(inline)  |   1000   |
|        id         |   100    |
| class｜属性｜伪类 |    10    |
|   标签｜伪元素    |    1     |
|     通配符(*)     |    0     |

> 其中优先级的进制为:256
>
> 浏览器对元素选择时采取自右向左的方式,下面的选择会从`em`开始选择

```css
section ul li a span em{
	/* some code in here. */
}
```

### CSS元素类别

CSS 行级(内联)元素`display:inline`:

1. 不会独占一行,相邻的行级元素会排在同一行。**其宽度随内容的变化而变化**。 
2. 内联元素不可以设置宽高
3. 内联元素可以设置margin，padding，**但只在水平方向有效**。

- a、br、em、img、input、span、strong

CSS块级元素`display:block`:

1. 独占一行、**默认情况下宽度自动填满其父元素宽度** 
2. 可以通过CSS改变宽高
3. 块级元素可以设置margin，padding

- div、ol、ul、li、h1-h6、form、p、table

CSS行级块元素`display:inline-block`:

1. 内容决定大小、可以更改宽高
2. 使其既具有block的宽度高度特性又具有inline的同行特性。
   1. 被设置了`position`和`float`的元素,在内部会被转化为`display:inline-block`

CSS伪元素`a::before/after`含有`content`属性,并且是`inline`属性

> 带有inline值的元素都有文字特性 -> 会被分割

> 先写CSS后写HTML

> **利用伪元素来清除浮动**

```css
selector::after {
	content:"";
	clear:both;
	display:block;
}
```

CSS中的`display:none`和`visibility:hidden`的区别

```css
p{
  display:none;/* 隐藏,不占原有位置 */
}
p{
  visibility:hidden;/* 不可视,占原有位置 */
}
```



### CSS盒子模型

> box=margin+border+padding+(content=height+width
>
> 外边距+边框+内边距+内容

> 行级元素嵌套行级元素
>
> 块级元素可以嵌套任何元素
>
> **`<p><div></div></p>`不允许**

> IE盒模型 `box-sizing:border-box`
>
> Box = height+width
>
> 可以不用关心频繁修改border和padding的困扰

### CSS定位/层模型

- 绝对定位 `absolute`
  - 脱离原来位置进行定位
  - 相对于最近的有定位的父级进行定位,如果没有则相对文档定位

- 相对定位 `relative`
  - 保留原来位置进行定位
  - 相对于自己原来的位置进行定位
- 固定 `fixed`

> 与`left/right`和`top/bottom`搭配

> 常常用`relative`作为参照物,用`absolute`进行定位

```css
body{margin:8px;}/*body的默认值*/
```

### CSS BFC(Block Fomat Context)

如何触发一个盒子的BFC,使得子盒子能够相对父盒子进行`magin-top`

```css
position:absolute
display:inlin-block
float:left/right
overflow:hidden
```

- 创建BFC的元素，它的自动高度需要计算浮动元素
- 创建BFC的元素，它的边框盒不会与浮动元素重叠
- 创建BFC的元素，不会和它的的子元素进行外边距合并



浮动元素产生浮动流

> 所有产生了浮动流的元素,块级元素看不到他们
>
> 产生了BFC的元素和文本类属性 (inline)的元素以及文本能够看到浮动元素
>
> > **利用伪元素来清除浮动**
>
> ```css
> selector::after {
> 	content:"";
> 	clear:both;
> 	display:block;
> }
> ```
>

### CSS文字溢出处理、背景图片处理

- 单行内容过多展示...

  ```css
  .no-more-content{
  	width:300px;
    height:30px;
    line-height:30px;
    
    white-space:nowrap;/* 不换行输出*/
    overflow:hidden;/* 溢出输出隐藏*/
    text-overflow: ellipsis;/* 输出...*/
  }
  ```

- 多行直接截断处理

- 背景图片处理知识点(保留文字信息)

  ```html
  <!DOCTYPE html>
  <html>
  <head>
    <style>
    	<!-- padding可以设置background-color或者bacground-img -->
      a{
        display:inline-block;
        text-decoration:none;
        width:190px;
        background-img:url();
        background-size:190px 90px;
        /* 方法一 */
        height:0px;
        padding-top:90px;/* 让图片放在padding中 */
        overflow:hidden;
        
        /* 方法二 */
        height:90px;
        white-space:nowrap;
        text-indent:200px;/* 设置缩进使得文字内容超出盒子 */
        overflow:hidden;
      }
    </style>
  </head>
    <body>
      <a href="#">淘宝</a>
    </body>
  </html>
  ```

  

### 水平垂直居中汇总

#### 1.水平居中

- 内联元素：

  父元素，设置`text-align: center`

- 定宽块级元素：

自身，设置`margin: 0 auto`

- 定宽浮动元素：
  设置定位后，可以重新布局元素框，进而定位到中点，是从中点开始排布，因此需要会拉自身宽度一半，达到居中的效果。

  自身，设置`position: relative; left: 50%; margin-left: -(1/2) width`
  自身，设置`position: absolute; top: 0; right: 0; bottom: 0; left: 0; margin: auto;`

- 未知宽度的块级元素：
  自身，设置`display: table; margin: auto`
  自身，设置`position: absolute; left: 50%; transform: translateX(-50%)`
  自身，设置`width: fit-content; margin: auto`
  自身，设置`display: flex; justify-content: center;`
  父级，设置`display: flex; flex-direction: column; 自身，设置align-self: center`
  父级，设置`display: flex; 自身，设置margin: auto`
  父级，设置`display: inline-block; position: relative; left: 50%` 自身，设置`position: relative; right: 50%`

#### 2.垂直居中

- 内联元素：
  自身，设置`line-height: height`
  父级，设置`line-height: son-height;`自身，设置`vertical-align: middle`

  > 其中``vertical-align`属性常用来解决行盒的垂直对齐

- 知道容器高度并且容器内只有一个元素：
  自身，设置`position: relative; top: 50%; transform: translateY(-50%)`
- 不知道容器与自身高度：
  父级，设置`position: relative;` 自身，设置`position: absolute；top: 50%; transform: translateY(-50%)`
  父级，设置`display: flex; align-items: center`



### 图片的底部白边

```html
<html>
  <head>
    <style>
      div{border:2px solid;}
      img{display:block}
    </style>
  </head>
  <body>
    <div>
      <img src="1.jpg">
    </div>
  </body>
</html>
```

> 图片的父元素是一个块盒，块盒高度自动，图片底部和父元素之间往往会出现白边
>
> 常将图片属性`display:block`可解决该问题



### 行高的各种区别

> `linehight`值有多种
>
> 数字`1.5` 像素`15px` em`1.5em`百分比 `150%` `normal`

```css
body {
  /* 使用数字方式,子元素会继承父元素的line-hight进行计算 */
  font-size:12px;
  line-hight:1.5;
}
body {
  font-size:12px;
  line-hight:1.5em;
  line-hight:160%;
}
p {
  /* 在数字情况下 line-hight为 10*1.5=15px */
  /* 在em或者百分比的情况下 line-height是 12*1.5   12.160% */
  font-size:10px;
}
```

> 所以在重置样式中选择数字形式，使得子元素继承父元素的行高值

