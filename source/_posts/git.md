---
title: git学习下的一些基本操作
date: 2023-10-18 16:25:48
tags:
  - git
  - 学习
---

# 基础操作

```shell
git clone [ssh]
```

> ![image-20231017162915772](C:\Users\7878\AppData\Roaming\Typora\typora-user-images\image-20231017162915772.png)

```shell
# 执行 git status 查看整个仓库的状态
git status

# 使用 git add [文件名] 命令跟踪此新建文件，即把新增文件添加到暂存区，以备提交
git add one.txt

# 如果要撤销暂存区的修改怎么办？
# 根据上图的提示，执行 git reset -- [文件名] 或者 git rm --cached [文件名] 命令即可
git reset -- one.txt

# 用于查看 Git 仓库中所有分支（包括本地和远程分支）详细信息的命令。
git branch -avv
# 执行 git commit 命令生成一个新的提交，一个必须的选项 -m 用来提供该提交的备注
git commit -m 'commit one'

# 执行 git log 查看提交记录，紫色框中的十六进制序列号就是提交版本号
git log

#  git reset --soft HEAD^ 撤销最近的一次提交，将修改还原到暂存区
git reset --soft HEAD^

# 因为刚才的提交操作不是基于远程仓库 origin/master 分支的最新提交版本，而是撤回了一个版本。这种情况下也是可以将本地 master 分支推送到远程仓库的，需要加一个选项 -f ，它是 --force 的简写，这就是强制推送
# push 是需要联网执行的，它对远程仓库进行了修改
git push -f

# git reflog 命令，它会记录本地仓库所有分支的每一次版本变化
git reflog

# 怎么回退到 5c04 那个版本呢？可以直接执行命令 git reset --hard [版本号]
# 如果记不清版本号，也可以根据上图第 3 行的信息，执行 git reset --hard HEAD@{2} 命令
git reset --hard HEAD@{2}

# 还想反悔，刚才还是改对了，怎么办？再执行一次即可，这次大括号里就是 1 了
git reset --hard HEAD@{1}


```

# 分支操作

有些命令的重复度极高，比如 `git status` 和 `git branch -avv` 等，Git 可以对这些命令设置别名，以便简化对它们的使用，设置别名的命令是 `git config --global alias.[别名] [原命令]`，如果原命令中有选项，需要加引号。别名是自定义的，可以随意命名，设置后，原命令和别名具有同等作用。

> ![图片描述](https://doc.shiyanlou.com/courses/uid310176-20190514-1557819719173)

自己设置的别名要记住，也可以使用 `git config -l` 命令查看配置文件。

1. **git fetch**：

   - `git fetch` 仅仅是将远程仓库的更新下载到本地，但它不会自动合并或更新你的当前工作分支。
   - 它会下载远程分支的最新状态，但不会影响你的本地分支，你需要手动将这些更新合并到你的分支中。

   使用示例：

   ```shell
   git fetch origin
   ```

2. **git pull**：

   - `git pull` 也从远程仓库获取更新，但它会自动将远程分支的更新合并到你的当前分支。
   - 通常，`git pull` 相当于运行 `git fetch` 后再运行 `git merge` 来合并远程分支的更新。

   使用示例：

   ```shell
   git pull origin master
   ```

总之，主要区别在于自动合并。`git fetch` 用于获取远程更新，但不自动合并，而 `git pull` 用于获取远程更新并自动合并到当前分支。选择使用哪一个取决于你的工作流程和需求。如果你想手动审查和控制合并过程，可以首先运行 `git fetch`，然后手动合并。如果你想快速将远程更新合并到当前分支，可以使用 `git pull`。

## 创建分支

要查看分支信息，只需在终端中输入以下命令：

```shell
git branch
```

这将列出本地分支，当前分支将以星号标记。如果要查看远程分支，可以使用以下命令：

```shell
git branch -r
```

```shell
# 执行 git branch [分支名] 可以创建新的分支
git branch dev

# 执行 git checkout [分支名] 切换分支
git checkout dev
```

在新的分支中创建文件然后进行提交到暂存区和版本库

<img src="C:\Users\7878\AppData\Roaming\Typora\typora-user-images\image-20231018144722734.png" alt="image-20231018144722734" style="zoom:50%;" />

好，新功能已经写好并提交到了版本区，现在要推送了，推送到哪里呢？正常逻辑当然要推送到远程仓库的同名分支，不过现在远程仓库里只有一个分支：

```shell
# 执行 git push [主机名] [本地分支名]:[远程分支名] 即可将本地分支推送到远程仓库的分支中，通常冒号前后的分支名是相同的，如果是相同的，可以省略 :[远程分支名]，如果远程分支不存在，会自动创建
git push origin dev:dev
```

<img src="C:\Users\7878\AppData\Roaming\Typora\typora-user-images\image-20231018145103413.png" alt="image-20231018145103413" style="zoom:50%;" />

<img src="C:\Users\7878\AppData\Roaming\Typora\typora-user-images\image-20231018145147990.png" alt="image-20231018145147990" style="zoom: 50%;" />

如果再次在dev上修改并提交每次仍要输入`git push origin dev:dev`,可以像main一样将本地branch与远程branch关联

```shell
# 执行这个命令 git branch -u [主机名/远程分支名] [本地分支名] 将本地分支与远程分支关联
git branch -u origin/dev
```

## 删除分支

```shell
# 删除远程分支的命令：git push [主机名] --delete [远程分支名]
git push origin --delete dev

# 使用 git branch -D [分支名] 删除本地分支
git branch -D dev
```

# 多人操作

建立新的仓库，邀请参与人员

组长可以发布issue

组员克隆仓库到本地 `git clone `

解决issue 在提交时 `git commit - m 'fix #1 this is fix one'`

`pull requests`

![此处输入图片的描述](https://doc.shiyanlou.com/document-uid310176labid9824timestamp1548757171365.png)

![此处输入图片的描述](https://doc.shiyanlou.com/document-uid310176labid9824timestamp1548757180192.png)

![此处输入图片的描述](https://doc.shiyanlou.com/document-uid310176labid9824timestamp1548757180192.png)

![此处输入图片的描述](https://doc.shiyanlou.com/document-uid310176labid9824timestamp1548757219135.png)

以上就是一次完整的修改、提交、推送、提 PR、合并 PR 的过程。

**需要注意的一点：从 A 向 B 提 PR 后，在 PR 合并或关闭前，A 上所有新增的提交都会出现在 PR 里。**
