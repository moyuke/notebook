# Git操作指北

## 基本操作

$工作区\stackrel{add}{\longrightarrow}暂存库\stackrel{commit}{\longrightarrow}本地git版本库\stackrel{push}{\longrightarrow}remote版本库$ 

!!! note ""
	工作区：电脑里能看到的目录。<br>
	暂存区：一般存放在 .git 目录下的 index 文件（.git/index）中，有时也叫作索引（index）。<br>
	版本库：工作区的隐藏目录 .git。不算工作区，而是 Git 的版本库。

??? note "Python命令行参数"
	-c：可在命令行中写Python代码执行，用""包围，可分行。<br>
	-m：以脚本的方式执行Python模块或包。<br>
	-u：unbuffered，标准输出打印到屏幕。

### 注册全局信息

```bash
git config --global user.name <name>
git config --global user.email <email>
```

### 初始化

```bash
git init #在当前目录下生成.git
git init newrepo #在newrepo目录下生成.git
```

### 添加文件

```bash
git add <file>
git add . #添加所有
git add * #添加新/修改文件
```

### 提交项目到仓库

```bash
git commit -m "upd"
```

### 查看信息

```bash
git status #查看状态
git log #查看历史提交记录
git branch #查看本地分支
```

### 远程仓库命令

```bash
git remote -v #列出当前仓库中已配置的远程仓库，并显示URL
git remote add origin <url> #添加一个新的远程仓库并指定其的名称和URL
git remote rename <old_name> <new_name> #重命名远程仓库
git remote remove <remote_name> #删除远程仓库
git remote show <remote_name> #显示指定远程仓库的详细信息，包括URL和跟踪分支
```

### 下载项目

```bash
git clone <url> #拷贝远程仓库
git pull origin master:brantest
#将远程主机 origin 的 master 分支拉取过来，与本地的 brantest 分支合并
git pull origin master #合并对象为当前分支
```

### 上传项目

```bash
git push -u origin master
git push origin master:master
#将本地master分支推送到origin主机的master分支，master不存在则新建
git push --force origin master
git push -uf origin master
#本地版本与远程版本有差异，强制推送
```

### 回退版本

```bash
git reset --hard HEAD^
#HEAD^:上一个版本,HEAD~100:上100个版本
```

### 删除文件

```bash
git rm <file> #从暂存区和工作区中删除文件
git rm -f <file> #修改过且已放到暂存区，强制删除
git rm --cached <file> #从暂存区移除，在工作区保留
git mv <file> #移动或重命名
```



## 分支管理

### 创建分支

```bash
git branch <branchname>
git branch #没有参数时会列出本地分支
```

### 切换分支

```bash
git checkout <branchname>
#切换分支的时候，Git 会用该分支的最后提交的快照替换你的工作目录的内容
git checkout -b <branchname> #创建新分支并立即切换
```

### 合并分支

```bash
git merge <branchname> #将<branchname>合并到当前分支
#合并：
```

### 删除分支

```bash
git branch -d <branchname>
```

### 切换分支

```bash
git checkout <branchname>
```

