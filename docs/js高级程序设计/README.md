## defer与async的区别
默认情况下，浏览器是同步加载 JavaScript 脚本，即渲染引擎遇到`<script>`标签就会停下来，等到执行完脚本，再继续向下渲染。如果是外部脚本，还必须加入脚本下载的时间。

如果脚本体积很大，下载和执行的时间就会很长，因此造成浏览器堵塞，用户会感觉到浏览器“卡死”了，没有任何响应。这显然是很不好的体验，所以浏览器允许脚本异步加载

script标签打开`defer`或`async`属性，脚本就会异步加载。渲染引擎遇到这一行命令，就会开始下载外部脚本，但不会等它下载和执行，而是直接执行后面的命令。



defer与async的区别是：defer要等到整个页面在内存中正常渲染结束（DOM 结构完全生成，以及其他脚本执行完成），才会执行；async一旦下载完，渲染引擎就会中断渲染，执行这个脚本以后，再继续渲染。一句话，defer是“渲染完再执行”，async是“下载完就执行”。
如果同时指定了两个属性，则会遵从`async`属性而忽略`defer`属性。
> 如果有多个defer脚本，会按照它们在页面出现的顺序加载，而多个async脚本是不能保证加载顺序的。

![gJ2rOzVm3tu8ybK](https://i.loli.net/2020/05/13/gJ2rOzVm3tu8ybK.png)

## 
## 5个false
- ''
- 0
- null
- undefined
- NaN

> "''"   为真

## 
## NaN
NaN与任何值都不想等，包括NaN本身
```javascript
alert(isNaN(NaN)) //true
alert(isNaN(10)) //false
alert(isNaN('10')) //false  
alert(isNaN('blue')) //true
alert(isNaN(true)) //flase
```
> 任何涉及NaN的操作都会返回NaN，但是NaN +'test' = 'NaNtest' 因为 + 除了运算还有一个字符串拼接的作用<br>
> window的isNaN方法 会对非数字类型做一个数字类型的转换<br>
> Number.isNaN不会做类型转换


## 
## 数值转换的3个方法
- Number()
- parseInt()
- parseFloat()
![](https://i.loli.net/2020/04/23/7Cx6jZE9QNhpa3k.png)
> Number('')  // 0

## 
## 转换为字符串的2个方法
- toString()
- String()
几乎每个值都有toString()方法，但是null和undefined没有, `NaN有哦`
```javascript
var age = 11;
var found = true;
age.toString() //'11'
found.toString() //'true'
```
那null和undefined咋办
使用String()方法
```javascript
String(null) //'null'
```
里面也是用的toString()方法，只不过先判断了是不是null和undefined

## 
js中不允许直接访问内存中的位置，也就是说不能直接操作对象的内存空间。在操作对象时，实际上是在操作对象的引用而不是实际的对象。所以js中没有获取对象地址的方法

## 
## typeof 和 instanceof
检测基本数据类型的最佳工具是使用typeof
```javascript
// 2个需要注意的
typeof null // object
typeof fn  // function
```
引用类型的最好工具是 instanceof ，会在原型链上查找
> 但是instanceof检测基本类型的值，始终返回false，因为基本类型不是对象

## 
## 检测数组
instanceof 和 Array.isArray()都可以检测数组
但是instanceof的问题在于，它假定只有一个全局执行环境。如果网页中包含多个框架，那实际上就存在两个以上不同的全局执行环境，从而存在两个以上不同版本的Array构造函数。<br>
Array.isArray()是为了解决上面问题新增的方法

## 
## 闭包
闭包是指有权访问另一个 函数作用域中的变量的函数。 

## 
## window对象
```javascript
window.open(url) //默认会新开一个窗口<br>
window.open(url,'_self')  //打开url，效果和location.href一样
```

## 
## location对象
location中有许多属性,这些属性都是可读可写的，除了hash属性，其他属性重新写入，都会刷新<br>
![](https://i.loli.net/2020/04/24/SFNHJCtk3qa5EKb.png)
```javascript
location.assign('url'); //跳转到url
location.href本质也是调用上面这个方法
location.relplace(url)  //不会产生历史记录
location.reload()  //重新加载(有可能从缓存中加载)<br>
location.reload(true); //重新加载(从服务器重新加载)
```

## 
## Navigator对象
![](https://i.loli.net/2020/04/24/rU8E3itD1LguYf4.png)
![](https://i.loli.net/2020/04/24/YwdVZ4D5aWsCjmy.png)

## 
## history对象
```javascript
history.go(-1); 
history.go(1); 
history.back(); 
history.forward(); 
```

## 
## ajax
必须在调用 open()之前指定 onreadystatechange 事件处理程序才能确保跨浏览器兼容性。
```javascript
var xhr = createXHR();
xhr.onreadystatechange = function () {
    if (xhr.readyState == 4) {
        if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304) {
            alert(xhr.responseText);
        } else {
            alert("Request was unsuccessful: " + xhr.status);
        }
    }
};
xhr.open("get", "example.txt", true);
xhr.send(null);
```
