> `git log`
> �鿴�����޸Ĺ�����ʷ��¼
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448659/a9cfb052-1f9a-11e6-8564-c1f7d960fa14.png)
>
> `git reset --hard commit id`
> ���ǻ��˵�ĳ���汾��commit id�ſ���ֻ�ǽ�ȡ��ʼ��һ����
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448681/f8c2102e-1f9a-11e6-86a2-0e84cd75510b.png)
>
> `dir`
> �鿴�ļ���Ŀ¼����������ļ�
>
> `cat`
> ��ӡĳ���ļ�
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448689/41ce494a-1f9b-11e6-9b67-6d709e492d85.png)
>
> `git reflog`
> �鿴��¼��ִ�й���ÿһ������
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448814/e7b0beb2-1f9e-11e6-914b-fb18afb76dc1.png)
>
> `git checkout`
>
> `git checkout -b dev`
>
> �л���ĳ����֧
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448702/b1787d56-1f9b-11e6-8ffc-5dd1102d7554.png)
>
> `git status`
> pushǰ�����޸Ĺ���ʲô�ļ�
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448704/c37566c2-1f9b-11e6-9481-512800fc3955.png)
>
> `git branch -d xxxx`
> ɾ�����ط�֧��ע���ڵ�ǰ�����֧����ɾ���Լ���ֻ���л���������֧��ɾ����ǰ�������֧
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448710/f3f80f3e-1f9b-11e6-8044-434fecc81810.png)
>
> `git branch -a`
> �鿴���غ�Զ�̷�֧
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448737/7e299984-1f9c-11e6-96e4-e8a3bbbbd54c.png)
>
> `git merge xxx`
> �ϲ�xxx��֧����ǰ��֧
> ![image](https://cloud.githubusercontent.com/assets/17243165/15448802/b435b40c-1f9e-11e6-9b58-c417ead4b55d.png)
>
> `git add [<file>]`
> ����ļ�����������Ҳ���� "git add ." ��������ļ�������
> ![image](https://camo.githubusercontent.com/7a97d48299c1b3e14ec871e066dd83351d83a1a1/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313630363031313733353032393037)
>
> `git diff [<file>]`
> �Ƚϵ�ǰ�ļ����ݴ����ļ�����
> ![image](https://camo.githubusercontent.com/053f2bc2153f1af068403db02c78f460862dc76c/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313630363032313034373134303536)
>
> `git checkout [<file>]`
> �ع�ָ���ļ�
> ![image](https://cloud.githubusercontent.com/assets/17243165/15766871/b602ea8a-2975-11e6-81d7-e9212f01b041.png)
>
>
>
> ɾ��
>
> ` rm test.txt`
>
> ���ʱ��Git֪����ɾ�����ļ�����ˣ��������Ͱ汾��Ͳ�һ���ˣ�`git status`��������̸�������Щ�ļ���ɾ���ˣ�
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
> ������������ѡ��һ��ȷʵҪ�Ӱ汾����ɾ�����ļ����Ǿ�������`git rm`ɾ��������`git commit`��
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

