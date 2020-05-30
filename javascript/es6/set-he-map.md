# Set和Map



Set:

* Set.prototype.constructor：构造函数，默认就是Set函数。
* Set.prototype.size：返回Set实例的成员总数。
* Set.prototype.add\(value\)：添加某个值，返回 Set 结构本身。
* Set.prototype.delete\(value\)：删除某个值，返回一个布尔值，表示删除是否成功。
* Set.prototype.has\(value\)：返回一个布尔值，表示该值是否为Set的成员。
* Set.prototype.clear\(\)：清除所有成员，没有返回值。
* Set.prototype.keys\(\)：返回键名的遍历器
* Set.prototype.values\(\)：返回键值的遍历器
* Set.prototype.entries\(\)：返回键值对的遍历器
* Set.prototype.forEach\(\)：使用回调函数遍历每个成员

WeakSet:

* 成员为对象
* 方法:add delete has

Map:

* size
* set\(,\)
* get\(\)
* has
* clear
* delete
* values
* forEach
* entries
* keys

WeakMap:

* 对象
* 不计入垃圾回收机制
* DOM节点做键名

