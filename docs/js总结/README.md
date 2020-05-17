## 引擎
浏览器内核分成两部分：渲染引擎和JS引擎。<br>
chrome的渲染引擎是webkit，js引擎是v8<br>
safari的渲染引擎也是webkit，但是js引擎不是v8<br>
firefox的渲染引擎是gecko<br>
IE的渲染引擎是Trident

## 
## isNaN的检测机制
这里指window.isNaN，Number.isNaN()没有这个机制<br>
- 先检测是否为数字类型，如果不是，会默认转换为数字类型Number()
- Number()方法遇到`引用类型`时,先toString()转换为字符串，然后再把字符串Number()转换为数字类型

```javascript
Number('13') //13
Number('13px') //NaN
Number(true) //1
Number(false) //0
Number(null) //0  
Number(undefined) //NaN
Number('') //0   
Number('  ') //0   //这个需要注意的

Number([12]) // -> '12' -> 12
Number([12,13]) // -> '12,13' -> NaN
Number([]) // -> '' -> 0
Number({}) // -> '[object object]' -> NaN 

isNaN(NaN) // true
isNaN(null) // false   
isNaN(undefined) // true
isNaN({}) // true
isNaN('12') // false
isNaN('a') // true
isNaN('') // false 
isNaN([12]) // fasle  
isNaN([12,13]) // true 
isNaN([]) // false 
```

## 
## 堆栈内存
- 基本数据类型的值会存储在当前作用域下(栈内存)
- 引用数据类型会在堆中新开辟一块内存(堆内存)
    - 对象存储的是键值对
    - 函数存储的是代码字符串，函数执行，首先会形成一个私有的作用域(栈内存)，把之前在堆内存中存储的字符串复制一份过来，在执行
    - 函数如果没有return，`那返回的默认是undefined`
    - 如果只写了return，`默认也是undefined`

```javascript
var obj = {
    n: 10,
    m: obj.n * 10
}
console.log(obj.m) 
// 先开辟堆内存，此时obj还是undefined
// 所以会报错
```

## 
## 盲点
数学运算除了+ 其他的都会先将'3px'用Number()方法转换为数字再进行运算

```javascript
'3px'/3  //NaN
'3px'*3  //NaN
'3px'-3  //NaN
Number('3px') -> NaN
//因为+ 还有字符串拼接
//所以如果+ 遇到了字符串。就为字符串拼接
// + 运算的时候，只要出现字符串就是字符串拼接
1 + true  // 2
1+ 'true' // '1true'
[12]+10 // '1210'  //这个需要注意的
// 虽然没看见字符串，但是引用类型转换为数字，首先会转换为字符串，所以变为了字符串拼接
```

==比较
```javascript
2 == true //false 
null == undefined // true
null === undefined // false
null == 0 // fasle
NaN 和谁都不相等
```
> null在做相等判断时，不进行转型，所以null和0为不同类型数据，结果为false

null，undefined内存问题
```javascript
var total = 0; //0是有值的，会在栈中占一个位置
var total = null  //这样不占位置
var total;  //undefined也占内存的
```



