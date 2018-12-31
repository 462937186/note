> `git log`
> 查看我们修改过的历史记录
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448659/a9cfb052-1f9a-11e6-8564-c1f7d960fa14.png)
>
> `git reset --hard commit id`
> 这是回退到某个版本，commit id号可以只是截取开始的一部分
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448681/f8c2102e-1f9a-11e6-86a2-0e84cd75510b.png)
>
> `dir`
> 查看文件夹目录里面的所有文件
>
> `cat`
> 打印某个文件
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448689/41ce494a-1f9b-11e6-9b67-6d709e492d85.png)
>
> `git reflog`
> 查看记录你执行过的每一次命令
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448814/e7b0beb2-1f9e-11e6-914b-fb18afb76dc1.png)
>
> `git checkout`
>
> `git checkout -b dev`
>
> 切换到某个分支
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448702/b1787d56-1f9b-11e6-8ffc-5dd1102d7554.png)
>
> `git status`
> push前看看修改过了什么文件
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448704/c37566c2-1f9b-11e6-9481-512800fc3955.png)
>
> `git branch -d xxxx`
> 删除本地分支，注意在当前这个分支不能删除自己，只能切换到其他分支再删除当前的这个分支
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448710/f3f80f3e-1f9b-11e6-8044-434fecc81810.png)
>
> `git branch -a`
> 查看本地和远程分支
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448737/7e299984-1f9c-11e6-96e4-e8a3bbbbd54c.png)
>
> `git merge xxx`
> 合并xxx分支到当前分支
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448802/b435b40c-1f9e-11e6-9b58-c417ead4b55d.png)
>
> `git add [<file>]`
> 添加文件到缓存区，也可以 "git add ." 添加所有文件到缓存
> ![image](https://camo.githubusercontent.com/7a97d48299c1b3e14ec871e066dd83351d83a1a1/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313630363031313733353032393037)
>
> `git diff [<file>]`
> 比较当前文件和暂存区文件差异
> ![image](https://camo.githubusercontent.com/053f2bc2153f1af068403db02c78f460862dc76c/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313630363032313034373134303536)
>
> `git checkout [<file>]`
> 回滚指定文件
> ![image](https://cloud.githubusercontent.com/assets/17243165/15766871/b602ea8a-2975-11e6-81d7-e9212f01b041.png)
>
>
>
> 删除
>
> ` rm test.txt`
>
> 这个时候，Git知道你删除了文件，因此，工作区和版本库就不一致了，`git status`命令会立刻告诉你哪些文件被删除了：
>
> ```js
> $ git status
> On branch master
> Changes not staged for commit:
>   (use "git add/rm <file>..." to update what will be committed)
>   (use "git checkout -- <file>..." to discard changes in working directory)
> 
>     deleted:    test.txt
> 
> no changes added to commit (use "git add" and/or "git commit -a")
> ```
>
> 现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令`git rm`删掉，并且`git commit`：
>
> ```js
> $ git rm test.txt
> rm 'test.txt'
> 
> $ git commit -m "remove test.txt"
> [master d46f35e] remove test.txt
>  1 file changed, 1 deletion(-)
>  delete mode 100644 test.txt
> ```
>
>

