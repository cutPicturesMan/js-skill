### Array.prototype.slice和[].slice的区别
#### 1、[].slice运行更快
近5年以来，截止至2018年，即时编译器(JITs)已经包含在除了IE8之外运行js的各种地方。得益于这种机制，`[].slice`并没有实例化一个空数组，而是直接访问`slice`属性

#### 2、Array.prototype.slice有可能失败
当`Array`被重新定义之后，`Array.prototype.slice`

### undefined和void(0)的区别
#### 1、可改变的undefined变量
`undefined`是全局对象的一个属性，即全局作用域的一个变量，初始值就是原始数据类型`undefined`。ES5标准规定`undefined`是一个只读属性，但是由于`undefined`不是保留字，在局部作用域中有可能被当作标识符（变量名）来使用，导致`undefined`的值和类型会被改变。
```javascript
function foo() {
    var undefined = 'foo';
    console.log(undefined, typeof undefined);
}
// 'foo' 'string'
foo()
```

void运算符能够对给定的表达式进行求值，然后返回`undefined`。通常只用于获取undefined的原始值，一般使用void(0)（等同于void 0）
```javascript
function fn(err){
    if (err) {
        // 当走到此流程中时，由于不知道next()的返回值是多少，这里会return什么类型的值无从得知
        return next(err)
    }
}

function fn(err){
    if (err) {
        // 写法1，return undefined
        next(err)
        return
        // 写法2，void执行next(err)后返回undefined
        // return void next(err)
    }
}
```

#### 2、立即执行函数的另一种写法
`void`可以直接将`function`关键字作为表达式代替函数声明，并且通过`()`立即执行，达到跟立即执行函数一样的效果
```javascript
// 立即执行函数
(function iife() {
    console.log(1);
})()
// 等同于上式立即执行函数
void function iife() {
    console.log(1);
}()
```

#### 何时使用void？
`void`在某些时刻可以减少代码量，但是会让之前没有听说过`void`关键字的人更难阅读和理解。建议仅用在获取`undefined`的原始值上。


优化：
1、for key in obj -> Object.key(obj)之后使用for循环
【解析】这样做在v8引擎中会提升性能。如果一个对象在内部表示为哈希映射，JIT编译器有可能会拒绝优化包含for-in循环的函数，