### 前端解决跨域问题之nginx代理

##### （Visual Studio Code 用的本地启动服务端口的插件名称	GO Live	 端口为http://127.0.0.1:5500/）

#### 一、下载nginx（https://nginx.org/en/download.html）

#### 二、以管理员身份设置 本机hosts文件

##### 	C:\Windows\System32\drivers\etc 根目录

##### 	hosts文件添加本地域名127.0.0.1 yun.localhost

#### 三、nginx文件夹conf 创建文件夹及新文件  serv   yun.localhost

#### 四、nginx.conf 引入新建的文件include serv/yun.localhost;

#### 五、在yun.localhost 配置端口


```js
server{
    listen 80;
    server_name yun.localhost;
    proxy_set_header upgrade $http_upgrade;
    proxy_set_header connection "upgrade";
   
	location / {
    	proxy_pass http://127.0.0.1:5500/;
	}
     //这些按后端给的接口文档里的接口配置 proxy_pass 是后端端口配置完成后重启nginx 
    // nginx -s reload 重启服务
    //然后在postman上测一下
	location /screen {
    	proxy_pass http://192.168.11.118:6009;
	}
	location /department {
    	proxy_pass http://192.168.11.118:6009;
	}
}
```


#### 六、nginx.conf 清除默认配置



![1](https://github.com/PandoraSB0X/record/blob/master/%E7%AC%94%E8%AE%B0/img/2019-01-27_002915.png?raw=true)

##### 访问的时候直接利用配好的端口加路径  yun.localhost/pages/management/management.html

#### nginx的作用不只有这一点但是前端为了解决开发中的跨域问题上述配置已经足够，更多更详细的配置还需要继续学习。。。。







