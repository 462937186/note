> # ��װ����
> ��`Mongodb`�����������°汾��[Mongodb���ص�ַ](https://cloud.mongodb.com/)
> 
> ����`msi`��`window`��װ��������װ��C�̻���D��Ŀ¼��
> 
> # ����
> �������ǰ�װ��D�̵Ļ�����
> 
> ```shell
> D:\Program Files (x86)\MongoDB\Server\3.2\bin
> ```
> 
> ������bin�ļ������ҵ�mongod.exe���Ȼ��ͨ������Աִ��`mongod --dbpath x·��x`��·���������κεط���������ѡ����D�̵�MongoDBĿ¼�£���Ȼ·����Ҫ����������ַ���������`Program Files (x86)`Ҳ����
> 
> ```shell
> mongod --dbpath D:\mongodb\data\db
> ```
> 
> ![image](https://user-images.githubusercontent.com/17243165/31977540-fc0a5a6e-b96f-11e7-9a2b-34d66d7241c4.png)
> 
> # ������
> �������������֮�󣬾Ϳ��Է���binĿ¼���ҵ�`mongo.exe`���������Ա��ִ�У��Ϳ��Գ���mongodb��������ģʽ
> 
> ```shell
> D:\Program Files (x86)\MongoDB\Server\3.2\bin
> ```
> 
> ![image](https://user-images.githubusercontent.com/17243165/31978099-57bce3ca-b972-11e7-88bd-30f5d68036ed.png)
> 
> Ȼ��Ϳ���ʹ�������������������
> 
> ```js
> db.help()//����
> db.stats()//ͳ��
> ```
> 
> # ��ʾ���ݿ�
> ```js
> show dbs
> ```
> 
> ��鵱ǰѡ������ݿ�
> 
> ```js
> db
> ```
> 
> # ������ݿ�
> **���ݿ���**Ϊ���ݿⴴ�������֣�ʹ�ø�������Ĭ���л�����Ӧ�����ݿ⣬���������ݿ������ѡ����ݿ���Ϣ����ʾ�����Ĭ�Ͼ��и����ݿ⣬�Ǿ����л�����Ӧ�����ݿ�����
> 
> ```js
> use ���ݿ���
> ```
> 
> # ɾ�����ݿ�
> ���л�����Ӧ�����ݿ⣬Ȼ����ִ��`db.dropDatabase()`ɾ�������ݿ�
> 
> ```js
> use ���ݿ���
> //switched to db ���ݿ���
> db.dropDatabase()
> ```
> 
> # ��ʾ����
> ��һ��������Լ�鴴���ļ���
> 
> ```js
> show collections
> ```
> 
> # ��Ӽ���
> �ڴ��������ݿ�֮�����ǾͿ��Դ�������
> 
> ```js
> db.createCollection(��������name�����ò���options[��������])
> ```
> 
> **name**��Ҫ�����ļ��ϵ����ơ� **options**��һ���ĵ�������ָ�����ϵ�����
> 
> ����	����	����
> name	String	Ҫ�����ļ��ϵ�����
> options	Document	(��ѡ)ָ���й��ڴ��С��������ѡ��
> **options**�����ǿ�ѡ�ģ����ֻ��Ҫָ�����ϵ����ơ� �����ǿ���ʹ�õ�ѡ���б�
> 
> �ֶ�	����	����
> capped	Boolean	(��ѡ)���Ϊtrue�������÷�յļ��ϡ����޼����ǹ̶���С�ļ��ϣ����ڴﵽ������Сʱ�Զ���������ɵ���Ŀ�� ���ָ��true������Ҫָ��size������
> autoIndexId	Boolean	(��ѡ)���Ϊtrue������_id�ֶ����Զ�����������Ĭ��ֵΪfalse��
> size	����	(��ѡ)ָ�����޼��ϵ�����С(���ֽ�Ϊ��λ)�� ���cappedΪtrue����ô����Ҫָ�����ֶε�ֵ��
> max	����	(��ѡ)ָ�����޼��������������ĵ�����
> ����**option**�ǿ�ѡ������Ҳ���Բ��������������
> 
> ```js
> db.createCollection("mycollection")
> ```
> 
> # ɾ������
> `db.collection.drop()`���ڴ����ݿ���ɾ������
> 
> ```js
> db.������.drop()
> ```
> 
> �������ǿ��Բ������²���
> 
> ```js
> db.createCollection("wscats")//������Ϊwscats�ļ���
> show collections//��ʾ�����ݿ����м���   wscats
> db.wscats.drop()//ɾ����Ϊwscats�ļ���
> ```
> 
> # �鿴�ĵ�
> ��򵥲鿴�ĵ��ķ�������`find()`����������������е��ĵ����
> 
> ```js
> db.������.find()
> ```
> 
> Ҫ�Ը�ʽ���ķ�ʽ��ʾ���������ʹ��`pretty()`������
> 
> ```js
> db.������.find().pretty()
> ```
> 
> ## 1.��ֵѰ��
> Ѱ��age�����������к�������ֵΪwscats���ĵ�������൱��`where name = 'wscats'`
> 
> ```js
> db.age.find({name:"wscats"})
> ```
> 
> ## 2.��ֵѰ��
> ����	�﷨	ʾ��	��Ч���
> ���	{:}	`db.age.find({"name":"wscats"}).pretty()`	where name = 'wscats'
> С��	{:{$lt:}}	`db.age.find({"likes":{$lt:50}}).pretty()`	where likes < 50
> С�ڵ���	{:{$lte:}}	`db.age.find({"likes":{$lte:50}}).pretty()`	where likes <= 50
> ����	{:{$gt:}}	`db.age.find({"likes":{$gt:50}}).pretty()`	where likes > 50
> ���ڵ���	{:{$gte:}}	`db.age.find({"likes":{$gte:50}}).pretty()`	where likes >= 50
> ������	{:{$ne:}}	`db.age.find({"likes":{$ne:50}}).pretty()`	where likes != 50
> ## 3.AND��ORѰ��
> ### AND
> ��find()�����У����ͨ��ʹ��`��`�����Ƿֿ����ݶ��������mongodb������Ϊ**AND**������ ������AND�Ļ����﷨
> 
> Ѱ��`_id`Ϊ1����`name`Ϊwscats�����н����
> 
> ```js
> db.age.find(
>    {
>       $and: [
>          {"_id": 1}, {"name": "wscats"}
>       ]
>    }
> )
> ```
> 
> ### OR
> ��Ҫ����OR������ѯ�ĵ�����Ҫʹ��`$or`�ؼ��֡�������OR�����Ļ����﷨
> 
> Ѱ��`name`Ϊcorrine����`name`Ϊwscats�����н����
> 
> ```js
> db.age.find(
>    {
>       $or: [
>          {"name": "corrine"}, {��name��: "wscats"}
>       ]
>    }
> )
> ```
> 
> ### AND��OR�Ƚ��
> �൱�����`where title = "wscats" OR ( title = "corrine" AND _id < 5)`
> 
> ```js
> db.age.find({
>   $or: [{
>     "title": "wscats"
>   }, {
>     $and: [{
>       "title": "corrine"
>     }, {
>       "_id": {
>         $lte: 5
>       }
>     }]
>   }]
> })
> ```
> 
> # �����ĵ�
> �ĵ������ݽṹ��JSON����һ����
> ���д洢�ڼ����е����ݶ���BSON��ʽ��
> BSON��һ����json��һ�ֶ�������ʽ�Ĵ洢��ʽ,���**Binary JSON**��
> 
> Ҫ�����ݲ��뵽mongodb�����У���Ҫʹ��mongodb��`insert()`��`save()`������
> 
> ```js
> db.������.insert(document)
> ```
> 
> �������ǿ��Բ�����������
> 
> ```js
> db.wscats.insert({
>    _id: 100,
>    title: 'MongoDB Tutorials', 
>    description: 'node_tutorials',
>    by: 'Oaoafly',
>    url: 'https://github.com/Wscats/node-tutorial',
>    tags: ['wscat','MongoDB', 'database', 'NoSQL','node'],
>    num: 100,
> })
> ```
> 
> Ҳ����֧�ֲ�������ע�⴫�����������ʽ
> 
> ```js
> db.wscats.insert([{
>    _id: 100,
>    title: ��Hello��
> },{
>    _id: 101,
>    title: ��World��
> }])
> ```
> 
> �ڲ�����ĵ��У������ָ��_id��������ômongodb��Ϊ���ĵ�����һ��Ψһ��ObjectId
> Ҫ�����ĵ���Ҳ����ʹ��`db.post.save(document)`����������ĵ���ָ��_id����ô`save()`��������`insert()`����һ���Զ�����ID��ֵ�����ָ��_id������save()��������ʽ�滻����**_id**���ĵ���ȫ�����ݡ�
> 
> ```js
> db.wscats.save({
>    _id: 111,
>    title: 'Oaoafly Wscats', 
> })
> ```
> 
> # �����ĵ�
> ## 1.update()����
> Ѱ�ҵ�һ��titleΪwscats��ֵ�����Ҹ���ֵtitleΪcorrine��ageΪ12
> 
> ```js
> db.age.update({
>   'title': 'wscats'
> }, {
>   $set: {
>     'title': 'corrine',
>     'age': 12
>   }
> })
> ```
> 
> Ĭ������£�mongodbֻ�����һ���ĵ���Ҫ���¶���ĵ�����Ҫ������`multi`����Ϊtrue�����������find��������ĸ��ָ��������ж���ɸѡ�����Ȼ����¶���ĵ�
> 
> Ѱ������titleΪwscats��ֵ�����Ҹ���ֵtitleΪcorrine��ageΪ12
> 
> ```js
> db.age.update({
>   'title': 'wscats'
> }, {
>   $set: {
>     'title': 'corrine',
>     'age': 12
>   }
> }, {
>   multi: true
> })
> ```
> 
> ## 2.save()����
> ��`_id`����Ϊ3���ĵ��������µ�ֵ��ע��`_id`Ϊ�ش�
> 
> ```
> db.age.save({
>   '_id':3,
>   'title': 'wscats'
> })
> ```
> # ɾ���ĵ�
> ɾ������`_id`Ϊ3���ĵ���Ĭ����ɾ������
> 
> ```js
> db.age.remove({
>   '_id':3
> })
> ```
> 
> ������ִ��`remove()`����ǰ��ִ��`find()`�������ж�ִ�е������Ƿ���ȷ
> 
> �����ֻ��ɾ����һ���ҵ��ļ�¼��������**justOne**Ϊ1��������ʾ
> 
> ```js
> db.age.remove({...},1)
> ```
> 
> ȫ��ɾ��
> 
> ```js
> db.age.remove({})
> ```
> 
> # Limit��Skip����
> ## Limit
> �������Ҫ��mongodb�ж�ȡָ�����������ݼ�¼������ʹ��mongodb��Limit������`limit()`��������һ�����ֲ������ò���ָ����mongodb�ж�ȡ�ļ�¼������
> 
> ```js
> db.age.find().limit(����)
> ```
> 
> ## Skip
> ���ǳ��˿���ʹ��`limit()`��������ȡָ�������������⣬������ʹ��`skip()`����������ָ�����������ݣ�skip����ͬ������һ�����ֲ�����Ϊ�����ļ�¼������
> 
> ```js
> db.age.find().limit(����).skip(����)
> //skip()����Ĭ��ֵΪ0
> ```
> 
> ����������ʵ�ַ�ҳ��ʱ��Ϳ�����limit������ÿҳ����������(һ��̶�һ��ֵ)����skip��������ʾ�ڼ�ҳ(һ���й��ɱ䶯��ֵ)
> 
> # ����
> ��mongodb��ʹ��ʹ��`sort()`���������ݽ�������`sort()`��������ͨ������ָ��������ֶΣ���ʹ��1��-1��ָ������ķ�ʽ������1Ϊ�������У���-1�����ڽ������С�
> 
> 1	��������
> -1	��������
> ```js
> db.������.find().sort({��ֵ(����ֵ):1})
> ```
> 
> ��`age`���ϱ����¸���`_id`�������н�������
> 
> ```js
> db.age.find().sort({
>   "_id": -1
> })
> ```
> 
> # Node.js����
> ��װmongodb��ģ��
> 
> ```js
> npm install mongodb
> ```
> 
> ## 1.�������ݿ�
> ```js
> var MongoClient = require('mongodb').MongoClient;
> //��β��ѡ�����ݿ���
> var DB_CONN_STR = 'mongodb://localhost:27017/wscats';
> MongoClient.connect(DB_CONN_STR, function(err, db) {
>   console.log("���ӳɹ���");
> });
> ```
> 
> ## 2.��ѯ����
> ע���ѯ�����Ľ����ҪtoArray����������
> 
> ```js
> var MongoClient = require('mongodb').MongoClient;
> var DB_CONN_STR = 'mongodb://localhost:27017/wscats';
> 
> MongoClient.connect(DB_CONN_STR, function(err, db) {
>   console.log("���ӳɹ���");
>   //ѡ��age���ϣ�����find�����ѽ�����û������д���
>   db.collection("age").find({title: "cba"}).toArray(function(err, result) {
>     if (err) {
>       console.log('Error:' + err);
>       return;
>     }
>     console.log(result);
>   });
> });
> ```
> 
> ## 3.��������
> insert������һ����������Ҫ�����ֵ(����һ��Ҳ���Զ��)���ڶ��������ǽ���һ���ص���������ֵ����ɹ���ط��ز���ֵ��һЩ�ؼ���Ϣ������`_id`
> 
> ```js
> var MongoClient = require('mongodb').MongoClient;
> var DB_CONN_STR = 'mongodb://localhost:27017/wscats';
> 
> MongoClient.connect(DB_CONN_STR, function(err, db) {
>   console.log("���ӳɹ���");
>   db.collection("age").insert([
>     {
>       title: "�����ֵA"
>     }, {
>       title: "�����ֵB"
>     }
>   ], function(err, result) {
>     if (err) {
>       console.log('Error:' + err);
>       return;
>     }
>     console.log(result)
>   })
> });
> ```
> 
> ## 4.��������
> ע���������$set������ȫ�滻ԭ�����Ƿ�(û�����õ�����ֵ���ᶪʧ)������$set��ֻ�Ǹ��¶�Ӧ������ֵ�����಻���ı�
> 
> ```js
> var MongoClient = require('mongodb').MongoClient;
> var DB_CONN_STR = 'mongodb://localhost:27017/wscats';
> 
> MongoClient.connect(DB_CONN_STR, function(err, db) {
>   console.log("���ӳɹ���");
>   db.collection("age").update({
>     "_id": 1
>   }, {
>     $set: {
>       title: "��ã�����",
>       skill: "js"
>     }
>   }, function(err, result) {
>     if (err) {
>       console.log('Error:' + err);
>       return;
>     }
>     //console.log(result);
>   });
> });
> ```
> 
> ## 5.ɾ������
> ```js
> var MongoClient = require('mongodb').MongoClient;
> var DB_CONN_STR = 'mongodb://localhost:27017/wscats';
> 
> MongoClient.connect(DB_CONN_STR, function(err, db) {
>   console.log("���ӳɹ���");
>   db.collection("age").remove({
>     "_id": 1
>   }, function(err, result) {
>     if (err) {
>       console.log('Error:' + err);
>       return;
>     }
>     //console.log(result);
>     //�ر����ݿ�
>     db.close();
>   });
> });
> ```
> 
> ## 6.�ر����ݿ�
> ```js
> db.close();
> ```
> 
> # ��װ�Զ���ģ��
> �½�`mongo.js`д�����´��룬��װ�Զ���ģ�飬��������·�ɸ��ã�ע��`assert`��node�Դ��Ķ���ģ�飬���ڲ��Դ���
> 
> �ο�
> 
> * [����API�ĵ�](http://nodejs.cn/api/assert.html)
> * [Node.js�Ķ���ģ��assert���е�Ԫ����](https://www.cnblogs.com/hong7zai/p/5909914.html)
> 
> ```js
> const MongoClient = require('mongodb').MongoClient;
> const assert = require('assert');
> const url = 'mongodb://localhost:27017';
> const dbName = 'shop';
> function query(callback) {
> 	MongoClient.connect(url, function(err, client) {
> 		assert.equal(null, err);
> 		console.log("Connected successfully to server");
> 		const db = client.db(dbName);
> 		callback(db);
> 		client.close();
> 	});
> }
> module.exports = {
> 	query
> }
> ```
> 
> ��·���ļ��������ʹ��
> 
> ```js
> var mongo = require('./mongo.js')
> router.post('/addproduct', function(req, res, next) {
> 	mongo.query(function(db) {
> 		db.collection("product").insertMany([req.body], function(err, result) {
> 			console.log("Inserted 1 document into the collection");
> 			res.send('respond with a resource');
> 		});
> 	})
> });
> ```
> 
> # ���ӻ�
> * [Robo 3T](https://robomongo.org/)
> * [Studio3t](https://studio3t.com/download-thank-you/?OS=win64)
> 
> # �ο��ĵ�
> * [�װ�-MongoDB�̳�](http://www.yiibai.com/mongodb/)
> * [����-MongoDB�̳�](http://www.runoob.com/mongodb/mongodb-tutorial.html)

