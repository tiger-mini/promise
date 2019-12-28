# promise
promise 自实现




[https://juejin.im/post/5c121b82f265da612061b225](https://juejin.im/post/5c121b82f265da612061b225)

```
// Promise 形式的异步方法定义
var promiseAsyncFunc = function() {
  var fulfillCallback
  var rejectCallback

  setTimeout(() => {
    var randomNumber = Math.random()
    if (randomNumber > 0.5) fulfillCallback(randomNumber)
    else rejectCallback(randomNumber)
  }, 1000)
  return {
    then: function(_fulfillCallback, _rejectCallback) {
      fulfillCallback = _fulfillCallback
      rejectCallback = _rejectCallback
    }
  }
}

// Promise 形式的异步方法调用
promiseAsyncFunc().then(fulfillCallback, rejectCallback)
```
我们的思路是在 .then() 方法中, 将 fullfill 和 reject 结果的回调函数保存下来, 然后在异步方法中调用. 因为是异步调用, 根据 event-loop 的原理, promiseAsyncFunc().then(fulfillCallback, rejectCallback) 传入的 callback 在异步调用结束时一定是已经赋值过了.




