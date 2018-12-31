

# git常用命令及手动关联git本地和远端仓库

## 1、关联git本地和远端仓库步骤

1. 打开git，输入mkdir newProject 新建一个文件夹。
2. git init 初始化本地文件夹为一个可以管理的git仓库。
3. 关联本地仓库和远端仓库：git remote add origin [http://$](https://link.juejin.im?target=http%3A%2F%2F%24){path}.git.   (如果是从远端仓库克隆下来那么本地仓库和远端仓库已经自动完成关联)
4. 把文件放入本地仓库 
   - git status          // 列出没有被git管理或者修改但还没有未被提交的文件(如果有可视化工具此处很可观的可以观察到那些文件未提交)
   - git add .           // 将未被管理的文件添加到git
   - git commit -m "提交文件"
5. 把本地库推送到远端仓库 
   - git push -u origin master
     - ps：当远端仓库使用Readme文件初始化项目，需要先git pull origin master，有固定格式时需手动编辑，按i修改，:wq退出		(  shift+:    即可输入)
6. 切换本地开发分支并管理远端分支 
   - git checkout -b topic      // 创建并切换到topic新分支，相当于git branch topic 和git checkout topic 组合
   - git push origin topic:topic       // 关联本地topic分支和远端topic分支 （没有将自动创建topic分支并关联）

## 2、git 常用命令

- 开发四部曲。 
  1. git add .
  2. git commit -m "commit"
  3. git pull origin master
  4. git push origin master
- 代码冲突。 （推荐使用可视化工具解决冲突）
  1. 解决冲突
  2. git add .
  3. git rebase --continue （或者再次git commit）
  4. git push origin master
- git 分支管理 
  - git fetch （-p）               // branch在服务器上的最新状态
  - git branch (-a)                 // 查看所有branch
  - git branch newBranch     // 本地创建branch
  - git checkout branch         // 切换branch
  - git checkout -b topic      // 创建并切换到topic新分支
  - git push origin topic:topic       // 关联本地topic分支和远端topic分支
  - git branch --set-upstream-to=origin/topic topic      //设置本地topic的上游及远端分支（设置之后git pull将默认从远端topic分支可拉取代码，git push将默认推送代码到远端topic分支）
- git版本管理 
  1. git reset --hard HEAD^             // 回退上一个版本
  2. git reset --hard HEAD~3            // 回退上三个版本
  3. git reset --hard 版本号            // 回退指定版本
- git远端版本回退 
  1. git checkout  target_branch             // 切换到需要回滚的分支
  2. git pull		                                                    //更新代码
  3. git branch target_branch_copy            //备份一下这个分支当前的情况
  4. git reset --hard target_commit_id    //把target_branch本地回滚到target_commit_id
  5. git push origin :target_branch             //删除远程 target_branch
  6. git push origin target_branch            //用回滚后的本地分支重新建立远程分支
  7. git push origin :target_branch_copy       //如果前面都成功了，删除这个备份分支
- 重命名 
  1. git mv oldName newName
  2. git status
  3. 可以看到rename的提示，此时正常提交即可。