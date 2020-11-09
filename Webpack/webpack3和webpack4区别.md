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

7.移除 loaders，必须使用 rules
- （在 3 版本的时候 loaders 和 rules 是共存的但是到 4 的时候只允许使用 rules）
