# Reflect



* 将`Object`对象的一些明显属于语言内部的方法如（`Object.defineProperty`），放到`Reflect`对象上。
* 修改某些`Object`方法的返回结果。
* 让`Object`操作变成函数行为。某些`Object`操作时命令式，如`name in obj`及`delete obj[name]`，而`Reflect.has(obj,name)`和`Reflect.deleteProperty(obj,name)`。
* `Reflect`对象的方法与`Proxy`对象的方法一一对应。
* 方法：
  * `Reflect.get()`
  * `Reflect.construct()`
  * `Reflect.set()`
  * `Reflect.defineProperty()`
  * `Reflect.has()`
  * `Reflect.ownKeys()`
  * `Reflect.getPrototypeOf()`

