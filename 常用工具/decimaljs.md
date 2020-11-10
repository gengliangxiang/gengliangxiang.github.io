# decimal.js

## 引入

```
import {Decimal} from 'decimal.js';
```

## 基本运算

```
// 加法
let add = new Decimal(a).add(new Decimal(b))
// or
let plus = new Decimal(a).plus(new Decimal(b))

// 减法
let sub = new Decimal(a).sub(new Decimal(b))
// or
let minus = new Decimal(a).minus(new Decimal(b))

// 乘法
let mul = new Decimal(a).mul(new Decimal(b))
// or
let times = new Decimal(a).times(new Decimal(b))

// 除法
let div = new Decimal(a).div(new Decimal(b))
// or
let dividedBy = new Decimal(a).dividedBy(new Decimal(b))

// 保留小数位
x = 3.456
y = new Decimal(x)
x.toFixed()                       // '3'
y.toFixed()                       // '3.456'
y.toFixed(0)                      // '3'
x.toFixed(2)                      // '3.46'
y.toFixed(2)                      // '3.46'
y.toFixed(2, Decimal.ROUND_DOWN)  // '3.45'
x.toFixed(5)                      // '3.45600'
y.toFixed(5)                      // '3.45600'
```

## 比较运算

```
// 相等比较
x = new Decimal(123.4567)
y = new Decimal('123456.7e-3')
x.equals(y)

// NaN 比较
x = new Decimal(NaN)
x.isNaN()

// 有限数比较
x = new Decimal(1)
x.isFinite()                             // true
y = new Decimal(Infinity)
y.isFinite()                             // false

```

## Math 内置方法实现

```
// 开平方
Decimal.sqrt('6.98372465832e+9823')      // '8.3568682281821340204e+4911'
// 指数幂
Decimal.pow(2, 0.0979843)
```

[参考 API](http://mikemcl.github.io/decimal.js/)
