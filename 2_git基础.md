## 一、获取Git仓库

### 1.本地目录转换

```sh
git init
git add *.c
git add LICENSE
git commit -m "initial project version"
```

### 2.从服务器克隆

```sh
git clone <url> [newName]
```

### 3.检查当前文件状态

```sh
git status
```

**Untracked** ---> 

### 4.跟踪新文件

```sh
git add <file>
```

### 5.暂存已修改文件

```sh
git add
git commit
```

**git add: 精确地将内容添加到下一次提交中**

- 跟踪新文件
- 暂存已修改文件
- 合并时把有冲突的文件标记为已解决状态

### 6.忽略文件

```.gitignore
# 忽略所有 .js 文件
*.a
# 只忽略当前目录下的 TODO 文件，而不忽略子文件中的
/TODO
# 忽略任何目录下的 TODO 文件
TODO/
```

### 7.查看已暂存和未暂存的修改

```sh
# 尚未暂存的改动
git diff
# 查看已暂存的将要添加到下次提交的内容
git diff --staged
git diff --cached
```

### 8.提交

```sh
git commit #这样会启动文本编辑器来输入提交说明
git commit -m "story 123: Fix bug" # 把提交信息和命令放到一行
```

### 9.跳过使用暂存区域

```sh
# 自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 git add 步骤
git commit -a -m 'added new'
```

### 10.移除文件

要从 Git 中移除某个文件，就必须要从已跟踪文件清单中移除（确切地说是从暂存区域移除），然后提交

```sh
# 从暂存区移除并连带从工作目录中删除指定文件
git remove README.md
```

*直接从工作目录中移除会导致下一次提交出现 Changes not staged for commit*

```sh
# 改名
git mv file_from file_to
```

### 11.查看提交历史

```sh
# 不传入任何参数的默认情况下，按时间先后顺序列出所有提交
# 列出每个提交的 SHA-1 校验和、作者名字、邮件地址、提交时间、提交说明
git log

# 显示每次提交所引入的差异（按补丁的格式输出）并限制显示条数
git log -p -2
git log --patch -3

# 查看提交的简略统计信息
git log --stat

# 按照不同于默认格式的方式展示提交历史
git log --pretty=oneline
git log --pretty=short
git log --pretty=full
git log --pretty=fuller
git log --pretty=format

# 展示分支、合并历史
git log --pretty=format:"%h %s" --graph

# 限制展示长度
git log -<n>
git log --since=2.weeks

# 其他限制
git log --author="junio" --since="2008-10-01"

## 隐藏合并提交
git log -- no-merges
```

**git log --pretty=format**

| 选项 | 说明               | 选项 | 说明                               |
| :--- | ------------------ | ---- | ---------------------------------- |
| %H   | 提交的完整哈希值   | %ad  | 作者修订日期，可以用--date定制格式 |
| %h   | 提交的简写哈希值   | %ar  | 作者修订日期，按多久以前显示       |
| %T   | 树的完整哈希值     | %cn  | 提交者名字                         |
| %t   | 树的简写哈希值     | %ce  | 提交者email                        |
| %P   | 父提交的完整哈希值 | %cd  | 提交日期                           |
| %p   | 父提交的简写哈希值 | %cr  | 提交日期（距今多久）               |
| %an  | 作者名字           | %s   | 提交说明                           |
| %ae  | 作者email          |      |                                    |

### 12.撤销操作

```sh
git commit --amend
```

- 如果自上次提交以来还没做任何修改，那么快照保持不变，修改的只是提交信息
- 最终只会有一个提交（第二次提交会代替第一次提交的效果，与其说是修复旧提交，不如说是用一个新的提交完全取代旧的提交）

### 13.取消暂存区的文件

```sh
git reset HEAD <file>
```

### 14.撤销对文件的修改

```sh
git checkout -- <file>
```

## 二、远程仓库

### 1.查看

```sh
# 
git remote
# 显示简写和对应的URL
git remote -v

# 查看某一个远程仓库的更多信息
git remote show <remote>
```

### 2.添加远程仓库

```sh
# git remote add <shortname> <url>
git remote add origin https://github.com/schacon/gicgit

# 远程仓库重命名 git remote rename <oldname> <newname>
git remote rename pb paul

# 远程仓库移除 git remote remove/rm <name>
git remote remove paul
```

### 3.从远程拉取

```sh
# 从远程仓库拉取所有还没有的数据，执行完后会拥有那个远程仓库的所有分支
git fetch origin
# git fetch 之后并不会自动合并或修改当前的工作，必须手动合并
```

### 4.推送到远程分支

```sh
# git push <remote> <branch>
git push origin master
```

## 三、Git 别名

```sh
git config --global alias.ci commit
git config --global alisa.unstage 'reset HEAD --'
```

```sh
# 之后就可以使用
git unstage fileA
git reset HEAD -- fileA
git commit -m ""
git ci -m ""
```



