## html5新增的API
除了常用的获取元素的querySelector和querySelectorAll,还有操作类的几个API

```javascript
Node.classList.add('class') //添加class
Node.classList.remove('class') //移除class
Node.classList.toggle('class') //切换class，有则移除，无则添加
Node.classList.contains('class') //检测是否存在class复制代码
```


## 属性
- childNodes
- nodeType
    - 仅有3种有实用价值
    - 元素节点 nodeType=1
    - 属性节点 nodeType=2
    - 文本节点 nodeType=3
- nodeValue
    - 元素节点的nodeValue为null
    - 文本节点时才有用
- firstChild
- lastChild


## window.onload
html文档被加载到浏览器窗口里，加载完后会调用window的onload方法


## 动态创建标签
```javascript
createElement() //创建元素
appendChild() //添加元素
parentNode.insertBefore(newEle,targetEle) //添加元素 这里需要注意:必须是目标元素的parentNode
```

## 样式
- style属性

element.style是一个对象，里面有自己的原型指向，所以不能element.style = {xx:xx}指向一个新对象，只能通过element.style.xx = 'xx'设置，和通过element.style.xx获取
> element.style获取和设置的都是行内样式，只能一个一个设置和一个一个获取,打印element.style会得到一个超多属性的CSSStyleDeclaration对象，并不仅仅是你设置过了的那几个

- className

虽然可以通过element.setAtrribute('class','xx')来设置样式<br>
更简便的方法是element.className来设置和获取
> 如果你有自己的样式库或者使用bootstrap等会非常方便，比如只要element.className = 'bg-red'
