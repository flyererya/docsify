## setTimeout()注意点
setTimeout()并不是把你的回调事件放在事件循环队列中，而是定时器到时后，环境会把你的回掉函数放在事件循环队列中

## 
如果你引用了一个当前作用域中不存在的变量，并不会像对象属性一样返回 undefined，而是会抛出一个ReferenceError异常:
```javascript
var myObject = { 
    a: undefined
};
myObject.a; // undefined 
myObject.b; // undefined 
```

## 
## in 和 hasOwnProperty()的区别
- in会在原型链中查找
- hasOwnProperty()只会检查属性是否在当前对象中
```javascript
var myObject = {
     a:2
};
("a" in myObject); // true 
("b" in myObject); // false
myObject.hasOwnProperty( "a" ); // true 
myObject.hasOwnProperty( "b" ); // false
```

## 
## for of 和 for in 以及 forEach()
for of 和 forEach() 都用来遍历数组
```javascript
var myArray = [ 1, 2, 3 ];
for (var v of myArray) { 
    console.log( v );
}
// 1 2 3
```
for in 通常用来遍历对象,但遍历项是key
```javascript
var myObj = {
    a: 1,
    b: 2
}
for (var key in myObj) { 
    console.log( key );
}
//  "a"  "b"
```
需要注意的是，for in `会遍历原型链`
```javascript
var triangle = {a: 1, b: 2, c: 3};

function ColoredTriangle() {
  this.color = 'red';
}

ColoredTriangle.prototype = triangle;

var obj = new ColoredTriangle();

for (var prop in obj) {
  if (obj.hasOwnProperty(prop)) {  //只遍历当前对象
    console.log(`obj.${prop} = ${obj[prop]}`);
  } 
}
// "obj.color = red"
```
> for in 也可以用来遍历数组，但遍历项是数组的index，不如直接用for in 或者forEach就好了

## 
## Object.create() 
- 参数是一个对象，返回一个空对象，但这个空对象的prototype指向objA
```javascript
var objB = Object.create(objA);
```


## 
## 将类数组转化为数组
```javascript
var arr = Array.from( arguments );
```


## 
```javascript
"''"  // true
```


## 
## typeof
- 对于没有声明的变量，typeof返回"undefined"
```javascript
var a;
typeof a; // "undefined" 
typeof b; // "undefined"
```
```javascript
typeof a !=="undefined"
//说明a被声明且除了是undefined的任何一种类型
```
```javascript
typeof NaN //'number' //书上的解释是：本来准备存一个数字的，结果不是数字
```

## 
## window.isNaN() 和 Number.isNaN()
Number.isNaN()是ES6才出的，解决了isNaN()的判断问题
```javascript
var  a = 2 / "foo";
var b = "foo";

isNaN(a) //true
isNaN(b) //true

Number.isNaN(a) //true
Number.isNaN(b) //false
```

## 
## 将非数字值当作数字来使用时
- true 转换为 1
- false 转换为 0
- undefined 转换为 NaN
- null 转换为 0
- '' 转换为0

## 
## null和undefined之间的相等比较
在==中null和undefined想等(它们也与自身相等)
```javascript
var a = null;
var b;
a == b //true
a == null //true
b == null //true

a == false //false
b == false //false
```

## 
## 其他类型==比较
类型不一样都会换成数字进行比较
```javascript
var a = 42;
var b = "42";
a ==b  //true

var a = "42";
var b = true;
a == b //false
```

## 
## 日期对象
```javascript
var d = new Date()
+d //返回结果为时间戳
var d = +new Date() //时间戳
var d = +new Date // 不传参时()可省
var d = new Date().getTime() // 时间戳
var d = Date.now() // 时间戳 //静态方法
```

## 
## es6新增的一些常用方法
```javascript
Object.assign(..) // 就是混入
Object.assign(target,obj1,obj2,...) // 就是混入 target是一个对象
              
"foo".repeat( 3 ); // "foofoofoo"

//字符串的三个方法
startsWith(..)、endsWidth(..) 和 includes(..)。

Array.prototype.includes() 数组也有这个方法
```