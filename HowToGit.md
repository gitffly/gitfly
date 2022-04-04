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
git add xxx文件名
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



工作区中里的隐藏目录 `.git` 其实是版本库。版本库里有暂存区stage（或index），以及Git自动创建的第一个分支`master`，指向master的第一个指针即为`HEAD`。