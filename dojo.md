# dojo API

## dojo.byId

这个类似于`document.getElementById`,但是 dojo.byId 消除了浏览器之间的兼容问题[隔离浏览器不一致的行为]
如果dojo.byId会在多个元素具有相同id值的情况下返回第一个元素。

## dojo.connect

通过`dojo.connect`为节点添加UI事件。工具箱中添加和移除此类事件的重要机制。

```js
var handle = dojo.connect(dojo.byId(), 'onmouseover', null, function(e){console.log(e)})
```

## dojo.disconnect

切断执行函数与相关DOM事件之间的联系

```js
dojo.disconnect(handle);
```

## dojo.query

通过css3风格的语法来实现快速查询

```javascript
dojo.query('div')

dojo.query('div#d2')

dojo.query('.blue')
```

## dojo.addClass

给元素添加class属性

```javascript
dojo.addClass('s1','blue')
```


## dojo.setObject

组织命名空间

```javascript
dojo.setObject(/* String */ object, /* Any */ value, /* Object * / context)

/*
	第一个参数是会自动创建的对象层次，第二个参数是一个映射到该层次的值
*/

```

```javascript
var foo = {bar:{baz:{qux:1}}}
console.log(foo.bar.baz.qux)

dojo.setObject('foo.bar.baz.qux',1)

console.log(foo.bar.baz.qux)

var someObject = {}

dojo.setObject('foo.bar.baz.qux',1,someObject)

console.log(someObject.foo.bar.baz.qux)
```


















