## 某些时候我们既要到github上找轮子，又需要保持公司内部git与电脑的连接。此时就需要配置多账号 否则你的ssh key就会频繁更改。

**备注：**所有执行命令的地方请在管理员模式下进行，即打开**cmd，Git Bash**客户端**用管理员身份运行程序。**

### 1. 生成github.com对应的私钥公钥(我是在git客户端直接生产key)

#### 先**cd ~/.ssh**到此目录后   **ssh-keygen -t rsa -C  你的邮箱**

### 2. 同样的方式生产公司git所要的的私钥公钥 (邮箱地址可以相同可以不同)

执行命令**ssh-keygen -t rsa -C email**  创建sshkey，命名为**id_rsa_home** (命名随便)

### 3.由于是在git的 ~/.ssh目录下创建的所以这是git默认访问的.ssh目录。除了秘钥文件之外，**config**文件是后面的步骤中手动生产的，**known_hosts**文件是后续自动生产的。（在cd ~/.ssh后 输入pwd可以查看~/.ssh所在的目录）

![git-1](https://github.com/PandoraSB0X/record/blob/master/note/img/git/git-1.png?raw=true)

###  4.把github对应的公钥和公司git对应的公钥上传到服务器(步骤和github添加公钥差不多)

### 5. 在.ssh目录创建config文本文件并完成相关配置(最核心的地方)

##### 每个账号单独配置一个**Host**，每个**Host**要取一个别名，每个Host主要配置**HostName**和**IdentityFile**两个属性即可

##### **config文件配置如下：**

```js
# 配置github.com
Host github.com                 
    HostName github.com
    IdentityFile ~/.ssh/id_rsa

# 配置git.gitlab.net 
Host gitlab.com 
    HostName gitlab.com 
    IdentityFile ~/.ssh/id_rsa_gitlab
    
HostName 　　　　　　　   这个是真实的域名地址
IdentityFile 　　　　　　　  这里是id_rsa的地址
PreferredAuthentications   配置登录时用什么权限认证--可设为publickey,password publickey,keyboard-interactive等
User 　　　　　　　　　　　配置使用用户名

```

### 6. 打开Git Bash客户端（管理员身份运行）执行测试命令测试是否配置成功（会自动在.ssh目录生成known_hosts文件把私钥配置进去）

### 7. 测试成功之后就可以在电脑上同时使用git,多账号同时操作，互不影响了.

[参考文档](https://www.cnblogs.com/popfisher/p/5731232.html) 	[参考文档2](https://blog.csdn.net/iceking66/article/details/80563716)