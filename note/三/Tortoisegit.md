# Tortoisegit使用方法

### 1、按顺序安装安装包

([小乌龟下载地址](https://tortoisegit.org/download/) 下载好安装包和汉化包，先安装安装包再安装汉化包)

### 2、设置中文

![设置中文](https://github.com/PandoraSB0X/record/blob/master/note/img/Tortoisegit-1.gif?raw=true)





### 利用Tortoisegit解决冲突

![img](https://github.com/PandoraSB0X/record/blob/master/note/img/Tortoisegit-2.png?raw=true)





例如以上的界面左上角是远端拉下来的，右上角是本地的，红色的代表冲突部分，把需要代码复制到下面的框内，

然后保存时 标记冲突解决  再commit冲突就解决完成了。(请注意所有冲突部分是否修改完毕再进行保存)

### 利用Tortoisegit设置外部解决冲突程序解决冲突

![冲突解决](https://github.com/PandoraSB0X/record/blob/master/note/img/%E5%B7%AE%E5%BC%82%E6%9F%A5%E7%9C%8B%E5%99%A8%20.jpg?raw=true)



![冲突解决工具](https://github.com/PandoraSB0X/record/blob/master/note/img/%E5%86%B2%E7%AA%81%E8%A7%A3%E5%86%B3%E5%B7%A5%E5%85%B7.jpg?raw=true)



### 设置合并工具这里我设置的是vscode,利用vscode进行冲突处理

![vscode](https://github.com/PandoraSB0X/record/blob/master/note/img/%E5%B7%AE%E5%BC%82%E6%9F%A5%E7%9C%8B%E5%99%A8%20.jpg?raw=true)

![vscode解决冲突](https://github.com/PandoraSB0X/record/blob/master/note/img/Tortoisegit-3.png?raw=true)



![1546235071(F:\record\笔记\img\1546235071(1).jpg)](https://github.com/PandoraSB0X/record/blob/master/note/img/Tortoisegit-4.jpg?raw=true)



### 首先双击红色冲突文件，解决冲突代码，在提交的时候把#后的东西删除并提交再推送远端那么冲突就解决完成了



### 如果遇到上传无权限问题，请设置好您的ssh key 并且在可视化设置ssh客户端

![](https://github.com/PandoraSB0X/record/blob/master/note/img/Tortoisegit-5.jpg?raw=true)

### 一般来说都使用的是git的安装目录下的   usr\bin 的ssh.exe文件



