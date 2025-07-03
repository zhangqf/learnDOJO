# DOJO

## 类型检查

- isArray
- isString
- isFunction
- isObject
- isArrayLike
	如果value时Array类型，但又允许存在一些例外情况则返回true。如：Function中的内置的arguments对象。因为arguments不支持push这样的内置方法。可以说是类数组
- isAline
	如果value是一个内置的函数或者是ActiveX组件之类的本地函数，但又不能通过像instanceof Function 这样的常规检查来确认，返回true

## 鸭子类型

## 字符串工具

- dojo.string.trim
- dojo.string.pad
- dojo.string.substitute

## 数组处理


### 查找元素位置

`dojo.indexOf` 和 `dojo.lastIndexOf`,这俩个方法在元素存在的情况下都会返回表示该元素索引的整数值。如果元素不存在则返回-1	。它们的方法签名都包含一个可选参数，用于表示从数组开头或末尾算起的起点位置。

```js
dojo.indexOf(/*Array*/ array, /*Any*/ value, /*Integer?*/ fromIndex ) // 返回整数值

dojo.lastIndexof(/*Array*/ array, /*Any*/ value, /*Integer?*/ fromIndex） // 返回整数值
```

### 根据条件测试元素

dojo.every
dojo.some

### 迭代操作元素
forEach

### 转换元素

map和filter与forEach的方法签名相同，但从对每个元素应用自定义逻辑以及返回另外一个数字并且不会修改原始数组。

## 通过模块管理源代码

dojo.provide 
dojo.require

当需要把一个文件作为dojo.require语句可以导入的模块或资源时，应该将dojo.provide语句放在该文件中的第一行。不过，dojo.require也不仅仅是一个类似script标签的占位符，它还负责将模块映射到磁盘上的特定位置，取得其中的代码并缓存以前请求过的模块和资源。




## JavaScript对象实用程序

mixin extend clone


### 对象混入

`mixin` 可以接受任意数量的对象作为参数，其中第一个对象将作为混入了其他对象的结果返回。只能用于对象实例。

```js
dojo.mixin(/* Object * / o, /* Object */ o, ...) // 返回对象
```

### 扩展对象原型

`extend` 将混入的所有属性和方法都添加到构造函数的原型中。这样，所有基于该构造函数创建的对象实例都将自动包含混入的新属性和方法。


```js
dojo.extend(/* Function */ constructor, /* Object */ props, ...)  // 返回Function
```

### 克隆对象

`clone`基于对象层次的深复制。

### 部分应用参数

`dojo.partial`根据参数的可用情况为函数部分地应用参数，然后在将来某个时刻再最终执行该函数。

```js
dojo.partial(/* Function | String */ func, /* arg1,...argN */) // 返回应用参数后的函数
```

```js
function addThree(x,y,z){console.log(x+y+z)}


f = dojo.partial(addThree, 1,2)
f = dojo.partial(f,3)
f() // 6
```

### 把对象连接到特定的环境

`dojo.hitch`可以将函数永久地绑定到特定的执行环境中【类是与改变this的指向】。无论最终的指向环境变成什么。这种方法对于无法预知最终执行环境的情况下，确保执行回调函数特别有用

```js
dojo.hitch(/* Object */ scope, /* Function || String */ method /*, arg1,...argN */)
```

```js
var foo = {
	name: 'Foo',
	greet:function(){
		console.log('Hi, I`m', this.name)
	}
}
var bar = {
	name: 'Bar',
	greet:function(){
		console.log('Hi, I`m', this.name)
	}
}

foo.greet() // Hi, I`m Foo
bar.greet() // Hi, I`m Bar

bar.greet = dojo.hitch(foo, 'greet')
bar.greet() // Hi, I`m Foo



bar.greet = foo.greet

bar.greet() // Hi, I`m Bar

```



## 委托和继承

委托：一个对象可以通过其他对象执行某种操作，

```js
dojo.delegate(/*Object*/ delegate, properties) // 返回对象
```


```js

function Foo() {
    this.talk = function(){console.log("Hello, my name is", this.name)}
}
var bar = dojo.delegate(new Foo, {name: 'Bar'})
bar.talk() // Hello, my name is Bar
```


## DOM实用程序

### 判断祖先

`isDescendant` 该方法接受两个值，第一个参数表示要判定的相关节点，第二个参数是可能的祖先节点。如果判定的节点是可能的祖先节点的后代，该方法返回true

```js
dojo.isDescendant(/*String|DomNode*/ node, /* String ｜DomNode */ potentialAncestor)
```

### 设置可选择性

```js
dojo.setSelectable(/*String | DomNode */ node, /*Boolean*/ selectable)
```

### 为节点添加样式

```js
dojo.style('foo', 'height') // 返回 foo 的 height值
dojo.style('foo', 'height', '100px')
dojo.style('foo', {
	height:'100px'
})
```


`dojo.style`
`dojo.addClass`
`dojo.removeClass`
`dojo.hasClass`
`dojo.toggleClass`



### 操作属性

`dojo.attr`
`dojo.hasAttr`
`dojo.removeAttr`


### 放置节点

`dojo.place(/*String | DomNode */ node, /*String|DomNode */ refNode, /*String|Number*/ position)`

第一个参数表示要放置的节点，
第二个参数是参照节点，
第三个参数是说明相对位置关系的字符串或数字值。可以是before after first 和 last



### 盒模型


`dojo.boxModel`属性 可能的值为`content-box` 或者 `margin-box` 和 dojo.marginBox、dojo.contentBox方法。

与盒模型有关的方法

`dojo.marginBox(/*DomNode|Sting*/ node, /*Object?*/ box)`
`dojo.contentBox(/*DomNode | String */ node, /*Object*/ box)`
`dojo.coords(/*HTMLElement */ node, /*Boolean*/ includeScroll)`



## 浏览器实用程序

### cookie

`dojo.cookie(/*String*/ name, /*String*/ value, /*Object?*/ properties)`

- 只传一个参数，表示 cookie值的名称，作为getter返回相应的值
- 只传两个参数，作为setter，设置cookie的值。
- 第三个参数properties，包含下列键/值对：`expires (Date|String|Number)`,如果是数字值，表示从今天起cookie失效的天数；如果是日期值，表示cookie失效的日期，如果省略expires或该值为零，那么cookie在浏览器关闭时失效。path（String）有权使用cookie的路径 domain（String）有权使用cookie的域 secure（Boolean）是否只在安全连接的情况下发送cookie。


`dojo.cookie.isSupported()` 浏览器是否支持cookie


### 后退按钮的处理


`init()`
`setInitialState(/*Object*/ args)`
`addToHistory(/*Object*/ args)`


















