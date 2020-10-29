# JavaScript 继承

## 1. 一般模式

```
var baseObj = {
    sayHello: function() {
        console.log("Hello, I'm JK!");
    },
};
var Person = function() {
    this.name = 'tom';
};
Person.prototype = baseObj;
var subObj = new Person();
```

## 2. 原型式继承

```
function object(o) {
    function F() {}
    F.prototype = o;
    return new F();
}
```

## 3. 借用构造函数继承

```
function BaseType() {
    this.name = 'tom';
}
function SubType() {
    BaseType.call(this);
    this.age = 19;
}
```

## 4. 组合式继承

```
function BaseType(name) {
    this.name = name;
}
BaseType.prototype.sayHello = function() {
    console.log('Hello, 我是 ' + this.name);
};
function SubType(name, age) {
    BaseType.call(this, name); // 继承属性 this.age = age;
}
SubType.prototype = new BaseType(); // 继承方法
```

## 5. 寄生式继承

```
function createObject(baseObj) {
    var temp = object(baseObj);
    temp.sayHello = function() {
        console.log("hello, I'm Tom");
    };
    return temp;
}
```

## 6. 寄生组合式继承

```
function SuperType(name) {
    this.name = name;
    this.colors = ['red', 'blue', 'green'];
}
SuperType.prototype.getName = function () {
    return this.name;
}

function SuberType(name, age) {
    SuperType.call(this, name);
    this.age = age;
}
//寄生组合式继承
SuberType.prototype = Object.create(SuperType.prototype);
SuberType.prototype.constructor = SuberType;

SuberType.prototype.getAge = function () {
    return this.age;
}

let girl = new SuberType('Yvette', 18);
girl.getName()

```
