# this+call+apply

```javascript
Function.prototype.bind2 = function (context) {
    var self = this,
        context = [].shift.call(arguments),
        args = [].slice.call(arguments);
    return function(){
        self.apply(context,[].concat.call(args,[].slice.call(arguments)));
    };
}

var obj = {
    name:'sven'
}
var func = function () {
    console.log(this.name);
}.bind2(obj);

func();

```

