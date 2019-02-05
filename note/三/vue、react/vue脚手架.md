## 一、vue脚手架安装步骤

https://cli.vuejs.org/

#### 1.全局安装

```bash
npm install -g @vue/cli
```

#### 2.安装完，会在全局有vue命令

```bash
vue -V
```

#### 3.创建项目

```bash
vue create weibo
```

#### 4.定位到该文件夹

```
cd weibo

```

#### 5.启动服务器

```
npm run serve

```



- 利用路由传递参数

```
this.$route.push({path:'/xxx',query:{id:1}});//类似get传参，通过URL传递参数
this.$route.push({path:'/xxx',params:{id:1}});//类似post传参

```

- 接收参数

```
this.$route.query.id
this.$route.params.id

```

- 利用emit发送数据

```
this.$emit('showCityName',data);

```

- 利用on接收数据

```
this.$on('increment',function(msg){
                //获取$emit方法传递的第二个参数
                console.log(msg);
                alert("1");
            })

```