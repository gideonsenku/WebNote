## Webpack

### 为什么需要构建工具

- 转换ES6语法
- 转换JSX
- CSS前缀补全/预处理器
- 压缩混淆
- 图片压缩

### 配置文件

默认：webpack.config.js

指定：webpack --config 指定配置文件

```js
module.exports = {
  mode: 'development',
  devtool: 'inline-source-map',
  devServer: {
    contentBase: './dist',
    hot: true
  },
  entry: {
    app: './src/index.js',//指定打包入口，单入口是一个字符串，多入口是一个对象
  },
  output: {
    filename: '[name].bundle.js',// [name]占位符，确保文件名称的唯一
    path: path.resolve(__dirname, 'dist')
  },
  plugins: [
    // new CleanWebpackPlugin(['dist']),
    new webpack.NamedModulesPlugin(),
    new webpack.HotModuleReplacementPlugin(),
    new HtmlWebpackPlugin({
      title: 'Output',
    }),
  ]
}
```

### Loaders

webpack只支持JS和JSON两种文件类型，通过Loaders去支持其他文件类型并且将它们转化成有效的模块，并且可以添加到依赖图中。

本身是一个函数，接受源文件作为参数，返回转换的结果。

常见的Loaders

| 名称          | 描述                       |
| ------------- | -------------------------- |
| babel-loader  | 转换ES6、ES7等JS新特性语法 |
| css-loader    | 支持.css的加载和解析       |
| less-loader   | 将Less转换成CSS            |
| ts-loader     | 将TS转换成JS               |
| file-loader   | 进行图片、字体等的打包     |
| raw-loader    | 将文件以字符串的形式导入   |
| thread-loader | 多进程打包JS和CSS          |



### 文件指纹

- `Hash`：和整个项目的构建相关，只要项目文件有修改，整个项目构建的`hash`值就会更改
- `Chunkhash`：和webpack打包的`chunk`有关，不同的`entry`会生成不同的`chunkhash`值
- `Contenthash`：根据文件内容定义的`hash`，文件内容不变，则`contenthash`不变

