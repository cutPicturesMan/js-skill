### Array.prototype.slice和[].slice的区别

### undefined和void(0)的区别
`undefined`是全局对象的一个属性，即全局作用域的一个变量，初始值就是原始数据类型`undefined`。ES5标准规定`undefined`是一个只读属性，但是由于`undefined`不是保留字，在局部作用域中有可能被当作标识符（变量名）来使用，导致`undefined`的值和类型会被改变
```javascript
function foo() {
    var undefined = 'foo';
    console.log(undefined, typeof undefined);
}
// 'foo' 'string'
foo()
```

void运算符能够对给定的表达式进行求值，然后返回`undefined`。通常只用于获取undefined的原始值，一般使用void(0)（等同于void 0）