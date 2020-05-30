# Proxy



* Proxy用于修改某些操作的默认行为。是对编程语言的修改或编程。
* 提供对外界访问进行过滤和改写的机制
* 拦截操作：
  * `get(target,propKey,receiver)`：拦截对象读取
  * `set(target,propKey,value,receiver)`：拦截对象属性的设置
  * `has(target,propKey)`：拦截`propKey in proxy`的操作，返回布尔值
  * `ownKeys(target)`：拦截`Object.getOwnPropertyNames(proxy)`、`Object.getOwnpropertySymbols(proxy)`、`Object.keys(proxy)`、`for...in`等，返回一个数组。返回目标对象所有自身属性的属性名。`Object.keys()`的返回结果仅包括目标对象自身的可遍历属性。

```javascript
var proxy = new Proxy({},{
    get:function(target,propKey){
        return 35;
    }
});
proxy.time //35
proxy.name //35
proxy.title //35
```

```javascript
//handler没有设置任何拦截，则等同于直接通向原对象
var target = {};
var handler = {};
var proxy = new Proxy(target,handler);
proxy.a = 'b';
target.a  //'b'
```

```javascript
//Proxy实例可以作为其他对象的原型对象
var proxy = new Proxy({},{
    get:function(target,propKey){
        return 35;
    }
});

let obj = Object.create(proxy);
obj.time //35，从原型链中的proxy实例获得的time属性
```

