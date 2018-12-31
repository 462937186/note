> # ��װmulterģ��
> # ��ͼ�ϴ�
> ```js
> npm install multer
> ```
> 
> # ����ģ��
> ����������express��һ��ģ��
> 
> ```js
> //����express������
> var express = require("express");
> var app = express();
> app.listen(3000);
> ```
> 
> ```js
> var multer = require('multer');
> /*var upload = multer({
> 	//��������ַ����ϴ���Ҫ�ֶ������������׺
>         //������������õĴ��룬�����ʡ����һ��
> 	dest: 'uploads/'
> })*/
> ```
> 
> # ����
> ���ñ����ļ��ĵط����������ϴ����ļ�����Ӧ�ļ���Ӻ�׺
> ����ͨ��`filename`���Զ����ļ�����ĸ�ʽ
> 
> ����ֵ	��;
> `destination`	������Դ�ı���·����ע�⣬���û����������Ĭ�ϻᱣ����`/tmp/uploads`�¡����⣬·����Ҫ�Լ�����
> `filename`	������Դ�����ڱ��ص��ļ���
> ```js
> var storage = multer.diskStorage({
> 	//�����ϴ����ļ�·����uploads�ļ��л��Զ�������
> 	destination: function(req, file, cb) {
> 		cb(null, './uploads')
> 	},
> 	//���ϴ��ļ�����������ȡ��Ӻ�׺��
> 	filename: function(req, file, cb) {
> 		var fileFormat = (file.originalname).split(".");
> 		//��ͼƬ����ʱ�����ʽ��ֹ������
> 		//����� abc.jpgͼƬ�и�Ϊ����[abc,jpg],Ȼ�������鳤��-1����ȡ��׺��
> 		cb(null, file.fieldname + '-' + Date.now() + "." + fileFormat[fileFormat.length - 1]);
> 	}
> });
> var upload = multer({
> 	storage: storage
> });
> ```
> 
> # �����ļ�
> `upload.single('xxx')`��xxx����е�name���Ե�ֵ��Ӧ
> ������Ȼ�õ�post���󣬵�ʵ���ϲ���Ҫ`bodyParser`ģ�鴦��
> 
> ```js
> app.post('/upload-single', upload.single('logo'), function(req, res, next) {
> 	console.log(req.file)
> 	console.log('�ļ����ͣ�%s', req.file.mimetype);
> 	console.log('ԭʼ�ļ�����%s', req.file.originalname);
> 	console.log((req.file.originalname).split("."))
> 	console.log('�ļ���С��%s', req.file.size);
> 	console.log('�ļ�����·����%s', req.file.path);
> 	res.send({
> 		ret_code: '0'
> 	});
> });
> ```
> 
> # ��ͼ�ϴ�
> ��ͼ�ϴ�ֻҪ����һ�µط���ǰ����file�����Ӷ�һ��`multiple="multiple"`����ֵ����ʱ�Ϳ�����ѡͼ��ʱ���ѡ�ˣ���ȻҲ���Բ��ж��file�����(���Ƽ�����ϴ�ͼƬ�����)����������᲻��
> 
> ```html
> <input type="file" name="logo" multiple="multiple" />
> ```
> 
> ���Ҳ��Ҫ��Ӧ�ĸı�
> 
> ```js
> app.post('/upload-single', upload.single('logo'), function(req, res, next) {
> //upload.single('logo')��Ϊupload.array('logo', 2)�����ִ�����Խ��ܶ�����ͼƬ
> app.post('/upload-single', upload.array('logo', 2), function(req, res, next) {
> ```
> 
> ���������ͼƬ�����ϴ����ƣ����ǿ�����`upload.any()`����
> 
> ```js
> app.post('/upload-single', upload.any(), function(req, res, next) {	
> 	res.append("Access-Control-Allow-Origin","*");
> 	res.send({
> 		wscats_code: '0'
> 	});
> });
> ```
> 
> # ǰ�˲���
> ## formData���ύ
> ```html
> <form action="http://localhost:3000/upload-single" method="post" enctype="multipart/form-data">
> 	<h2>��ͼ�ϴ�</h2>
> 	<input type="file" name="logo">
> 	<input type="submit" value="�ύ">
> </form>
> ```
> 
> ## formData��+ajax�ύ
> ```html
> <form id="uploadForm">
> 	<p>ָ���ļ����� <input type="text" name="filename" value="" /></p>
> 	<p>�ϴ��ļ��� <input type="file" name="logo" /></ p>
> 	<input type="button" value="�ϴ�" onclick="doUpload()" />
> </form>
> ```
> 
> `FormData`�����ǿ���ʹ��һϵ�еļ�ֵ����ģ��һ�������ı���Ȼ��ʹ��`XMLHttpRequest`�������"��"
> 
> **ע���**
> 
> * processData����Ϊfalse����Ϊdataֵ��FormData���󣬲���Ҫ������������
> * `<form>`��ǩ���`enctype="multipart/form-data"`���ԡ�
> * cache����Ϊfalse���ϴ��ļ�����Ҫ���档
> * contentType����Ϊfalse����Ϊ����`<form>`�������FormData�������Ѿ�����������`enctype="multipart/form-data"`��������������Ϊfalse
> 
> �ϴ��󣬷������˴�����Ҫʹ�ôӲ�ѯ������Ϊlogo��ȡ�ļ�������������Ϊ`<input>`����������`name="logo"`
> 
> ```js
> function doUpload() {
> 	$.ajax({
> 		url: 'http://localhost:3000/upload-single',
> 		type: 'POST',
> 		cache: false, //������
> 		data: new FormData($('#uploadForm')[0]),
> 		processData: false,//����
> 		contentType: false,//����
> 		success: function(data) {
> 			console.log(data)
> 		}
> 	})
> }
> ```
> 
> ## �ı���ʽ
> �����������ļ��ϴ������
> 
> ```html
> <form id="uploadForm">
> 	<input style="display: none;" type="file" name="logo" onchange="doUpload()" multiple="multiple" />
> </form>
> ```
> 
> Ϊ��Ҫ�����ļ��ϴ��ı�ǩ��ӵ���¼�
> 
> ```js
> <img onclick="uploadImg()" class="headpic" src="" />
> function uploadImg(){
> 	$("#uploadForm input").trigger("click");//�����ļ��ϴ����¼�
> }
> //����������Ļ���ϴ��¼�
> function doUpload() {
>         //upload code
> }
> ```
> 
> # Я����������
> ������ԭ����append�����������������ݣ��ȿ����ϴ�ͼƬҲ���Դ���������
> 
> ```js
> //����form���� 
> var data = new FormData();
> data.append("avatar", fileNode.files[0]);
> data.append("description", "��������");
> ```
> 
> # �ο��ĵ�
> [Github MyDemo](https://github.com/Wscats/node-tutorial/tree/master/uploadFiles)
> [Github Multer](https://github.com/expressjs/multer)
> [MDN FormData�����ʹ��](https://developer.mozilla.org/zh-CN/docs/Web/API/FormData/Using_FormData_Objects)

