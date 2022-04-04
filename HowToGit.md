软件安装

https://git-scm.com/download

初始化

```
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

创建版本库

```
进入库文件夹（目录）下右键Git Bash Here
git init
```

修改与提交

```
git add filename
git commit -m "注释说明"
```

查看提交日志

```
git log
或 git log --pretty=oneline  //单行显示
```

版本回退

```
git reset --hard head^  //一个^代表回退到上一个版本
git reset --hard head^^  //两个^回退到上上一个版本，以此类推
git reset --hard head~10  //回退到往前十个版本
```

版本还原

```
git reset --hard f92b5  //commit id的位数要求只要能区分即可
```

Git的版本切换其实是挪动`HEAD`指针，`HEAD`指向的版本就是当前版本

查看命令历史，便于找到因为版本变化而丢失的commit记录

```
git reflog
```



工作区中里的隐藏目录 `.git` 其实是版本库（Repository）。版本库里有暂存区stage（或index），以及Git自动创建的第一个分支`master`，指向master的第一个指针即为`HEAD`。

![git-repo](E:\FLY\MyRepository\image\0)

当我们把文件往Git版本库中添加时需要两步走：

第一步：`git add`实际上就是将文件修改添加到缓存区；

第二步：`git commit`实际上就是将缓存区的所有内容提交到当前分支（仓库）。



```
git status
```

做两次对比，对比工作区与暂存区，再对比暂存区与仓库，若不同则输出差别，若相同则输出`clean`。

例如：

<img src="E:\FLY\MyRepository\image\1" alt="image-20220404151602310" style="zoom:50%;" />

如图此时修改了库的内容，但是没有进行`git add`，所有状态是`untracked`。

当`git add`并`git commit`后：

<img src="E:\FLY\MyRepository\image\2" alt="image-20220404152203642" style="zoom:50%;" />

状态变为`clean`，即“干净”的工作区。



若未`git add`到暂存区，需要撤销对工作区的修改，回到最近一次`git add`或`git commit`时候的状态，只能用来撤回对已有文件内容的修改，文件的新建和删除无法撤销，使用：

```
git checkout -- filename
```



若已`git add`到暂存区，但未提交，需要撤销`git add`的操作，使用：

```
git reset HEAD fielname
```



提交删除文件操作

```
git rm filename
```





GitHub的使用

一、准备工作

（1）创建SSH Key（若已存在一般在`C:/users/username/.ssh`下，其中`id_rsa.pub`是公钥，`id_rsa`是私钥），若不存在可通过Git Bash创建:

```
ssh-keygen -t rsa -C "umail@exmple.com"
```

![image-20220404165247476](E:\FLY\MyRepository\image\3)

（2）登录GitHub添加`Add SSH Key`

![image-20220404165539253](E:\FLY\MyRepository\image\4)

GitHub上免费托管的Git仓库任何人都可以看到（不要放敏感数据），但只有自己可以修改。若不想让别人看到则需要交保护费让GitHub把自己公开的仓库私有化。或自己动手搭一个Git服务器。

二、添加远程库

登录GitHub，添加远程库`Add Repository`，需要自己起个仓库名称即可。

![image-20220404170304482](E:\FLY\MyRepository\image\5)

添加后的仓库是空的，需要在本地的仓库下运行命令：

```
git remote add origin https://github.com/xxx
git branch -M main
//挂了梯子需要加，IP和端口号在梯子界面下面找
git config --global http.proxy http://127.0.0.1:10809
git config --global https.proxy http://127.0.0.1:10809
//然后push
git push -u origin main
```

<img src="E:\FLY\MyRepository\image\6" alt="image-20220404172147992" style="zoom: 50%;" />

输入GitHub的账号和密码通过验证：

<img src="E:\FLY\MyRepository\image\7" alt="image-20220404171413161" style="zoom: 25%;" />

远程仓库创建完成！

<img src="E:\FLY\MyRepository\image\8" alt="image-20220404172101825" style="zoom: 33%;" />

三、删除远程库

查看远程库信息

```
git remote -v
```

<img src="E:\FLY\MyRepository\image\9" alt="image-20220404174013233" style="zoom: 50%;" />

然后根据名字删除库

```
git remote rm origin
```

此处的删除只是解除了本地与远程的绑定关系，并不是物理上地删除了远程库。远程库本身并没有任何改动，要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除。

<img src="E:\FLY\MyRepository\image\10" alt="image-20220404174604045" style="zoom: 33%;" />