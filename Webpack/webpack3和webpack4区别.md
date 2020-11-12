# webpack3 和 webpack4 区别

### 1. mode

- webpack 增加了一个 mode 配置，只有两种值 development | production。对不同的环境他会启用不同的配置。
- webpack4 中通过内置的 mode 使用相应模式的内置优化。比如设置 mode 等于'development'，会将 process.env.NODE_ENV 的值设为 development。设置 mode 等于'production'，会将 process.env.NODE_ENV 的值设为 production。production 侧重于打包后的文件大小，development 侧重于构建

### 2. CommonsChunkPlugin

webpack.optimize.CommonsChunkPlugin 已经从 webpack4 中移除。可使用 optimization.splitChunks 进行模块划分（提取公用代码）。

但是需要注意一个问题，默认配置只会对异步请求的模块进行提取拆分，如果要对 entry 进行拆分，需要设置 optimization.splitChunks.chunks = 'all'。

对应之前我们拆分 runtime 的情况，现在也有一个配置 optimization.runtimeChunk，设置为 true 就会自动拆分 runtime 文件

```
module.exports = {
  optimization: {
    runtimeChunk: true,
    splitChunks: {
      vendors: {
        name:  'venders',
        chunks:  'all',
        minChunks: 2
    }
  }
}
```

### 3. mini-css-extract-plugin （CSS 文件提取）

webpack4，删除原 extract-text-webpack-plugin 配置，增加 mini-css-extract-plugin 配置
注意：mini-css-extract-plugin 的 filename 选项不支持函数

```
module.exports = {
  plugins: [
    new  MiniCssExtractPlugin({
      filename:  'css/[name].css'
    }),
  ],
}

module.exports = {
  module: {
    rules: [
      {
        test:/\.vue$/,
        loader: 'vue-loader',
      },
      { test: /\.css$/,
         use: [
                  {
                    loader: MiniCssExtractPlugin.loader,
                    options: {
                      publicPath: '../',
                      hmr: process.env.NODE_ENV === 'development',
                    },
                  },
                  'css-loader',
                ],
        },
    ]
  }
}
```

### 4. 新版 babel

新版 babel 使用新的命名空间 @babel

- @babel/core
- @babel/plugin-proposal-class-properties
- @babel/plugin-proposal-decorators
- @babel/plugin-syntax-dynamic-import
- @babel/plugin-transform-runtime
- @babel/preset-env
- @babel/runtime
- babel-loader
- @babel/polyfill

```
//.babelrc
{
  "presets": [
    [
      "@babel/preset-env",
      {
        "modules": false,
        "targets": {
          "browsers": [
            "> 1%",
            "last 2 versions",
            "ie >= 11"
          ]
        },
        "useBuiltIns": "usage" // 按需引入 polyfill
      }
    ]
  ],
  "plugins": [
    "@babel/plugin-transform-runtime",
    "@babel/plugin-syntax-dynamic-import",
    ["@babel/plugin-proposal-class-properties", { "loose": false }],
    ["@babel/plugin-proposal-decorators", { "legacy": true }],
  ]
}
```

### 5. vue-loader

vue-loader 15 注意要配合一个 webpack 插件才能正确使用

```
const { VueLoaderPlugin } = require('vue-loader')

module.exports = {
  plugins: [ new VueLoaderPlugin() ]
}
```

### 5. UglifyJsPlugin

现在也不需要使用这个 plugin 了，只需要使用 optimization.minimize 为 true 就行，production mode 下面自动为 true
optimization.minimizer 可以配置你自己的压缩程序

```
module.exports = {
  optimization: {
    minimizer: [
      new TerserPlugin({ // 压缩js
          cache:  true,
          parallel:  true  //开启多线程
        }
      }),
      new OptimizeCSSAssetsPlugin({ // 压缩css
        cssProcessorOptions: {
          safe: true
        }
      })
    ]
  }
}
```

### 7. 移除 loaders，必须使用 rules

- （在 3 版本的时候 loaders 和 rules 是共存的但是到 4 的时候只允许使用 rules）

### 8. 支持 es6 的方式导入 JSON 文件，并且可以过滤无用的代码

```
let jsonData = require('./data.json')
import jsonData from './data.json'
import { first } from './data.json' // 打包时只会把first相关的打进去
```

```
{
  test: /\.json$/,  //用于匹配loaders所处理文件拓展名的正则表达式
  use: 'json-loader', //具体loader的名称
  type: 'javascript/auto',
  exclude: /node_modules/
}
```

### 9. 升级 happypack 插件（happypack 可以进行多线程加速打包）

运行在 node.js 之上的 webpack 时单线程模型，也就是只能一个一个文件进行处理，不能并行处理，happypack 可以将任务分解给多个子进程，最后将结果发给主进程，js 是单线程模型，只能通过这种多线程的方式提高性能
vue-loader 不支持 HappyPack，官方建议用 thread-loader

```
const HappyPack = require('happypack');

exports.module = {
  rules: [
    {
      test: /.js$/,
      use: ['happypack/loader?id=babel'],// 将对.js文件的处理转交给id为babel的HappyPack的实列
      exclude:/node_modules/
    }
  ]
};

exports.plugins = [
  new HappyPack({
    id: 'babel',// 用唯一的标识符id来代表当前的HappyPack 处理一类特定的文件
    loaders: [ 'babel-loader' ] // 如何处理.js文件，用法和Loader配置是一样的
  })
];
```

[参考](https://www.cnblogs.com/Super-scarlett/p/11085363.html)
