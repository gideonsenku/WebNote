# HTML响应式总结

### 设置响应头

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

## 使用响应式的图像

#### 使用width属性设置为%

```html
<img src="img_girl.jpg" style="width:100%;">
```

### 使用 the max-width 属性

```html
<img src="img_girl.jpg" style="max-width:100%;height:auto;">
```

### 根据浏览器宽度显示不同的图片

```html
<picture>
  <source srcset="img_smallflower.jpg" media="(max-width: 600px)">
  <source srcset="img_flowers.jpg" media="(max-width: 1500px)">
  <source srcset="flowers.jpg">
  <img src="img_smallflower.jpg" alt="Flowers">
</picture>
```

## 响应式文本大小

The text size can be set with a "vw" unit, which means the "viewport width".

```html
<h1 style="font-size:10vw">Hello World</h1>
```

## Ordered HTML List - The Type Attribute

The `type` attribute of the `<ol>` tag, defines the type of the list item marker:

| Type     | Description                                                  |
| :------- | :----------------------------------------------------------- |
| type="1" | The list items will be numbered with numbers (default)       |
| type="A" | The list items will be numbered with uppercase letters       |
| type="a" | The list items will be numbered with lowercase letters       |
| type="I" | The list items will be numbered with uppercase roman numbers |
| type="i" | The list items will be numbered with lowercase roman numbers |

## HTML Web Storage Objects

HTML web storage provides two objects for storing data on the client:

- `window.localStorage` - stores data with no expiration date
- `window.sessionStorage` - stores data for one session (data is lost when the browser tab is closed)

![webstorge](/Users/Senku/Desktop/webstorge.png)

