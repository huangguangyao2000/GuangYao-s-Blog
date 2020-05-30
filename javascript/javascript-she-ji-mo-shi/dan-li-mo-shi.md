# 单例模式

```javascript
//普通的单例模式
var Singleton = function(name){
    this.name = name;
    this.instance = null;
}

Singleton.prototype.getName = function(){
    console.log(this.name);
}

Singleton.getInstance = function(name){
    if(this.instance){
        return this.instance;
    }
    return this.instance = new Singleton(name);
}

var a = Singleton.getInstance('sven1');
var b = Singleton.getInstance('sven2');

console.log(a === b); //true

//2
var Singleton2 = function(name){
    this.name = name;   
}
Singleton2.getInstance = (function(){
    var instance = null;
    return function(name){
        if(!instance){
            instance = new Singleton2(name);
        }
        return instance;
    }
})();
```

```javascript
//透明的单例模式
var CreateDiv = (function(){
    var instance;

    var CreateDiv = function(html){
        if( instance ){
            return instance;
        }
        this.html = html;
        this.init();
        return instance = this;
    }

    CreateDiv.prototype.init = function(){
        var div = document.createElement('div');
        div.innerHTML = this.html;
        document.body.appendChild( div );
    }

    return CreateDiv;

})();

var a = new CreateDiv('sven1');
var b = new CreateDiv('sven2');
console.log(a);
console.log(a === b);
```

```javascript
//用代理实现单例模式
var CreateDiv = function(html){
    this.html = html;
    this.init();
}

CreateDiv.prototype.init = function(){
    var div = document.createElement('div');
    div.innerHTML = 'div';
    document.body.appendChild(div);
}

var ProxySingletonCreateDiv = (function(){
    var instance;
    return function (html) {
        if(!instance){
            instance = new CreateDiv(html);
        }
        return instance;
    }
})();

var a = new ProxySingletonCreateDiv('a');
var b = new ProxySingletonCreateDiv('b');

console.log(a === b);
```

