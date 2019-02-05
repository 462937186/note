> # promise
> ÿһ���첽�������̷���һ��**Promise**�������������̷��أ����Կ��Բ���ͬ�����������̡���Promise��then����������ָ���ص����������첽������ɺ����
> �����setTimeout()���Դ������Ϊһ��ajax��������ajax����ͬ��
> 
> ```js
> function a() {
> 	return new Promise(function(resolve, reject) {
> 		setTimeout(function() {
> 			console.log('ִ������a');
> 			resolve('ִ������a�ɹ�');
> 		}, 1000);
> 	});
> }
> 
> function b(value) {
> 	console.log(value)
> 	return new Promise(function(resolve, reject) {
> 		setTimeout(function() {
> 			console.log('ִ������b');
> 			resolve('ִ������b�ɹ�');
> 		}, 2000);
> 	});
> }
> 
> function c() {
> 	console.log('���ִ��c')
> }
> a().then(b).then(c);
> ```
> 
> * ���then��return��ֵ��promise��resolve�Ľ��������һ��then
> * ���then��return���صĲ���promise�򽫽��ֱ�Ӵ�����һ��then
> 
> # ��promise
> �ܶ���promise���첽��װ����������angular1.x���÷�װ��$http���������£�����ʵ�ֶ���ص�����ʽ���ã������˽�����ʽ�Ļص�����
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
> 		console.log("��ʱ��")
> 	}, 1000)
> })
> ```
> 
> # await
> await �Ǹ��������������ɱ��ʽ��await ���ʽ��������ȡ�������ȵĶ�����
> 
> ������ȵ��Ĳ���һ�� Promise ������ await ���ʽ���������������ȵ��Ķ�����
> 
> ������ȵ�����һ�� Promise ����await ��æ�����ˣ�������������Ĵ��룬���� Promise ���� resolve��Ȼ��õ� resolve ��ֵ����Ϊ await ���ʽ����������
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
> await�ȴ�����Ȼ��promise���󣬵�����д`.then(..)`��ֱ�ӿ��Եõ�����ֵ������ʹ��await��û���˶��then����ʽ����
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
>     // ������ʹ����������ͬ����������ֱ��
>     console.log('start');
>     await sleep(3000);
>     console.log('end');
> };
> start();
> ```
> 
> * async��ʾ����һ��async������awaitֻ����������������档
> * await��ʾ������ȴ�promise���ؽ���ˣ��ټ���ִ�С�
> * await������ŵ�Ӧ����һ��promise���󣨵�Ȼ����������ֵҲû��ϵ������������û�������ˣ�
> 
> # deferred
> $.ajax()������ɺ����ʹ�õ��ǵ���1.5.0�汾��jQuery�����ص���XHR������û��������ʽ�������������1.5.0�汾�����ص���deferred���󣬿��Խ�����ʽ������done()�൱��success������fail()�൱��error������������ʽд���Ժ󣬴���Ŀɶ��Դ����ߣ�deferred�����һ��ô���������������������Ӷ���ص�����
> 
> ```js
> $.when(function(dtd) {
> 	var dtd = $.Deferred(); // �½�һ��deferred����
> 	setTimeout(function() {
> 		console.log(0);
> 		dtd.resolve(1); // �ı�deferred�����ִ��״̬ ����done�ص�
> 		//dtd.reject(); //��resolve�෴������fail�ص�
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
> //ajaxĬ�Ͼ��Ƿ���deferred����
> $.when($.post("index.php", {
> 		name: "wscat",
> 	}), $.post("other.php"))
> 	.done(function(data1, data2) {
> 		//����ajax�ɹ��ſ��Խ���done�ص�
> 		console.log(data1, data2);
> 	}).fail(function(err) {
> 		//����һ��ajaxʧ�ܶ������fail�ص�
> 		console.log(err)
> 	})
> ```
> 
> # event loop
> * [�㲻�ò�֪��Event Loop](https://segmentfault.com/a/1190000013720401?utm_source=tag-newest)
> * [��һ����ǳ˵ JavaScript ���¼�ѭ��](https://github.com/dwqs/blog/issues/61)
> 
> # ����await/async����
> ��װһ������
> 
> ```shell
> npm i -D babel-core babel-polyfill babel-preset-es2015 babel-preset-stage-0 babel-loader
> ```
> 
> �½�`.babelrc`�ļ���������������
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
> �½�һ��index.js��������߼��ļ�`app.js`������require���κ�ģ�鶼����babel����polyfill֧��`await`��`async`
> 
> ```js
> require("babel-core/register");
> require("babel-polyfill");
> require("./app.js");
> ```
> 
> �ο�[Babel 6 regeneratorRuntime is not defined ](https://stackoverflow.com/questions/33527653/babel-6-regeneratorruntime-is-not-defined)
> 
> # await,async,promise�������
> ```js
> //async����������첽����˳��ִ��
> ((async() => {
> 	try {
> 		//await�൱�ڵȴ�ÿ���첽����ִ����ɣ�Ȼ�������һ��await����
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
> 		//����try��һ������reject����������֧
> 		console.log(err);
> 		return err;
> 	}
> })()).then((data) => {
> 	console.error(data)
> }).catch((err) => {
> 	console.error(err)
> })
> //�ֱ����213
> ```
> 
> ע��㣺
> 
> * async��������������������ݿ��Խ���ͬ���ķ�ʽִ�У�await���ǽ���ִ��˳����ƣ�ÿ��ִ��һ��await�����򶼻���ͣ�ȴ�await����ֵ��Ȼ����ִ��֮���await��
> * await������õĺ�����Ҫ����һ��promise���������������һ����ͨ�ĺ������ɣ�������generator��
> * awaitֻ������async����֮�У�������ͨ�����лᱨ��
> * await�������� Promise �������н�������� rejected��������ð� await ������� try...catch ������С�
> 
> ��Ȼ�Ҹ��˾�������д���Ƚ�������
> 
> ```js
> //����try...catch��׽Promise��reject
> async function ajax(data) {
> 	try {
> 		return await new Promise((resolve, reject) => {
> 			setTimeout(() => {
> 				console.log(data)
> 				resolve(data); //�ɹ�
> 			}, 2000);
> 		});
> 	} catch(err) {}
> }
> async function io() {
> 	try {
> 		const response = await new Promise((resolve, reject) => {
> 			setTimeout(() => {
> 				reject("io"); //ʧ��
> 			}, 1000);
> 		});
> 		//resolveִ�вŻ�ִ���������return 
> 		return response
> 	} catch(err) {
> 		console.log(err);
> 	}
> }
> //�첽����
> (async() => {
> 	await ajax("ajax1");
> 	await ajax("ajax2");
> 	await io();
> })()
> ```
> 
> # �ο�����
> * [�����첽���ռ��������-ES7��Async/Await](https://cnodejs.org/topic/5640b80d3a6aa72c5e0030b6)
> * [NodeJsͨ��async/await�����첽](https://www.cnblogs.com/YikaJ/p/4996174.html)
> * [��� JavaScript �� async/await](https://segmentfault.com/a/1190000007535316)

