# Webpack 基础知识

## 四个核心概念

- entry(入口)
- output(出口)
- module
- plugins

## entry(入口)

`entry` 是整个配置文件的入口,可以配置单文件入口，也可以配置多文件入口

- 单文件入口，也就是常用的单页面应用配置

```
const { resolve } = require('path')
module.exports = {
  entry:resolve(__dirname,'src/index.js')
}
```

- 多文件入口，多页面应用配置

```
const { resolve } = require('path')
module.exports = {
  entry:{
    test:resolve(__dirname,'src/index.js'),
    demo:resolve(__dirname,'src/demo.js')
  }
}
```

## output(出口)

- `output`基础配置项

  1. `path`(输出的位置，默认`dist`目录下)
  2. `filename`(输出文件的乳名，默认`main`),可以直接像写死，也可以文件名加hash值动态
  3. `pulibPath`(指定打包后的文件应该在哪里引用，一般用在生产环境,默认空)

- `webpack`哈希值
    1. hash (普通的hash)
    2. chunkhash (同一个chunk同一个hash)
    3. contenthash (一个文件一个hash)

- 代码

```
const { resolve } = require('path')
module.exports = {
  output:{
    path:resolve(__dirname,'dist'),
    filename:'bundle.js',
    // filename:'[name]_[hash].js'
    publicPath:'https://github.com'
  }
}
```

https://juejin.im/post/6883305742422507533#heading-14
