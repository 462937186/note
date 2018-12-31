#

> ## 介绍
> 在HTML5规范中，WebSocket现在越来越流行。WebSocket提供了一个受欢迎的技术，以替代我们过去几年一直在用的Ajax技术，这个新的API提供了一个方法，从客户端使用简单的语法有效地推动消息到服务器。让我们看一看HTML5的WebSocket API，它可用于客户端、服务器端。而且有一个优秀的第三方API，名为**Socket.IO**
>
> WebSocket是下一代客户端-->服务器的异步通信方法。该通信取代了单个的TCP套接字，使用ws或wss协议，可用于任意的客户端和服务器程序。WebSocket目前由W3C进行标准化。WebSocket已经受到Firefox 4、Chrome 4、Opera 10.70以及Safari 5等浏览器的支持。
>
> WebSocket最伟大之处在于服务器和客户端可以在给定的时间范围内的任意时刻，相互推送信息。WebSocket并不限于以Ajax(或XHR)方式通信，因为Ajax技术需要客户端发起请求，而WebSocket服务器和客户端可以彼此相互推送信息，XHR受到域的限制，而WebSocket允许跨域通信。
>
> WebSocket技术很聪明的一点是没有设计要使用的方式。WebSocket为指定目标创建，用于双向推送消息。
>
> ## 原生客户端WebSocket
> 下面的代码片段是打开一个连接，为连接创建事件监听器，断开连接，消息时间，发送消息返回到服务器，关闭连接。
>
> ```js
> // 创建一个Socket实例
> var socket = new WebSocket('ws://localhost:8080'); 
> 
> // 打开Socket 
> socket.onopen = function(event) { 
> 
>   // 发送一个初始化消息
>   socket.send('I am the client and I\'m listening!'); 
> 
>   // 监听消息
>   socket.onmessage = function(event) { 
>     console.log('Client received a message',event); 
>   }; 
> 
>   // 监听Socket的关闭
>   socket.onclose = function(event) { 
>     console.log('Client notified socket has closed',event); 
>   }; 
> 
>   // 关闭Socket.... 
>   //socket.close() 
> };
> ```
>
> 让我们来看看上面的初始化片段。参数为URL，ws表示WebSocket协议。onopen、onclose和onmessage方法把事件连接到Socket实例上。每个方法都提供了一个事件，以表示Socket的状态。
>
> onmessage事件提供了一个data属性，它可以包含消息的Body部分。消息的Body部分必须是一个字符串，可以进行序列化/反序列化操作，以便传递更多的数据。
>
> WebSocket的语法非常简单，使用WebSockets是难以置信的容易……除非客户端不支持WebSocket。IE浏览器目前不支持WebSocket通信。如果你的客户端不支持WebSocket通信，下面有几个后备方案供你使用：
>
> * Flash技术 —— Flash可以提供一个简单的替换。 使用Flash最明显的缺点是并非所有客户端都安装了Flash，而且某些客户端，如iPhone/iPad，不支持Flash。
> * AJAX Long-Polling技术 —— 用AJAX的long-polling来模拟WebSocket在业界已经有一段时间了。它是一个可行的技术，但它不能优化发送的信息。也就是说，它是一个解决方案，但不是最佳的技术方案。
> * 由于目前的IE等浏览器不支持WebSocket，要提供WebSocket的事件处理、返回传输、在服务器端使用一个统一的API，那么该怎么办呢？幸运的是，Guillermo Rauch创建了一个Socket.IO技术。
>
> ## 原生服务端websocket
> [用 Node 实现简单 WebSocket 协议](https://segmentfault.com/a/1190000012614419)
>
> ## 安装
> ```js
> npm install socket.io
> ```
>
> [官网参考文档](https://socket.io/docs/)
>
> ![image](https://cloud.githubusercontent.com/assets/17243165/21577625/b741a800-cf9c-11e6-904f-6282209f8ade.png)
>
> ## 服务端
> ```js
> var app = require('http').createServer(function(req, res) {})
> var io = require('socket.io')(app);
> app.listen(80);
> io.on('connection', function (socket) {
>   socket.emit('news', { hello: 'world' });
>   socket.on('my other event', function (data) {
>     console.log(data);
>   });
> });
> ```
>
> ## 客户端（非原生）
>
> ### 前端
>
> 客户端的JS文件，可以在CDN上得到
>
> ```js
> <script src="https://cdn.socket.io/socket.io-1.4.4.js"></script>
> ```
>
> ```html
> <!DOCTYPE html>
> <html>
> 	<head>
> 		<meta charset="UTF-8">
> 		<title></title>
> 	</head>
> 	<body>
> 	</body>
> 	<script src="js/socket.js"></script>
> 	<script>
> 		var socket = io('http://localhost:3001');
> 			socket.on('connect', function() {});
> 			socket.on('event', function(data) {});
> 			socket.on('disconnect', function() {});
> 			//监听
> 			socket.on('getServerMessage', function(data) {
> 				console.log(data)
> 			});
> 	</script>
> </html>
> ```
>
> 此时长连接后端有改动，前端就立即能接受新的值
>
> ### 后端
>
> 在express中使用，以下代码
>
> ```js
> var app = require('express')();
> var server = require('http').createServer(app);
> var io = require('socket.io')(server);
> io.on('connection', function(){ /* … */ });
> server.listen(3000);
> ```
>
> | 接口            | 描述     |
> | --------------- | -------- |
> | `socket.on()`   | 发送信息 |
> | `socket.emit()` | 接受信息 |
>
> ```js
> var app = require('express')();
> 	var server = require('http').createServer(app);
> 	var io = require('socket.io')(server);
> 	io.on('connection', function(socket) {
> 		//发送socket信息的逻辑写在这里
> 		/* … */
> 		//监听
> 		//socket.on();
> 		//发送
> 		setInterval(()=>{
> 			socket.emit('getServerMessage',parseInt(Math.random()*100));
> 		},1000)
> 	});
> 	server.listen(3001);
> ```
>
> ## 发送公共信息
> server
>
> ```js
> io.on('connection', function (socket) {
>         io.emit('pub', { will: 'be received by everyone'});
>         //or
>         io.sockets.emit("pub",{data:"hello,all"});
> });
> ```
>
> client
>
> ```js
> socket.on('pub', function(data) {
> 	console.log(data);
> });
> ```
>
> ## 发送私有信息
> server
>
> ```js
> socket.on('private message', function(from, to, msg) {
>         //客户端可传多个参数，服务端也可接受多个参数
> 	console.log(to, ' received a private message by ', from, ' saying ', msg.msg);
> });
> ```
>
> client
>
> ```js
> socket.emit('private message', 'oaoafly', 'windiest', {
> 	msg: 'hello'
> });
> ```
>
> 获取**socket.id**，每个客户端都有一个对应的**socket.id**
> 然后通过下面方法实现单对单的私人聊天
>
> ```js
> io.sockets.sockets[data.toId].emit("getMessage", data)
> ```
>
> ## 实例
>
> ```js
> function socket() {
> 	var app = require('express')();
> 	var server = require('http').createServer(app);
> 	var io = require('socket.io')(server);
> 	io.on('connection', function(socket) {
> 		console.log(socket.id);
> 		//发送socket信息的逻辑写在这里
> 		/* … */
> 		//监听
> 		//socket.on();
> 		//发送
> 		//		setInterval(()=>{
> 		//			socket.emit('getServerMessage',parseInt(Math.random()*100));
> 		//		},1000)
> 		socket.on("sendMessageToServer", function(data) {
> 			//公聊
> 			io.sockets.emit("sendMessageToAllClient", data)
> 			//私聊
> 			//io.sockets.sockets[socketid].emit
> 		})
> 	});
> 	server.listen(3001);
> }
> 
> module.exports = {
> 	socket
> }
> 
> 
> ```
>
> ## 
>
> ## 客户端监听的事件
>
> 客户端`socket.on()`监听的事件：
>
> * connect：连接成功
> * connecting：正在连接
> * disconnect：断开连接
> * connect_failed：连接失败
> * error：错误发生，并且无法被其他事件类型所处理
> * message：同服务器端message事件
> * anything：同服务器端anything事件
> * reconnect_failed：重连失败
> * reconnect：成功重连
> * reconnecting：正在重连
>
> 比如
> 客户端连接上服务端时候会触发回调函数
>
> ```js
> socket.on('connect', function() {
> 	console.log('Client has connected to the server!');
> });
> ```
>
> 终止服务端时候客户端触发的回调函数
>
> ```js
> socket.on('disconnect', function() {
> 	console.log('The client has disconnected!');
> });
> ```
>
> ## express配合websocket
> ```js
> var ioFn = require("socket.io");
> var express = require("express");
> var http = require("http")
> var server = http.createServer()
> var io = ioFn(server);
> var app = express();
> app.get("/", function(req, res) {
> 	res.send("hello")
> }).listen(9999);
> io.on("connection", function() {
> 
> })
> ```
>
> ## 参考文档
> [实时通讯之Socket.io](http://blog.csdn.net/nathanhuang1220/article/details/41348213)
