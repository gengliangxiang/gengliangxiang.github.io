# require 与 import

require 和 import 分别是不同模块化规范下引入模块的语句

## 遵循规范

- require/exports 是遵循 CommonJS 规范
- import/export 是 ES6 规范

## require/exports 是运行时动态加载，import/export 是静态编译

> CommonJS 加载的是一个对象（即 module.exports 属性），该对象只有在脚本运行完才会生成。而 ES6 模块不是对象，它的对外接口只是一种静态定义，在代码静态解析阶段就会生成

## require/exports 输出的是一个值的拷贝，import/export 模块输出的是值的引用

> require/exports 输出的是值的拷贝。也就是说，一旦输出一个值，模块内部的变化就影响不到这个值。

> import/export 模块输出的是值的引用。JS 引擎对脚本静态分析的时候，遇到模块加载命令 import，就会生成一个只读引用。等到脚本真正执行时，再根据这个只读引用，到被加载的那个模块里面去取值。

> 若文件引用的模块值改变，require 引入的模块值不会改变，而 import 引入的模块值会改变。

## 用法

- require/exports 的用法

```
const fs = require('fs')
exports.fs = fs
module.exports = fs
```

exports 是对 module.exports 的引用，相当于

```
exports = module.exports = {};
```

在不改变 exports 指向的情况下，使用 exports 和 module.exports 没有区别；如果将 exports 指向了其他对象，exports 改变不会改变模块输出值。示例如下：

```
//utils.js
let a = 100;

exports.a = 200;
console.log(module.exports) //{a : 200}
exports = {a:300}; //exports 指向其他内存区

//test.js

var a = require('./utils');
console.log(a) // 打印为 {a : 200}
```

- import/export 的写法

```
import {readFile} from 'fs' //从 fs 导入 readFile 模块
import {default as fs} from 'fs' //从 fs 中导入使用 export default 导出的模块
import * as fileSystem from 'fs' //从 fs 导入所有模块，引用对象名为 fileSystem
import {readFile as read} from 'fs' //从 fs 导入 readFile 模块，引用对象名为 read
import('/modules/my-module.js') //动态导入
  .then((module) => {
    // Do something with the module.
});

export default fs
export const fs
export function readFile
export {readFile, read}
export * from 'fs'
```

## ES6 模块可以在 import 引用语句前使用模块，CommonJS 则需要先引用后使用

- ES6 模块

```
//webUtils.js
export var e='export';
console.log(e) //export
  import {e} from './webUtils.js';
  console.log(e) //export
```

- CommonJS

```
//utils.js
exports.e = 'export';
console.log(a) // ReferenceError: a is not defined
a = require('./utils');
console.log(a)
```
