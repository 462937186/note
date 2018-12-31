> # ��װ
> ���Բο�[Express�ٷ��ĵ�](http://www.expressjs.com.cn/)
> ����express����
> 
> ```js
> npm install express
> ```
> 
> ![image](https://cloud.githubusercontent.com/assets/17243165/23907392/f81faf4a-090b-11e7-9ee4-5bceb5c1ba65.png)
> ��д�����ļ�index.js����ִ��
> 
> ```js
> node index/node index.js
> ```
> 
> # ��������
> ����GET�������req.query
> ����POST������Ҫ**body-parser**ģ�飬���req.body
> 
> GET	POST	JSONP	COOKIE
> `req.query`	`req.body`	`req.query`	`req.cookies`
> ```js
> //npm install express
> var express = require('express');
> //npm install body-parser
> var bodyParser = require("body-parser");
> var app = express();
> //���þ�̬�ļ���,�ڱ���public��ȡcss,js,html���ļ�
> app.use(express.static('public'));
> //post������Ҫbody-parserģ�鴦��
> app.use(bodyParser.urlencoded({
> 	extended: false
> }));
> app.get('/', function(req, res) {
> 	res.send('Hello World!');
> });
> app.get('/home', function(req, res) {
> 	//get�����������
> 	console.log('get�����������:', req.query);
> 	res.send('get����');
> });
> app.post('/home', function(req, res) {
> 	//post�����������
> 	console.log('post�����������:', req.body);
> 	res.send('post����');
> });
> var server = app.listen(3000, function() {
> 	var host = server.address().address;
> 	var port = server.address().port;
> 	console.log('Example app listening at http://%s:%s', host, port);
> });
> ```
> 
> # ƥ��·�ɲ���
> ```js
> app.get('/add/:id/:age', function(req, res) {
> 	//׷������ͷ
> 	res.append("Access-Control-Allow-Origin","*");
> 	//?id=xx&age=xxx
> 	console.log(req.query)
> 	//:id/:age
> 	console.log(req.params)
> 	res.send("Hello Oaoafly");
> })
> ```
> 
> # ����
> �����м����׷������ֹ����
> 
> ```js
> res.append("Access-Control-Allow-Origin","*");
> ```
> 
> # ģ���ļ�
> ���������ͼ�ļ��ķ��õط���Ȼ������jadeΪ��ģ����Ⱦ���棬����Ҳ��Ҫ��װjadeģ��ʵ��
> 
> ```js
> //views, ��ģ���ļ���Ŀ¼�����磺 
> app.set('views', './views')
> //view engine, ģ������
> app.set('view engine', 'jade')
> ```
> 
> Ȼ��װ��Ӧ��ģ������npm��
> 
> ```js
> npm install jade
> ```
> 
> Ȼ�󴴽�һ��views�ļ��У����������½�һ��xxxx.jade�ļ�����������
> 
> ```
> html
> 	head
> 	body
> 		h1 ���ǲ���
> 		p ���
> 			ul.hhh#ddd
> 				for n in news
> 					li=n.title
> ```
> 
> ���м����������¹ؼ����룬res.render("�ļ�����ʡ�Ժ�׺",{��Ҫ��Ⱦ��ģ���ϵ�����})
> 
> ```js
> app.get('/', function(req, res) {
> 	connection.query("select * from news",function(err,data){
> 	var content = "Hello Oaoafly";
> 	res.render("qianfeng",{
> 		//model
> 		name:'xie',
> 		name2:'lan',
> 		news:data
> 	    })
> 	})
> 	//res.send("<p style='color:red'>"+content+"</p>");
> })
> ```
> 
> # ��̬�ļ�
> Express�ṩ�����õ��м��`express.static`�����þ�̬�ļ��磺ͼƬ�� CSS��JavaScript��
> 
> �����ʹ��`express.static`�м�������þ�̬�ļ�·��
> 
> ���磬����㽫ͼƬ�� CSS��JavaScript�ļ�����`public`Ŀ¼��
> 
> ��`app.js`��Ŀ¼�´���һ��`public`�ļ��У�Ȼ���ڴ��������
> 
> ```js
> app.use(express.static('public'));
> ```
> 
> �����꾲̬�ļ��к����ǿ�����`res.sendFile(�ļ�·��)`���������ļ����͵�ǰ��
> 
> ע��·��Ҫ�þ���·��`__dirname + "/public/" + "upload.html"`
> 
> ```js
> app.get('/index.html', function (req, res) {
>    res.sendFile(__dirname + "/public" + "index.html");
> })
> ```
> 
> ����ֵ��ע���һ����ǣ�����ÿ��Ӧ�ó��򣬿����ж����̬Ŀ¼����������԰��ϴ����ļ����ͷ�Ŀ¼����������ĳ��ͼƬ��ʱ��ͻ���⼸����̬�ļ�����һ����ȡ
> 
> ```js
> app.use(express.static('public'));
> app.use(express.static('uploads'));
> app.use(express.static('files'));
> ```
> 
> # �������ݿ�
> �������ݿ⣬���԰�װmysqlģ��ʵ��
> 
> ```js
> var mysql = require("mysql");
> var connection = mysql.createConnection({
> 		host: "localhost",
> 		user: "root",
> 		password: "",
> 		database: "asm"
> })
> //ִ�����ݿ����� .close();
> connection.connect();
> app.post('/add', function(req, res) {
> 	//׷������ͷ
> 	res.append("Access-Control-Allow-Origin","*");
> 	console.log(req.body);
> 	connection.query("insert into news (title,text) values ('" + req.body.title + "','" + req.body.text + "')",function(err,data){
> 		console.log(data)
> 	})
> 	res.send("������Ϣ");
> 	
> })
> ```
> 
> # body-parser
> ```js
> npm install body-parser
> ```
> 
> Ȼ��ͨ��`app.use()`��������
> 
> ```js
> var express = require('express')
> var bodyParser = require('body-parser')
> var app = express()
> // parse application/x-www-form-urlencoded 
> app.use(bodyParser.urlencoded({ extended: false }))
> // parse application/json 
> app.use(bodyParser.json())
> ```
> 
> # cookie-parser
> ```js
> npm install cookie-parser
> ```
> 
> ͨ��`app.use()`��������
> 
> ```js
> var cookieParser = require('cookie-parser')
> app.use(cookieParser())
> ```
> 
> Ȼ�����м����ͨ��`req.cookies`��ȡǰ��ҳ���cookie����һ��ͨ������Ķ���
> 
> module	description
> querystring	��GET����url�е��ַ�����Ϣ����ת��
> chalk	�ѿ���̨�����Ϣ���ַ�����ɫ�ı�
> body-parser	���ͻ���ͨ��POST������������req.body���ݽ�����json����
> cookie-parser	����cookie��Ϣ
> svg-captcha	����������֤��
> trek-captcha	����������֤��
> emailjs	����ͨ�������һ�����
> validator	��֤��
> mongodb	����mongodb���ݿ�
> crypto	express�Դ��ļ���ģ��
> express-session	session����֤�����벻��cookie����Ҫͬʱʹ��`cookieParser`�м�����������������û��ĵ�½״̬���������½
> formidable	���ļ��ϴ�ģ��
> * [�ο�express���õ�ģ����](https://blog.csdn.net/YUHUI01/article/details/81048256)
> 
> # �ϴ��ļ�
> [node�ϴ��ļ�](https://github.com/Wscats/node-tutorial/issues/14)
> 
> # ������
> ```js
> npm install supervisor -g
> ```
> 
> ȫ�ְ�װ�󣬾ͻ���`supervisor`��������Զ��������ļ��仯��һ���仯����Զ�����
> 
> ```js
> supervisor app.js
> ```
> 
> # ������
> �������ö�·�ɵ����أ��������ڵ�¼���ص�
> 
> filter.js
> 
> ```js
> exports.authorize = function(req, res, next) {
> 	if(req.body.token) {
> 		//res.redirect('/beauty/test');
> 		console.log(1)
> 	} else {
> 		//res.redirect('/beauty/getFemaleList');
> 		console.log(2)
> 		next();
> 	}
> }
> ```
> 
> ·���߼�
> 
> ```js
> var express = require('express');
> var router = express.Router(); //ģ�黯
> var filter = require('../filter.js');
> router.get('/getFemaleList', filter.authorize, function(req, res) {
> 	res.send('hello world');
> });
> ```
> 
> ��ʱ����`/getFemaleList`·�ɵ�ʱ��ͻ����������߼����Ӷ�ʵ�����ع���
> 
> # ES6
> Ҫ��Express��ES6���������Ͳ��ò���ת����Babel�ˡ������½�һ����ĳĿ¼���½�һ����Ŀ��Ȼ����ת�����Ŀ¼�¿�ʼ����Ĳ���
> 
> ȫ�ְ�װ
> 
> ```shell
> npm install --save-dev babel-cli -g
> ```
> 
> Ȼ�󣬿��԰�װһЩpresets
> 
> ```shell
> cnpm install --save-dev babel-preset-es2015 babel-preset-stage-2
> ```
> 
> ��`package.json`��������еĽű�������Ϳ�����ES6����д����babel�Զ�������תES5����
> 
> ```js
> "scripts": {
>     "start": "babel-node index.js --presets es2015,stage-2"
> }
> ```
> 
> ������`babel lib -d dist`���router�ļ��е�����jsת��
> 
> ```js
> "scripts": {
>     "start": "babel-node --presets es2015,stage-2",
>     "build": "babel router -d dist --presets es2015,stage-2",
>      "serve": "node dist/index.js"
> }
> ```
> 
> # ���ּ�
> ȫ�ְ�װ
> 
> ```shell
> npm install -g express-generator@4
> ```
> 
> ��һ���ļ���������`express`�����Ӧ�üܹ�
> 
> ```shell
> express test
> cd test
> ```
> 
> ����test�ļ��а�װ�������Ƽ�`cnpm`��װ��������
> 
> ```shell
> npm install
> ```
> 
> ����Ӧ��
> 
> ```shell
> SET DEBUG=test:*
> npm start
> ```
> 
> �����������3000�˿ں�
> 
> ```shell
> http://localhost:3000
> ```
> 
> ### ����·��
> ���뵽testĿ¼��routes�ļ���,Ȼ����`users.js`
> 
> ����Ըı�`/home`�����·��
> 
> ```shell
> var express = require('express');
> var router = express.Router();
> router.get('/home', function(req, res, next) {
>   res.send('hello world');
> });
> module.exports = router;
> ```
> 
> ��`app.js`���������������·�ɾ������
> 
> ```js
> var homeRouter = require('./routes/home');
> //code
> app.use('/test', homeRouter);
> ```
> 
> ���ʸ�·��
> 
> ```js
> http://localhost:3000/test/home
> ```

