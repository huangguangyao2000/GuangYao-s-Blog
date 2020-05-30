# Iterator和for..of循环

* 表示集合的数据结构有——数组，对象，Map和Set
* Iterator提供接口，为不同的数据结构提供统一的访问机制，只要部署Iterator接口，即可完成遍历操作，主要供for..of消费
* 遍历过程
  * 创建指针对象，指向当前数据结构的起始位置。
  * 然后不断调用指针对象的next方法
* 统一访问机制for...of循环
  * 循环主动寻找Iterator接口
  * **ES6默认的Iterator接口部署在数据结构的`Symbol.iterator`**
* Symbol.iterator属性本身是一个函数，就是当前数据结构默认的遍历器生成函数。执行这个函数就会返回一个遍历器。属性名Symbol.iterator，是一个表达式，返回`Symbol`对象的`iterator`属性，是一个预定好的、类型为Symbol的特殊值，放在方括号内。
* 原生具备 Iterator 接口的数据结构如下。
  * Array
  * Map
  * Set
  * String
  * TypedArray
  * 函数的 arguments 对象
  * NodeList 对象
* 调用Iterator接口的场合
  * 解构赋值
  * 扩展运算符
  * yield
  * 其他
* 计算生成的数据结构
  * entries\(\) keys\(\) values\(\) 均返回遍历器对象
* 类数组对象——Array.from\(\)
* 对象
  * 普通对象，for...of结构不能直接使用，使用的话将报错。但for...in依然可以使用

