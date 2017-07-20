## 1、概述
我们开发过程中，最常用到的就是`jQuery`了，它为我们提供了大量的操作dom的方法，但是有时候我们任然需要扩展一些项目中需要的方法，这时候，我们就可以使用`jQuery`提供的`extend`方法来扩展`jQuery`对象。
```javascript
$.extend({
    myFn: function () {
        console.log('这是原型扩展', this);
    }
});
$.fn.extend({
    myFn: function () {
        console.log('这是实例扩展', this);
    }
});
```
这样，就分别给`jQuery`原型和实例都扩展了一个`myFn`方法，但是！你有没有想过，假如`jQuery`本来就有`myFn`这个方法呢？假如你的同事也给`jQuery`扩展了`myFn`呢？怎么办？


所以ES6引入了一种新的原始数据类型`Symbol`，表示独一无二的值。他是js的第七种数据类型。

`Symbol`通过`Symbol`函数生成。
```javascript
let s = Symbol();
typeof s; // symbol
s; // Symbol();
```
可以添加参数，便于区分。
```javascript
let s = Symbol('s');
s; // Symbol(s);
```

`Symbol`值可以转换为`字符串`和`布尔值`，但是不能于其它类型的值进行计算，否则会报。
## 2、作为属性名的Symbol
```javascript
var mySymbol = Symbol();

var a= {};
a[mySymbol] = 'Hello!';

var a = {
    [mySymbol]: 'Hello!'
};

var a {
    [mySymbol](arg) {}
};

var a = {};
Object.defineProperty(a, mySymbol, { value: 'Hello!' });
```
获取的时候，必须使用`[]`来获取
```javascript
a.mySymbol; // undefined
a[mySymbol]; // Hello!
```

## 3、实例：消除魔术字符串
```javascript
function getArea(shape, options) {
	var area = 0;
	switch (shape) {
		case 'Triangle': // 魔术字符串
			area = .5 * options.width + options.height;
			break;
	}
	return area;
}

getArea('Triangle', { width: 100, height100 });
```
传统方法通过定义变量来消除魔术字符串
```javascript
var shapeType = {
	triangle: 'triangle'
};

function getArea(shape, options) {
	var area = 0;
	switch (shape) {
		case shapeType.triangle:
			area = .5 * options.width + options.height;
			break;
	}
	return area;
}

getArea(shapeType.triangle, { width: 100, height100 });
```
直接用`Symbol()`,确保`shapeType.triangle`值不冲突
```javascript
const shapeType = {
	triangle: Symbol()
};

function getArea(shape, options) {
	var area = 0;
	switch (shape) {
		case shapeType.triangle:
			area = .5 * options.width + options.height;
			break;
	}
	return area;
}

getArea(shapeType.triangle, { width: 100, height100 });
```
## 4、属性名的遍历
`for...in`、`for...of`无法遍历到属性名为`Symbol`的值，`Object.keys()`、`Object.getOwnPropertyNames()`、`JSON.stringify()`也无法返回。但是，它也不是私有属性，有一个`Object.getOwnPropertySymbols`方法可以获取指定回想的所有`Symbol`属性名。

`Object.getOwnPropertySymbols`返回的是一个数组，成员是当前对象所有用作属性名的`Symbol`值。
```javascript
var obj = {};
var a = Symbol('a');
var b = Symbol('b');

obj[a] = 'Hello';
obj[b] = 'World';
var objectSymbol = Object.getOwnPropertySymbols(obj);

objectSymbol; // [ Symbol(a), Symbol(b) ]
```
`Reflect.ownKeys`可以返回对象的所有类型的键名
```javascript
var obj = {
    [Symbol('my_key')]: 1,
    enum: 2,
    nonEnum: 3
};
Reflect.ownKeys(obj); // ['enum', 'nonEnum', Symbol('my_key')]
```
## 5、Symbol.for() , Symbol.keyFor()
`Symbol.for()`可以让我们重新使用一个新的`Symbol`值。

先搜索，后创建或使用。
```javascript
var s1 = Symbol.for('foo');
var s2 = Symbol.for('foo');

s1 === s2; // true
```
`Symbol.keyFor()`配套使用。
```javascript
var s1 = Symbol.for('foo');
Symbol.keyFor(s1); // 'foo'

var s2 = Symbol('foo');
Symbol.keyFor(s2); // undefined
```
## 6、解决一开始的问题
```javascript
```
