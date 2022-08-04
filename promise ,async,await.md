**《--promise--》**
promise是一个对象  他本身是同步的，为了解决es5中的回调地狱问题，es6中的异步问题
new promise 作用把异步请求改成同步执行，在new这个promise对象的时候需要传递一个函数，这个函数里面有两个参数，
分别是异步操作执行成功后的回调函数resolve和异步操作执行失败后的回调函数reject,
请求成功会执行resolve中的.then这个方法，请求失败会被reject中的.catch这个方法所捕获
promise  有三种状态 正在进行pending  已完成 fulfilled   已失败  rejected
状态变化有两种情况  pending=>fulifiled  pending=>rejected
状态一旦发生变化将不会在改变
api方法有 
.then()     会获取resolve中返回成功的数据
.catch()    会捕获reject中的错误的数据
.finally()     不论成功还是失败都会返回结果
.all()      同时请求多个数据，返回的是每个异步函数执行回调函数后的结果组成的数组，
.race()   返回响应最快的，但是如果数据在中间请求错误的话，会从前面正确的里面挑选出响应最快的那一个，
如果第一个错误将会直接报错，后面的都不会执行，谁先执行结束，谁先进入回调
promise应用场景    封装ajax请求  网络请求   解决es5中的回调地狱的问题
promise 是一种从左到右的横向写法  
**《--async  await--》**
async await  将异步请求变为同步执行  
async 声明一个异步函数，返回一个promise对象，async搭配await使用  ，
async后面不论有没有await都会返回一个promsie对象，
await必须要在async函数中执行，出现在普通函数会报错
await 的功能相当于promsie中的.then执行的内容，async要写在await最近一个函数的外面，
await会阻塞代码的执行，await不能单独使用
async await从上到下执行， 符合js的执行顺序
网络请求的时候会遇到我们出乎意料的问题，我们在try里面放可能出错的网络请求，如果有异常通过catch捕获错误
