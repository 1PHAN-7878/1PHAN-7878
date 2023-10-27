---
title: 关于git上传文件的.gitignore
date: 2023-10-27 08:42:38
tags: git
---

# 问题

产生问题：由于我想上传一个Unity的项目到github，但是里面包含有大于50MB的文件，github规定了上传的文件大小，因此是不可以传上去的。

# 方案1

需要git-lfs工具支持

# 方案2 

将大文件加入.gitignore名单

由于我在操作时已经push出现了问题，所以需要先进行

```shell
git reset
```
我在创建了该文件之后，并没有删除之前的暂存区的内容，所以每一次commit和push都有之前的大文件，最终是折腾好。

==步骤如下==

创建 `.gitignore` 文件：在你的 Git 仓库根目录下，创建一个名为 `.gitignore` 的文件。可以使用文本编辑器来创建它。

编辑 `.gitignore` 文件：在 `.gitignore` 文件中，你可以列出你希望忽略的文件、目录或模式。每一行代表一个要忽略的项。可以使用通配符来匹配多个文件或目录，如 `*` 表示任意字符，`/` 表示目录分隔符，`#` 表示注释等。

   例如，以下是一个简单的 `.gitignore` 文件的示例：

   ```
   gitignoreCopy code# 忽略所有 .log 文件
   *.log
   
   # 忽略 temp 目录
   /temp/
   
   # 忽略 .DS_Store 文件（通常在 macOS 系统中生成）
   .DS_Store
   ```
保存并提交 `.gitignore` 文件：保存 `.gitignore` 文件后，将其提交到 Git 仓库中。你可以使用以下命令：

   ```shell
   git add .gitignore
   git commit -m "Add .gitignore file"
   ```

一旦设置了 `.gitignore` 文件，Git 将会忽略在文件中列出的文件和目录，不会将它们包括在版本历史中。
