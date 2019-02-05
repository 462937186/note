> # 安装
> 可以参考[Express官方文档](http://www.expressjs.com.cn/)
> 首先express环境
> 
> ```js
> npm install express
> ```
> 
> ![image](https://cloud.githubusercontent.com/assets/17243165/23907392/f81faf4a-090b-11e7-9ee4-5bceb5c1ba65.png)
> 编写配置文件index.js，并执行
> 
> ```js
> node index/node index.js
> ```
> 
> # 处理请求
> 处理GET请求：配合req.query
> 处理POST请求：需要**body-parser**模块，配合req.body
> 
> GET	POST	JSONP	COOKIE
> `req.query`	`req.body`	`req.query`	`req.cookies`
> ```js
> //npm install express
> var express = require('express');
> //npm install body-parser
> var bodyParser = require("body-parser");
> var app = express();
> //配置静态文件夹,在本地public读取css,js,html等文件
> app.use(express.static('public'));
> //post请求需要body-parser模块处理
> app.use(bodyParser.urlencoded({
> 	extended: false
> }));
> app.get('/', function(req, res) {
> 	res.send('Hello World!');
> });
> app.get('/home', function(req, res) {
> 	//get请求参数对象
> 	console.log('get请求参数对象:', req.query);
> 	res.send('get请求');
> });
> app.post('/home', function(req, res) {
> 	//post请求参数对象
> 	console.log('post请求参数对象:', req.body);
> 	res.send('post请求');
> });
> var server = app.listen(3000, function() {
> 	var host = server.address().address;
> 	var port = server.address().port;
> 	console.log('Example app listening at http://%s:%s', host, port);
> });
> ```
> 
> # 匹配路由参数
> ```js
> app.get('/add/:id/:age', function(req, res) {
> 	//追加请求头
> 	res.append("Access-Control-Allow-Origin","*");
> 	//?id=xx&age=xxx
> 	console.log(req.query)
> 	//:id/:age
> 	console.log(req.params)
> 	res.send("Hello Oaoafly");
> })
> ```
> 
> # 跨域
> 可在中间件中追加这句防止跨域
> 
> ```js
> res.append("Access-Control-Allow-Origin","*");
> ```
> 
> # 模板文件
> 这个设置视图文件的放置地方，然后配置jade为其模板渲染引擎，这里也需要安装jade模块实现
> 
> ```js
> //views, 放模板文件的目录，比如： 
> app.set('views', './views')
> //view engine, 模板引擎
> app.set('view engine', 'jade')
> ```
> 
> 然后安装对应的模板引擎npm包
> 
> ```js
> npm install jade
> ```
> 
> 然后创建一个views文件夹，并在里面新建一个xxxx.jade文件，内容如下
> 
> ```
> html
> 	head
> 	body
> 		h1 这是测试
> 		p 你好
> 			ul.hhh#ddd
> 				for n in news
> 					li=n.title
> ```
> 
> 在中间件中添加如下关键代码，res.render("文件名可省略后缀",{需要渲染在模板上的数据})
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
> # 静态文件
> Express提供了内置的中间件`express.static`来设置静态文件如：图片， CSS，JavaScript等
> 
> 你可以使用`express.static`中间件来设置静态文件路径
> 
> 例如，如果你将图片， CSS，JavaScript文件放在`public`目录下
> 
> 在`app.js`根目录下创建一个`public`文件夹，然后在代码中添加
> 
> ```js
> app.use(express.static('public'));
> ```
> 
> 设置完静态文件夹后我们可以用`res.sendFile(文件路径)`方法来把文件发送到前端
> 
> 注意路径要用绝对路径`__dirname + "/public/" + "upload.html"`
> 
> ```js
> app.get('/index.html', function (req, res) {
>    res.sendFile(__dirname + "/public" + "index.html");
> })
> ```
> 
> 还有值得注意的一点就是，对于每个应用程序，可以有多个静态目录，比如你可以按上传的文件类型分目录，当我们找某张图片的时候就会从这几个静态文件夹中一起找取
> 
> ```js
> app.use(express.static('public'));
> app.use(express.static('uploads'));
> app.use(express.static('files'));
> ```
> 
> # 连接数据库
> 连接数据库，可以安装mysql模块实现
> 
> ```js
> var mysql = require("mysql");
> var connection = mysql.createConnection({
> 		host: "localhost",
> 		user: "root",
> 		password: "",
> 		database: "asm"
> })
> //执行数据库连接 .close();
> connection.connect();
> app.post('/add', function(req, res) {
> 	//追加请求头
> 	res.append("Access-Control-Allow-Origin","*");
> 	console.log(req.body);
> 	connection.query("insert into news (title,text) values ('" + req.body.title + "','" + req.body.text + "')",function(err,data){
> 		console.log(data)
> 	})
> 	res.send("增加信息");
> 	
> })
> ```
> 
> # body-parser
> ```js
> npm install body-parser
> ```
> 
> 然后通过`app.use()`方法调用
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
> 通过`app.use()`方法调用
> 
> ```js
> var cookieParser = require('cookie-parser')
> app.use(cookieParser())
> ```
> 
> 然后在中间件中通过`req.cookies`获取前端页面的cookie，是一个通过处理的对象
> 
> module	description
> querystring	将GET请求url中的字符串信息进行转换
> chalk	把控制台输出信息的字符串颜色改变
> body-parser	将客户端通过POST方法传过来的req.body数据解析成json数据
> cookie-parser	处理cookie信息
> svg-captcha	用来生成验证码
> trek-captcha	用来生成验证码
> emailjs	用来通过邮箱找回密码
> validator	验证器
> mongodb	连接mongodb数据库
> crypto	express自带的加密模块
> express-session	session的认证机制离不开cookie，需要同时使用`cookieParser`中间件，可以用来保存用户的登陆状态，免密码登陆
> formidable	表单文件上传模块
> * [参考express常用的模块插件](https://blog.csdn.net/YUHUI01/article/details/81048256)
> 
> # 上传文件
> [node上传文件](https://github.com/Wscats/node-tutorial/issues/14)
> 
> # 热启动
> ```js
> npm install supervisor -g
> ```
> 
> 全局安装后，就会有`supervisor`命令，它会自动检测你的文件变化，一旦变化则会自动重启
> 
> ```js
> supervisor app.js
> ```
> 
> # 过滤器
> 可以设置对路由的拦截，比如用在登录拦截等
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
> 路由逻辑
> 
> ```js
> var express = require('express');
> var router = express.Router(); //模块化
> var filter = require('../filter.js');
> router.get('/getFemaleList', filter.authorize, function(req, res) {
> 	res.send('hello world');
> });
> ```
> 
> 此时访问`/getFemaleList`路由的时候就会进入过滤器逻辑，从而实现拦截功能
> 
> # ES6
> 要让Express在ES6下跑起来就不得不用转码器Babel了。首先新建一个在某目录下新建一个项目。然后跳转到这个目录下开始下面的操作
> 
> 全局安装
> 
> ```shell
> npm install --save-dev babel-cli -g
> ```
> 
> 然后，可以安装一些presets
> 
> ```shell
> cnpm install --save-dev babel-preset-es2015 babel-preset-stage-2
> ```
> 
> 在`package.json`里添加运行的脚本，这里就可以用ES6代码写程序，babel自动帮我们转ES5运行
> 
> ```js
> "scripts": {
>     "start": "babel-node index.js --presets es2015,stage-2"
> }
> ```
> 
> 可以用`babel lib -d dist`命令将router文件夹的所有js转码
> 
> ```js
> "scripts": {
>     "start": "babel-node --presets es2015,stage-2",
>     "build": "babel router -d dist --presets es2015,stage-2",
>      "serve": "node dist/index.js"
> }
> ```
> 
> # 脚手架
> 全局安装
> 
> ```shell
> npm install -g express-generator@4
> ```
> 
> 在一个文件夹里面用`express`命令创建应用架构
> 
> ```shell
> express test
> cd test
> ```
> 
> 进入test文件夹安装依赖，推荐`cnpm`安装所有依赖
> 
> ```shell
> npm install
> ```
> 
> 启动应用
> 
> ```shell
> SET DEBUG=test:*
> npm start
> ```
> 
> 访问在浏览器3000端口号
> 
> ```shell
> http://localhost:3000
> ```
> 
> ### 创建路由
> 进入到test目录的routes文件夹,然后复制`users.js`
> 
> 你可以改变`/home`这里的路径
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
> 在`app.js`添加以下两条，该路由就完成了
> 
> ```js
> var homeRouter = require('./routes/home');
> //code
> app.use('/test', homeRouter);
> ```
> 
> 访问该路径
> 
> ```js
> http://localhost:3000/test/home
> ```

