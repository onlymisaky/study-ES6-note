## 1、Set
`Set`类似数组，但是成员的值都是`唯一的`,没有重复的值。
```javascript
const s = new Set();
[1, 1, 2, 2, 3, 3, 4, 4,].forEach(n => s.add(n));
console.log(s); // Set { 1, 2, 3, 4 }
```
可以用于数组去重（浅数组）
```javascript
const set = new Set([1, 2, 3, 3]);
[...set]; // [ 1, 2, 3 ]
```
### 1.2、Set实例的属性和方法
- `Set.portotype.size`
- `Set.portotype.add(value)`：返回Set结构本身。
- `Set.portotype.delete(value)`：返回bool值。
- `Set.portotype.has(value)`：返回bool值。
- `Set.portotype.clear()`：没有返回值。
### 1.3、  Set的遍历
- `keys()`，`value()`，`entries()`
```javascript
let set = new Set(['red', 'green', 'blue']);

for (let item of set.keys()) {
    console.log(item);
    // red green blue
}

for (let item of set.values()) {
    console.log(item);
    // red green blue
}

for (let item of set.entries()) {
    console.log(item);
    // [ 'red', 'red' ]
    // [ 'green', 'green' ]
    // [ 'blue', 'blue' ]
}
```
- `forEach()`
```javascript
let set = new Set(['red', 'green', 'blue']);

set.forEach((value, key) => console.log(value, key));
// red red
// green green
// blue blue
```
## 2、WeakSet
`WeakSet` 结构与 `Set` 类似，也是不重复的值的集合。但是，它与 Set 有两个区别。

首先，WeakSet 的成员只能是对象，而不能是其他类型的值。

其次，`WeakSet` 中的对象都是`弱引用`，即垃圾回收机制不考虑 `WeakSet` 对该对象的引用，也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于 `WeakSet` 之中。

`WeakSet`不可以遍历。
## 3、Map
`Map`是加强版的对象，它的键可以是对象。

`Map`在作为构造函数的时候，可以接受数组作为参数。
```javascript
const map = new Map([
    ['name', 'qq'],
    ['age', 18]
]);
map.size; //2
map.get('name'); // qq
```
### 3.2、实例方法
- `Map.portotype.size`
- `Map.portotype.set(key, value)`：返回Map结构本身。
- `Map.portotype.get(key)`：
- `Map.portotype.has(key)`：返回bool值。
- `Map.portotype.delete(key)`：返回bool值。
- `Map.portotype.clear()`：没有返回值。
### 3.3、遍历
- `keys()`：返回键名的遍历器。
- `values()`：返回键值的遍历器。
- `entries()`：返回所有成员的遍历器。
- `forEach()`：遍历 Map 的所有成员。

需要特别注意的是，Map 的遍历顺序就是插入顺序。

可以通过扩展运算符，快速将`Map`转换为数组。
```javascript
const map = new Map([
    [1, 'one'],
    [2, 'two'],
    [3, 'three']
]);
[...map.keys()]; // [1, 2, 3]
[...map.values()]; // ['one', 'two', 'three']
[...map.entries()]; // [[1, 'one'], [2, 'two'], [3, 'three']]
[...map]; // [[1, 'one'], [2, 'two'], [3, 'three']]
```
## 4、WeakMap
