## 初始化一个新项目

```
yarn init
```

## 安装项目的全部依赖

```
yarn
// or yarn install
```

## 添加依赖包

```
yarn add [package]
yarn add [package]@[version]
yarn add [package]@[tag]
```

## 移除依赖包

```
yarn remove [package]
```

## 将依赖项添加到不同依赖项类别中

```
yarn add [package] --dev // yarn add [package] -D
yarn add [package] --peer
yarn add [package] --optional
```

## 查看 yarn 全局缓存包地址

```
yarn cache dir
```

## 清除全局缓存

```
yarn cache clean
```

## 升级依赖包

```
yarn upgrade [package]
yarn upgrade [package]@[version]
yarn upgrade [package]@[tag]
```

> 参考 [yarn 中文文档](https://yarn.bootcss.com/docs/usage/)、 [yarn 常用命令](https://www.jianshu.com/p/f5d85e541a99)
