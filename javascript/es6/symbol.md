# Symbol



* 表示独一无二的值，通过Symbol函数生成
* 作为属性名，避免属性被覆盖。
* Symbol 作为属性名，遍历对象的时候，该属性不会出现在for...in、for...of循环中，也不会被Object.keys\(\)、Object.getOwnPropertyNames\(\)、JSON.stringify\(\)返回。Object.getOwnPropertySymbols\(\)方法的示例，可以获取所有 Symbol 属性名。Reflect.ownKeys\(\)方法可以返回所有类型的键名，包括常规键名和 Symbol 键名。

```javascript
let s = Symbol();
typeof s; //"symbol"





let s1 = Symbol('foo');
let s2 = Symbol('bar');

s1 //Symbol(foo)
s2 //Symbol(bar)

s1.toString();
s2.toString();

+s1 //类型错误
!s1

Boolean(s1);




const obj = {
    toString(){
        return 'abc';
    }
}
const sym = Symbol(obj);//obj为对象的话，调用对象的toString方法




const sym2 = Symbol('foo');
sym2.description //'foo'





let mySymbol = Symbol();

let a = {};
a[mySymbol] = 'Hello!';
Object.defineProperty(a,mySymbol,{value:'Hello!'});
let a = {
    [mySymbol]:'Hello!'
}
a[mySymbol] //'Hello!'







//不能使用点运算符
const mySymbol = Symbol();
const a = {};
a.mySymbol = 'Hello!';
a[mySymbol] //undefined
a['mySymbol'] //"Hello!',点运算符后面总是字符串



const obj = {};
const foo = Symbol('foo');

obj[foo] = 'bar';

for(let i in obj){
    console.log(i); //无输出
}

Object.getOwnPropertyNames(obj); //[]
Object.getOwnPropertySymbols(obj); //[Symbol(foo)]
Reflect.ownKeys(obj);
```

