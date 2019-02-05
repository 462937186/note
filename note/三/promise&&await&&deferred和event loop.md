> # promise
> 每一个异步请求立刻返回一个**Promise**对象，由于是立刻返回，所以可以采用同步操作的流程。而Promise的then方法，允许指定回调函数，在异步任务完成后调用
> 下面的setTimeout()可以代替理解为一个ajax请求，所以ajax请求同理
> 
> ```js
> function a() {
> 	return new Promise(function(resolve, reject) {
> 		setTimeout(function() {
> 			console.log('执行任务a');
> 			resolve('执行任务a成功');
> 		}, 1000);
> 	});
> }
> 
> function b(value) {
> 	console.log(value)
> 	return new Promise(function(resolve, reject) {
> 		setTimeout(function() {
> 			console.log('执行任务b');
> 			resolve('执行任务b成功');
> 		}, 2000);
> 	});
> }
> 
> function c() {
> 	console.log('最后执行c')
> }
> a().then(b).then(c);
> ```
> 
> * 如果then里return的值是promise则将resolve的结果传入下一个then
> * 如果then里return返回的不是promise则将结果直接传入下一个then
> 
> # 类promise
> 很多像promise的异步封装方法，比如angular1.x内置封装的$http方法，如下，可以实现多个回调的链式调用，避免了金字塔式的回调地狱
> 
> ```js
> //1
> $http({
> 	method: 'GET',
> 	url: 'news.json',
> }).then(function successCallback(response) {
> 	console.log(response)
> }, function errorCallback(response) {
> 	console.log(response)
> })
> //2
> .then(function() {
> 	return $http({
> 		method: 'GET',
> 		url: 'data.json',
> 	})
> }).then(function(data) {
> 	console.log(data)
> })
> //3
> .then(function() {
> 	setTimeout(function() {
> 		console.log("定时器")
> 	}, 1000)
> })
> ```
> 
> # await
> await 是个运算符，用于组成表达式，await 表达式的运算结果取决于它等的东西。
> 
> 如果它等到的不是一个 Promise 对象，那 await 表达式的运算结果就是它等到的东西。
> 
> 如果它等到的是一个 Promise 对象，await 就忙起来了，它会阻塞后面的代码，等着 Promise 对象 resolve，然后得到 resolve 的值，作为 await 表达式的运算结果。
> 
> ```js
> function a() {
>   return new Promise(function(resolve){
>     setTimeout(()=>{
>     	console.log("a")
>     	resolve()
>     },1000)
>   });
> }
> 
> function b() {
>   return new Promise(function(resolve){
>     setTimeout(()=>{
>     	console.log("b")
>     	resolve()
>     },1000)
>   });
> }
> 
> function c() {
>   return new Promise(function(resolve){
>     setTimeout(()=>{
>     	console.log("c")
>     	resolve()
>     },1000)
>   });
> }
> 
> //ES6
> a()
>   .then(b)
>   .then(c);
> 
> //ES2017
> await a();
> await b();
> await c();
> ```
> 
> await等待的虽然是promise对象，但不必写`.then(..)`，直接可以得到返回值，所以使用await就没有了多个then的链式调用
> 
> ```js
> var sleep = function (time) {
>     return new Promise(function (resolve, reject) {
>         setTimeout(function () {
>             resolve();
>         }, time);
>     })
> };
> 
> var start = async function () {
>     // 在这里使用起来就像同步代码那样直观
>     console.log('start');
>     await sleep(3000);
>     console.log('end');
> };
> start();
> ```
> 
> * async表示这是一个async函数，await只能用在这个函数里面。
> * await表示在这里等待promise返回结果了，再继续执行。
> * await后面跟着的应该是一个promise对象（当然，其他返回值也没关系，不过那样就没有意义了）
> 
> # deferred
> $.ajax()操作完成后，如果使用的是低于1.5.0版本的jQuery，返回的是XHR对象，你没法进行链式操作；如果高于1.5.0版本，返回的是deferred对象，可以进行链式操作，done()相当于success方法，fail()相当于error方法。采用链式写法以后，代码的可读性大大提高，deferred对象的一大好处，就是它允许你自由添加多个回调函数
> 
> ```js
> $.when(function(dtd) {
> 	var dtd = $.Deferred(); // 新建一个deferred对象
> 	setTimeout(function() {
> 		console.log(0);
> 		dtd.resolve(1); // 改变deferred对象的执行状态 触发done回调
> 		//dtd.reject(); //跟resolve相反，触发fail回调
> 	}, 1000);
> 	return dtd;
> }()).done(function(num) {
> 	console.log(num);
> }).done(function() {
> 	console.log(2);
> }).done(function() {
> 	console.log(2);
> })
> 
> //ajax默认就是返回deferred对象
> $.when($.post("index.php", {
> 		name: "wscat",
> 	}), $.post("other.php"))
> 	.done(function(data1, data2) {
> 		//两个ajax成功才可以进入done回调
> 		console.log(data1, data2);
> 	}).fail(function(err) {
> 		//其中一个ajax失败都会进入fail回调
> 		console.log(err)
> 	})
> ```
> 
> # event loop
> * [你不得不知的Event Loop](https://segmentfault.com/a/1190000013720401?utm_source=tag-newest)
> * [从一道题浅说 JavaScript 的事件循环](https://github.com/dwqs/blog/issues/61)
> 
> # 配置await/async环境
> 安装一下依赖
> 
> ```shell
> npm i -D babel-core babel-polyfill babel-preset-es2015 babel-preset-stage-0 babel-loader
> ```
> 
> 新建`.babelrc`文件，输入以下内容
> 
> ```js
> {
>     "presets": [
>         "stage-0",
>         "es2015"
>     ]
> }
> ```
> 
> 新建一份index.js，把你的逻辑文件`app.js`，后面require的任何模块都交给babel处理，polyfill支持`await`和`async`
> 
> ```js
> require("babel-core/register");
> require("babel-polyfill");
> require("./app.js");
> ```
> 
> 参考[Babel 6 regeneratorRuntime is not defined ](https://stackoverflow.com/questions/33527653/babel-6-regeneratorruntime-is-not-defined)
> 
> # await,async,promise三者配合
> ```js
> //async定义里面的异步函数顺序执行
> ((async() => {
> 	try {
> 		//await相当于等待每个异步函数执行完成，然后继续下一个await函数
> 		const a = await (() => {
> 			return new Promise((resolve, reject) => {
> 				setTimeout(() => {
> 					console.log(1)
> 					resolve(2);
> 					//reject(3)
> 				}, 1000)
> 			});
> 		})();
> 		const b = await (() => {
> 			return new Promise((resolve, reject) => {
> 				setTimeout(() => {
> 					console.log(1)
> 					//resolve(2);
> 					reject(3)
> 				}, 1000)
> 			});
> 		})();
> 		console.log(4)
> 		console.log(a) //3
> 		return b;
> 	} catch(err) {
> 		//上面try中一旦触发reject则进入这个分支
> 		console.log(err);
> 		return err;
> 	}
> })()).then((data) => {
> 	console.error(data)
> }).catch((err) => {
> 	console.error(err)
> })
> //分别输出213
> ```
> 
> 注意点：
> 
> * async用来申明里面包裹的内容可以进行同步的方式执行，await则是进行执行顺序控制，每次执行一个await，程序都会暂停等待await返回值，然后再执行之后的await。
> * await后面调用的函数需要返回一个promise，另外这个函数是一个普通的函数即可，而不是generator。
> * await只能用在async函数之中，用在普通函数中会报错。
> * await命令后面的 Promise 对象，运行结果可能是 rejected，所以最好把 await 命令放在 try...catch 代码块中。
> 
> 当然我个人觉得下面写法比较清晰点
> 
> ```js
> //利用try...catch捕捉Promise的reject
> async function ajax(data) {
> 	try {
> 		return await new Promise((resolve, reject) => {
> 			setTimeout(() => {
> 				console.log(data)
> 				resolve(data); //成功
> 			}, 2000);
> 		});
> 	} catch(err) {}
> }
> async function io() {
> 	try {
> 		const response = await new Promise((resolve, reject) => {
> 			setTimeout(() => {
> 				reject("io"); //失败
> 			}, 1000);
> 		});
> 		//resolve执行才会执行下面这句return 
> 		return response
> 	} catch(err) {
> 		console.log(err);
> 	}
> }
> //异步串行
> (async() => {
> 	await ajax("ajax1");
> 	await ajax("ajax2");
> 	await io();
> })()
> ```
> 
> # 参考文章
> * [体验异步的终极解决方案-ES7的Async/Await](https://cnodejs.org/topic/5640b80d3a6aa72c5e0030b6)
> * [NodeJs通过async/await处理异步](https://www.cnblogs.com/YikaJ/p/4996174.html)
> * [理解 JavaScript 的 async/await](https://segmentfault.com/a/1190000007535316)

