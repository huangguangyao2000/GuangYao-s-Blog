# class

[Class](https://github.com/mqyqingfeng/Blog/issues/105)

### constructor

ES6中：

```javascript
class Person{
    constructor(name){
        this.name = name;
    }

    sayHello(){
        return 'hello,I am '+this.name;
    }
}
var kevin = new Person('Kevin');
kevin.sayHello();
```

ES5中

```javascript
function Person(name){
    this.name = name;
}
Person.prototype.sayHello = function(){
    return 'hello,I am '+this.name;
}
var kevin = new Person('Kevin');
kevin.sayHello();
```

ES5的构造函数Person对应ES6Person类的constructor方法

类的内部定义的所有方法，都是不可枚举的——es6中object.keys\(Person.prototype\);

### 实例属性

```javascript
class Person{
    constructor(){
        this.state = {
            count:0;
        };
    }
}

class Person{
    state = {
        count:0
    }
}

function Person(){
    this.state = {
        count:0
    }
}
```

### 静态方法

静态方法无法被实例访问，对比之下，放在类中的没有指定为静态方法的，对应到ES5中将作为从原型继承的方法

```javascript
class Person{
    static sayHello(){
        return 'hello'
    }
}

Person.sayHello();
var kevin = new Person();
kevin.sayHello();//类型错误
```

```javascript
//ES5
function Person(){}

Person.sayHello = function(){
    return 'hello'
}

Person.sayHello();

var kevin = new Person();
kevin.sayHello();
```

### 静态属性

```javascript
class Person(){}
Person.name = 'kevin'
```

```javascript
class Person(){
    static name = 'kevin'
}
```

```javascript
function Person(){};
Person.name = 'kevin'
```

### getter 和 setter

基本一致

### Babel编译

#### 编译1

```javascript
class Person{
    constructor(name){
        this.name = name;
    }
}
```

Babel编译后：

```javascript
var Person = function Person(name){
    _classCallCheck(this,Person);//检查Person是否通过new方式调用
    this.name = name;
}
```

#### 编译2

```javascript
class Person {
    // 实例属性
    foo = 'foo';
    // 静态属性
    static bar = 'bar';

    constructor(name) {
        this.name = name;
    }
}
```

Babel编译后

```javascript
function Person(name){
    _classCallCheck(this,Person);
    this.name = name;
    this.foo = 'foo'
}
Person.bar = 'bar'
```

#### 编译3

```javascript
class Person {
    constructor(name) {
        this.name = name;
    }

    sayHello() {
        return 'hello, I am ' + this.name;
    }

    static onlySayHello() {
        return 'hello'
    }

    get name() {
        return 'kevin';
    }

    set name(newName) {
        console.log('new name 为：' + newName)
    }
}
```

#### Babel编译

\_createClass 辅助函数，该函数传入三个参数，第一个是构造函数，在这个例子中也就是 Person，第二个是要添加到原型上的函数数组，第三个是要添加到构造函数本身的函数数组，也就是所有添加 static 关键字的函数。该函数的作用就是将函数数组中的方法添加到构造函数或者构造函数的原型中，最后返回这个构造函数。

```javascript
var _createClass = function(){
    function defineProperties(target,props){
        for(var i = 0; i < props.length; i++){
            var descriptor = props[i];
            descriptor.enumerable = descriptor.enumerable || false;
            descriptor.configurable = true;
            if("value" in descriptor) descriptor.writable = true;
            Object.defineProperty(target,descriptor.key,descriptor);
        }
    }
    return function(Constructor,protoProps,staticProps){
        if(protoProps) defineProperties(Constructor.prototype,protoProps);
        if(staticProps) defineProperties(Constructor,staticProps);
        return Constructor;
    }
}
```

