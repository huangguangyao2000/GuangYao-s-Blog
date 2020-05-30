# Promise



* Promise对象有以下两个特点。
  * （1）对象的状态不受外界影响。Promise对象代表一个异步操作，有三种状态：pending（进行中）、fulfilled（已成功）和rejected（已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是Promise这个名字的由来，它的英语意思就是“承诺”，表示其他手段无法改变。
  * （2）一旦状态改变，就不会再变，任何时候都可以得到这个结果。Promise对象的状态改变，只有两种可能：从pending变为fulfilled和从pending变为rejected。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果，这时就称为 resolved（已定型）。如果改变已经发生了，你再对Promise对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。
* 实例

```javascript
const promise = new Promise(function(resolve,reject){
    if(/*异步操作成功*/){
        resolve(value);
    }else{
        reject(error);
    }
})

promise.then(function(value){
    //success
},function(error){
    //failure
})
```

*  JSON请求实例

```text

```js
const getJSON = function(url){
    const promise = new Promise(function(resolve,reject){
        const handler = function(){
            if(this.readyState!=4){
                return;
            }
            if(this.status == 200){
                resolve(this.response);
            }else{
                reject(new Error(this.statusText));
            }
        };
        const client = new XMLHttpRequest();
        client.open('GET',url);
        client.onreadystatechange = handler;
        client.responseType = 'json';
        client.setRequestHeader('Accept','application/json');
        client.send();
    });
    return promise;
};
getJSON("/posts.json").then(function(json){
    console.log(json);
},function(error){
    console.log(error);
})
```

* Promise.prototype.then

  链式调用

* Promise.prototype.catch\(\)
* Promise.prototype.finally\(\)

  不管Promise对象最后状态如何，都会执行的操作。

* Promise.all\(\)

  用于将多个Promise实例包装成一个新的Promise实例。

参数可以不是数组，但必须具有Iterator接口，且返回的每个成员都是promise实例。

状态有参数决定：

* 只要成员有一个被rejected，状态变为rejected
* 只有所有成员状态都变为fulfilled，状态才会变成fulfilled
  * Promise.race\(\)

    用于将多个Promise实例包装成一个新的Promise实例。

只要其中一个实例率先改变状态，p的状态就跟着改变

* Promise.resolve\(\)

  将现有对象转为Promise对象。

* Promise.reject\(\)

