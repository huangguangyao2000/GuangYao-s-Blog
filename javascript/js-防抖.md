# JS-防抖

前端有一些频繁的事件触发如： 1. window的resize、scroll方法 2. mousedown、mousemove 3. keyup、keydown ......

## 解决方案

解决事件频繁触发一般有两种解决方案： 1. debounce防抖 2. throttle节流

## 防抖

无论事件触发多快，也一定只在事件触发n秒后才执行。如果在一个事件触发n秒内又触发了事件，则将以新事件的时间为准。

## 版本一

`index.html`

```markup
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>debouce</title>
    <style>
        #container{
            width: 100%;
            height: 200px;
            line-height: 200px;
            text-align: center;
            color: #fff; 
            background-color: #444; 
            font-size: 30px;
        }
        }
    </style>
</head>
<body>
    <div id="container"></div>
    <script src="debouce.js"></script>
</body>
</html>
```

```javascript
function debounce(func,wait){
    var timeout;
    return function(){
        clearTimeout(timeout);
        timeout = setTimeout(func,wait);
    }
}
container.onmousemove = debounce(getUserAction,500);
```

## 版本二

```javascript
//第二版代码，解决getUserAction中可能出现的this指向问题
function debounce(func,wait){
    var timeout;
    return function(){
        var context = this;

        clearTimeout(timeout);
        timeout = setTimeout(function(){
            func.apply(context);
        },wait);
    }
}
container.onmousemove = debounce(getUserAction,500);
//
```

## 版本三

```javascript
//没有使用debounce调用getUserAction时：
// container.onmousemove = getUserAction; //打印e将输出MouseEvent
//使用debounce调用时打印undefine，即事件这个参数没有被带到debounce函数上。
function debounce(func,wait){
    var timeout;
    return function(){
        var context = this;
        var args = arguments;
        debugger;

        clearTimeout(timeout);
        timeout = setTimeout(function(){
            func.apply(context,args);
        },wait);
    }
}
container.onmousemove = debounce(getUserAction,500);
```

## 版本四

```javascript
//第四版 立即执行
function debounce(func,wait,immediate){
    var timeout;

    return function(){
        debugger;
        var context = this;
        var args = arguments;

        if(timeout) clearTimeout(timeout);
        if(immediate){
            var callNow = !timeout;
            timeout = setTimeout(function(){
                timeout = null;
            },wait)
            if(callNow) func.apply(context,args)
        }else{
            timeout = setTimeout(function(){
                func.apply(context,args);
            },wait);
        }
    }
}
container.onmousemove = debounce(getUserAction,500,true);
```

## 版本五

```javascript
第五版 返回值
function debounce(func,wait,immediate){
    var timeout,result;

    return function(){
        var context = this;
        var args = arguments;

        if(timeout) clearTimeout(timeout);
        if(immediate){
            var callNow = !timeout;
            timeout = setTimeout(function(){
                timeout = null;
            },wait)
            if(callNow) result = func.apply(context,args)
        }else{
            timeout = setTimeout(function(){
                func.apply(context,args);
            },wait);
        }
        return result;
    }
}
container.onmousemove = debounce(getUserAction,500,true);
```

## 版本六

```markup
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>debouce</title>
    <style>
        #container{
            width: 100%;
            height: 200px;
            line-height: 200px;
            text-align: center;
            color: #fff; 
            background-color: #444; 
            font-size: 30px;
        }
        }
    </style>
</head>
<body>
    <div id="container"></div>
    <button id="button">cancel</button>
    <script src="debouce.js"></script>
</body>
</html>
```

```javascript
//可用按钮取消防抖
function debounce(func,wait,immediate){
    var timeout,result;
    var debounced =  function(){
        var context = this;
        var args = arguments;

        if(timeout) clearTimeout(timeout);
        if(immediate){
            var callNow = !timeout;
            timeout = setTimeout(function(){
                timeout = null;
            },wait);
            if(callNow) result = func.apply(context,args);
        }else{
            timeout = setTimeout(function(){
                func.apply(context,args);
            },wait)
        }
        return result;
    };
    debounced.cancel = function(){
        clearTimeout(timeout);
        timeout = null;
    };
    return debounced;
}
var setUseAction = debounce(getUserAction, 1000, true);

container.onmousemove = setUseAction;

document.getElementById("button").addEventListener('click', function(){
    setUseAction.cancel();
})
```

