#

> ## ����
> ��HTML5�淶�У�WebSocket����Խ��Խ���С�WebSocket�ṩ��һ���ܻ�ӭ�ļ�������������ǹ�ȥ����һֱ���õ�Ajax����������µ�API�ṩ��һ���������ӿͻ���ʹ�ü򵥵��﷨��Ч���ƶ���Ϣ���������������ǿ�һ��HTML5��WebSocket API���������ڿͻ��ˡ��������ˡ�������һ������ĵ�����API����Ϊ**Socket.IO**
>
> WebSocket����һ���ͻ���-->���������첽ͨ�ŷ�������ͨ��ȡ���˵�����TCP�׽��֣�ʹ��ws��wssЭ�飬����������Ŀͻ��˺ͷ���������WebSocketĿǰ��W3C���б�׼����WebSocket�Ѿ��ܵ�Firefox 4��Chrome 4��Opera 10.70�Լ�Safari 5���������֧�֡�
>
> WebSocket��ΰ��֮�����ڷ������Ϳͻ��˿����ڸ�����ʱ�䷶Χ�ڵ�����ʱ�̣��໥������Ϣ��WebSocket����������Ajax(��XHR)��ʽͨ�ţ���ΪAjax������Ҫ�ͻ��˷������󣬶�WebSocket�������Ϳͻ��˿��Ա˴��໥������Ϣ��XHR�ܵ�������ƣ���WebSocket�������ͨ�š�
>
> WebSocket�����ܴ�����һ����û�����Ҫʹ�õķ�ʽ��WebSocketΪָ��Ŀ�괴��������˫��������Ϣ��
>
> ## ԭ���ͻ���WebSocket
> ����Ĵ���Ƭ���Ǵ�һ�����ӣ�Ϊ���Ӵ����¼����������Ͽ����ӣ���Ϣʱ�䣬������Ϣ���ص����������ر����ӡ�
>
> ```js
> // ����һ��Socketʵ��
> var socket = new WebSocket('ws://localhost:8080'); 
> 
> // ��Socket 
> socket.onopen = function(event) { 
> 
>   // ����һ����ʼ����Ϣ
>   socket.send('I am the client and I\'m listening!'); 
> 
>   // ������Ϣ
>   socket.onmessage = function(event) { 
>     console.log('Client received a message',event); 
>   }; 
> 
>   // ����Socket�Ĺر�
>   socket.onclose = function(event) { 
>     console.log('Client notified socket has closed',event); 
>   }; 
> 
>   // �ر�Socket.... 
>   //socket.close() 
> };
> ```
>
> ����������������ĳ�ʼ��Ƭ�Ρ�����ΪURL��ws��ʾWebSocketЭ�顣onopen��onclose��onmessage�������¼����ӵ�Socketʵ���ϡ�ÿ���������ṩ��һ���¼����Ա�ʾSocket��״̬��
>
> onmessage�¼��ṩ��һ��data���ԣ������԰�����Ϣ��Body���֡���Ϣ��Body���ֱ�����һ���ַ��������Խ������л�/�����л��������Ա㴫�ݸ�������ݡ�
>
> WebSocket���﷨�ǳ��򵥣�ʹ��WebSockets���������ŵ����ס������ǿͻ��˲�֧��WebSocket��IE�����Ŀǰ��֧��WebSocketͨ�š������Ŀͻ��˲�֧��WebSocketͨ�ţ������м����󱸷�������ʹ�ã�
>
> * Flash���� ���� Flash�����ṩһ���򵥵��滻�� ʹ��Flash�����Ե�ȱ���ǲ������пͻ��˶���װ��Flash������ĳЩ�ͻ��ˣ���iPhone/iPad����֧��Flash��
> * AJAX Long-Polling���� ���� ��AJAX��long-polling��ģ��WebSocket��ҵ���Ѿ���һ��ʱ���ˡ�����һ�����еļ��������������Ż����͵���Ϣ��Ҳ����˵������һ�������������������ѵļ���������
> * ����Ŀǰ��IE���������֧��WebSocket��Ҫ�ṩWebSocket���¼��������ش��䡢�ڷ�������ʹ��һ��ͳһ��API����ô����ô���أ����˵��ǣ�Guillermo Rauch������һ��Socket.IO������
>
> ## ԭ�������websocket
> [�� Node ʵ�ּ� WebSocket Э��](https://segmentfault.com/a/1190000012614419)
>
> ## ��װ
> ```js
> npm install socket.io
> ```
>
> [�����ο��ĵ�](https://socket.io/docs/)
>
> ![image](https://cloud.githubusercontent.com/assets/17243165/21577625/b741a800-cf9c-11e6-904f-6282209f8ade.png)
>
> ## �����
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
> ## �ͻ��ˣ���ԭ����
>
> ### ǰ��
>
> �ͻ��˵�JS�ļ���������CDN�ϵõ�
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
> 			//����
> 			socket.on('getServerMessage', function(data) {
> 				console.log(data)
> 			});
> 	</script>
> </html>
> ```
>
> ��ʱ�����Ӻ���иĶ���ǰ�˾������ܽ����µ�ֵ
>
> ### ���
>
> ��express��ʹ�ã����´���
>
> ```js
> var app = require('express')();
> var server = require('http').createServer(app);
> var io = require('socket.io')(server);
> io.on('connection', function(){ /* �� */ });
> server.listen(3000);
> ```
>
> | �ӿ�            | ����     |
> | --------------- | -------- |
> | `socket.on()`   | ������Ϣ |
> | `socket.emit()` | ������Ϣ |
>
> ```js
> var app = require('express')();
> 	var server = require('http').createServer(app);
> 	var io = require('socket.io')(server);
> 	io.on('connection', function(socket) {
> 		//����socket��Ϣ���߼�д������
> 		/* �� */
> 		//����
> 		//socket.on();
> 		//����
> 		setInterval(()=>{
> 			socket.emit('getServerMessage',parseInt(Math.random()*100));
> 		},1000)
> 	});
> 	server.listen(3001);
> ```
>
> ## ���͹�����Ϣ
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
> ## ����˽����Ϣ
> server
>
> ```js
> socket.on('private message', function(from, to, msg) {
>         //�ͻ��˿ɴ���������������Ҳ�ɽ��ܶ������
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
> ��ȡ**socket.id**��ÿ���ͻ��˶���һ����Ӧ��**socket.id**
> Ȼ��ͨ�����淽��ʵ�ֵ��Ե���˽������
>
> ```js
> io.sockets.sockets[data.toId].emit("getMessage", data)
> ```
>
> ## ʵ��
>
> ```js
> function socket() {
> 	var app = require('express')();
> 	var server = require('http').createServer(app);
> 	var io = require('socket.io')(server);
> 	io.on('connection', function(socket) {
> 		console.log(socket.id);
> 		//����socket��Ϣ���߼�д������
> 		/* �� */
> 		//����
> 		//socket.on();
> 		//����
> 		//		setInterval(()=>{
> 		//			socket.emit('getServerMessage',parseInt(Math.random()*100));
> 		//		},1000)
> 		socket.on("sendMessageToServer", function(data) {
> 			//����
> 			io.sockets.emit("sendMessageToAllClient", data)
> 			//˽��
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
> ## �ͻ��˼������¼�
>
> �ͻ���`socket.on()`�������¼���
>
> * connect�����ӳɹ�
> * connecting����������
> * disconnect���Ͽ�����
> * connect_failed������ʧ��
> * error���������������޷��������¼�����������
> * message��ͬ��������message�¼�
> * anything��ͬ��������anything�¼�
> * reconnect_failed������ʧ��
> * reconnect���ɹ�����
> * reconnecting����������
>
> ����
> �ͻ��������Ϸ����ʱ��ᴥ���ص�����
>
> ```js
> socket.on('connect', function() {
> 	console.log('Client has connected to the server!');
> });
> ```
>
> ��ֹ�����ʱ��ͻ��˴����Ļص�����
>
> ```js
> socket.on('disconnect', function() {
> 	console.log('The client has disconnected!');
> });
> ```
>
> ## express���websocket
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
> ## �ο��ĵ�
> [ʵʱͨѶ֮Socket.io](http://blog.csdn.net/nathanhuang1220/article/details/41348213)
