# TypeScript 文档笔记

## 基础类型

### 基础类型定义

```
let isDone: boolean = false;
let num: number = 6;
let notANumber: number = NaN;
let myName: string = 'Tom';
let sentence: string = `Hello, my name is ${ myName }`.
let u: undefined = undefined;
let n: null = null;
let unusable: void = undefined;
```
1. `Boolean`、`String`、 `Number`、`Undefined`、`Null`构造函数创造的是对应类型的对象，不是一个基本值，例如，`new Boolean()`返回的就是一个 `Boolean` 对象
2. 直接调用 `Boolean` 返回的是一个boolean 类型，其他同理
3. 声明一个 `void` 类型的变量没有什么用，因为你只能将它赋值为 `undefined` 和 `null`
