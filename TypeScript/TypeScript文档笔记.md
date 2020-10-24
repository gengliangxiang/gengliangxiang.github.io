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

1. `Boolean`、`String`、 `Number`构造函数创造的是对应类型的对象，不是一个基本值，例如，`new Boolean()`返回的就是一个 `Boolean` 对象
2. 直接调用 `Boolean` 返回的是一个 boolean 类型，其他同理
3. 声明一个 `void` 类型的变量没有什么用，因为你只能将它赋值为 `undefined` 和 `null`

## interface 和 type

### interface

#### 接口定义

- 使用`interface` 关键字来定义

```
interface LabelledValue {
  label: string;
}
```

#### 可选属性

- 带有可选属性的接口与普通的接口定义差不多，只是在可选属性名字定义的后面加一个`?`符号

```
interface SquareConfig {
  color?: string;
  width?: number;
}
```

#### 只读属性

- 属性名前用`readonly`来指定只读属性

```
interface Point {
    readonly x: number;
    readonly y: number;
}
```

#### 函数类型

- 使用接口表示函数类型,需要给接口定义一个调用签名,一个只有参数列表和返回值类型的函数定义。参数列表里的每个参数都需要名字和类型

```
interface Point {
    readonly x: number;
    readonly y: number;
}
```

#### 可索引的类型

- 可索引类型具有一个 索引签名，它描述了对象索引的类型，还有相应的索引返回值类型

```
interface StringArray {
  [index: number]: string;
}

let myArray: StringArray;
myArray = ["Bob", "Fred"];

let myStr: string = myArray[0];
```

#### 接口的实现

- 使用`implements`关键字,并且一个类可以实现多个接口

```
interface ClockInterface {
    currentTime: Date;
}

class Clock implements ClockInterface {
    currentTime: Date;
    constructor(h: number, m: number) { }
}
```

#### 接口的集成

- 使用`extends`关键字,一个接口可以继承多个接口，创建出多个接口的合成接口。接口也可以继承类

```
interface Shape {
    color: string;
}

interface PenStroke {
    penWidth: number;
}

interface Square extends Shape, PenStroke {
    sideLength: number;
}
// 继承类
class Control {
    private state: any;
}

interface SelectableControl extends Control {
    select(): void;
}
```
