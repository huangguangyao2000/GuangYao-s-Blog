# JS-JSON

## 语法

* 简单值：使用与JavaScript相同的语法，但不支持`undifined`
* 对象
* 数组

不支持变量、函数或对象实例，是一种表示结构化数据的格式。

## 解析与序列化

JSON成了Web服务开发中交换数据的事实标准

### JSON对象

早期使用JavaScript的`eval`函数

ECMAScript 5 对解析JSON行为进行规范，定义了全局对象JSON。有两个方法：

* `stringify()`序列化成JSON字符串
* `parse()`把字符串解析为原生JavaScript值。

  **序列化选项**

* 过滤结果

  ```javascript
  var jsonText = JSON.stringify(book,['title','edition']);
  ```

  后两个参数与将要序列化的对象中的属性是对应的，在返回的结果字符串中就**只会包含这两个属性**。

若传入的第二个参数为**函数**，传入的函数接收两个参数，属性名和属性值。

```javascript
var book = {
    "title":"Professional JavaScript",
    "authors":["Nicholas C. Zakas"],
     edition:3,
     year:2011
};
var jsonText = JSON.stringify(book,function(key,value){
    switch(key){
        case 'authors':
                return value.join(",")
        case 'year':
                return 5000;
        case 'edition':
                return undefined;
        default:
                return value;
    }
})
```

返回：

```javascript
{"title":"Professional JavaScript","authors":"Nicholas C. Zakas","year":5000}
```

函数会根据返回值修改JSON对象。 2. 字符串缩进 `JSON.stringify()`第三个参数用于控制结果中的缩进和空白符。 3. toJSON\(\)方法 返回其自身的JSON数据格式。

### 解析选项

`JSON.parse()`可接收另一个参数，该参数为函数，将在每个键值对上调用。

