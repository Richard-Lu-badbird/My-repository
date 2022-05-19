# Git分布式版本控制工具

## 1、目标

- 了解Git基本概念
- 能够概述git工作流程
- 能够使用Git常用命令
- 熟悉Git代码托管服务
- 能够使用idea操作git

## 2、概述

### 2.1、开发中的实际场景

### 2.2  版本控制器的方式

```
a、集中式版本控制工具
	集中式版本控制工具，版本库是集中存放在中央服务器的，team里每个人work时从中央服务器下载代码，是必须联网才能工作，局域网或者互联网。个人修改后然后提交到中央版本库。
	举例：SVN（SubVersion）和CVS（Concurrent Version System）
b、分布式版本控制工具
	分布式版本控制系统没有“中央服务器”，每个人的电脑上都是一个完整的版本库，这样工作的时候，无需联网，因为版本库就在你自己的电脑上。多人协作只需要各自的修改推送给对方，就能互相看到对方的修改了
	举例：GIt
```

### 2.3、SVN

![](https://richard-resources.oss-cn-hangzhou.aliyuncs.com/img/202205181532007.png)

### 2.4、Git

![](https://richard-resources.oss-cn-hangzhou.aliyuncs.com/img/202205181533390.png)

```
 	Git是分布式的，Git不需要有中心服务器，我们每台电脑拥有的东西都是一样的，我们使用Git并且有个中心服务器，仅仅是为了方便交换大家的修改，但是这个服务器的地位和我们每个人的PC是一样的。
```

### 2.5 、Git工作流程图

![](https://richard-resources.oss-cn-hangzhou.aliyuncs.com/img/202205181533205.png)

## 3、 Git安装与常用命令

本教程的里的git命令例子都是在Git Bash中演示的，会用到一些基本的linux命令，在此为大家提前举例

- ls/ll      查看当前目录
- cat      查看文件内容
- touch  创建文件
- vi         vi编辑器（使用vi编辑器是为了方便展示效果）

### 3.1、 Git安装与常用命令

#### 3.1.1 下载与安装

Git GUI：Git提供的图形界面工具

Git Bash: Git提供的命令行工具

当安装Git后首先要做的事情是设置用户名称和email地址。这是非常重要的，因为每次Git提交都会使用该用户的信息

#### 3.1.2 基本配置

1. 打开Git Bash

2. 设置用户信息

   `git config --global user.name "Richard Lu" # 名称` 

   `git config --global user.email "1828356181@qq.com" #邮箱` 
   
   `git config --global --list #查询用户全局信息`

#### 3.1.3 为常用指令配置别名（可选）

有些长的指令参数非常多，每次都要输入好多参数，我们可以使用别名

1.打开用户目录，创建.bashrc文件

部分windows系统不允许用户创建点号开头的文件，可以打开gitBash,执行 touch ~/.bashrc

2.在.bashrc 文件中输入以下内容

```shell
# 用于输出git提交日志
alias git-log='git log --pretty=oneline --all --graph --abbrev-commit'
# 用于输出当前目录所有文件及基本信息
alias ll='ls -al'
```

### 3.2、获取本地仓库

要使用Git对我们的代码进行版本控制，首先需要获得本地仓库

1. 在电脑的任意位置创建一个空目录，（例如Test）作为我们的本地Git仓库
2. 进入这个目录中，点击右键打开Git Bash窗口
3. 执行命令git init
4. 如果创建成功后可在文件夹下看到隐藏的,git目录

### 3.3、基础操作指令

Git工作目录下对于文件的**修改**（增加、删除、更新）会存在几个状态，这些修改的状态会随着我们执行Git的命令而发生变化

![](https://richard-resources.oss-cn-hangzhou.aliyuncs.com/img/202205181533336.png)

如何使用命令来控制这些状态之间的转换

1.`git add   (工作区 ———> 暂存区) git add . #添加所有文件到暂存区`

2.`git commit( 暂存区———>本地仓库) git commit -m "消息内容"#提交暂存区中的内容到本地仓库`

#### 3.3.1、*查看修改的状态（status）

- 作用:查看的修改的状态（暂存区、工作区）
- 命令形式：git status

#### 3.3.2、*添加工作区到暂存区（add）

- 作用：添加工作区一个或多个文件的修改到暂存区
- 命令形式：git add单个文件名|通配符
  - 将所有修改加入暂存区：git add .

#### 3.3.3、*提交暂存区到本地仓库（commit）

- 作用：提交暂存区内容到本地仓库的当前分支
- 命令形式：git commit -m '注释内容'

#### 3.3.4、*查看提交日志（log）

在3.1.3中配置的别名git-log就包含了这些参数，所以后续可以直接使用命令git-log

- 作用：查看提交记录
- 命令形式：git log [option]
  - options
    - --all显示所有分支
    - --pretty=oneline 将提交信息显示为一行
    - --abbrev-commit 使得输出的commitid更简短
    - --graph 以图的形式显示

#### 3.3.5、版本回退

- 作用：版本切换
- 命令形式：git reset --hard commitID
  - commitID 可以使用git-log 或者git log 指令查看
- 如何查看已经删除的记录？
  - git reflog
  - 这个指令可以看到已经删除的提交记录

#### 3.3.6、添加文件至忽略列表

一般我们总会有些文件无需纳入Git得管理，也不希望他们总出现在未跟踪文件列表。通常都是些自动生成得文件，比如日志文件，或者编译过程中创建的临时文件等。在这种情况下，我们可以在工作目录中创建一个名为.gitignore得文件（文件名称固定），列出要忽略的文件模式。

> 忽略文件 .gitignore

1. 忽略文件中的空行或以井号（#）开始的行会被忽略。
2. 可以使用Linux通配符。例如：星号（*）代表任意多个字符，问号（？）代表一个字符，方括号（[abc]）代表可选字符范围，大括号（{String1, String2}）代表可选的字符串等。
3. 如果名称的最前面有一个感叹号，表示例外规则，将不被忽略
4. 如果名称的最前面是一个路径分隔符（/），表示要忽略的文件在此目录下，而子目录中的文件不忽略
5. 如果名称的最后面是一个路径分隔符（/），表示要忽略的是此目录下该名称的子目录，而非文件（默认文件或目录都忽略）

```shell
#为注释
*.txt	#忽略所有.txt结尾
!lib.txt # 但lib.txt除外
/temp	#仅忽略根目录下的TODO文件，不包括其他目录temp
build/	#忽略build目录下的所有文件
# no .a files
*.a
# but do track lib.a , even though you're ignoring .a files above
!lib.a
# only ignore the TODO file in the current directory, not subdir/TODO
/TODO
# ignore all files in the build/directory
build/
# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt
# ignore all .pdf files in the doc/ directory
doc/**/*.pdf
```



### 3.4、分支

几乎所有的版本控制系统都以某种形式支持分支，使用分支意味着你可以把你的工作从开发主线上分离开来进行重大得bug修改、开发新的功能，以免影响开发主线。

#### 3.4.1、查看本地分支

- 命令：git branch

#### 3.4.2、创建本地分支

- 命令：git branch 分支名

#### 3.4.4、*切换分支（checkout）

- 命令：git checkout 分支名

我们还可以直接切换到一个不存在的分支（创建并切换）

- 命令：git checkout -b 分支名

#### 3.4.6、*合并分支（merge）

一个分支上的提交可以合并到另一个分支

命令：git merge 分支名称

#### 3.4.7、删除分支

**不能删除当前分支，只能删除其他分支**

git branch -d b1  删除分支时，需要做各种检查

git branch -D b1 不做任何检查，强制删除

#### 3.4.8、解决冲突

当两个分支上对文件的修改可能会存在冲突，例如同时修改了同一个文件的同一行，这时就需要手动解决冲突，解决冲突步骤如下：

1. 处理文件中冲突的地方
2. 将解决完冲突的文件加入暂存区（add）
3. 提交到仓库(commit)

#### 3.4.9、开发中分支使用原则与流程

在开发中，一般有如下分支使用原则与流程：

- master（生产）分支
  - 线上分支，主分支，中小规模项目作为线上运行的应用对应的分支
- develop（开发）分支
  - 是从master创建的分支，一般作为开发部门的主要开发分支，如果没有其它并行开发不同期上线要求，都可以在此版本进行开发，阶段开发完成后，需要合并到master分支，准备上线
- feature
  - 从develop创建的分支，一般是同期并行开发，但不同期上线时创建的分支，分支上的研发任务完成后合并到develop分支。
- hotfix/xxxx分支、
  - 从master派生的分支，一般作为线上bug修复使用，修复完成后需要合并到master\test\develop分支
- 还有一些其他的分支，再次不再详述，例如test分支（用于代码测试）、pre分支（预上线分支）等等

![](https://richard-resources.oss-cn-hangzhou.aliyuncs.com/img/202205181534389.png)

## 4、Git远程仓库

### 4.1、常用的托管服务[远程仓库]

```
前面我们已经知道了Git中存在两种类型的仓库，即本地仓库和远程仓库。那么我们如何搭建Git远程仓库呢？我们可以借助互联网上提供的一些代码托管服务来实现，其中比较常用的有Github、码云、GitLab等。
github(地址：https//github.com/)是一个面向开源及私有软件项目的托管平台，因为只支持git作为唯一的版本库格式进行托管，故名github
码云（地址：https://gitee.com/）是国内的一个代码托管平台，由于服务器在国内，所以相比于github，码云速度会更快
GitLab(地址：https://about.gitlab.com/)是一个用于仓库管理系统的开源项目，使用Git作为代码管理工具，并再次基础上搭建起来的web服务，一般用于在企业，学校等内部网络搭建git私服
```

### 4.4、配置SSH公钥

- 生成SSH公钥
  - 在user/.ssh文件下git
  - `ssh-keygen -t rsa`
  - 不断回车
    - 如果公钥已经存在，则自动覆盖
- Gitee设置账户共公钥
  - 获取公钥
    - `cat ~/.ssh/id_rsa.pub`
  - 验证是否配置成功
    - `ssh -T git@gitee.com`

### 4.5、操作远程仓库

#### 4.5.1、添加远程仓库

**此操作是先初始化本地库，然后与已创建的远程库进行对接**

- 命令：`git remote add <远端名称> <仓库路径>`

```shell
git remote add origin git@gitee.com:RichardLDH/git_test.git
```

- 远端名称，默认是origin,取决于远端服务器设置
- 仓库路径，从远端服务器获取此URL
- 例如上面的代码块

#### 4.5.2、查看远程仓库

- 命令：`git remote`

- ```shell
  git remote
  ```

#### 4.5.3、推送到远程仓库

- 命令：git push [-f] [--set-upstream] [远端名称  [ 本地分支名][ :远端分支名]]
  - 如果远程分支名和本地分支名称相同，则可以只写本地分支
    - `git push origin master`
  - `-f `表示强制覆盖
  - `--set-upstream `推送到远端的同时并且建立起和远端分支的关联关系
    - `git push --set-upstream origin master:master`
  - 如果**当前分支已经和远端分支已经关联**，则可以省略分支名和远端名
    - `git push `将master分支推送到一关联的远端分支

#### 4.5.4、本地分支与远程分支的关联关系

- 查看关联关系我们可以使用git branch -vv 命令

#### 4.5.5、从远程仓库克隆

如果已经有一个远端仓库，我们可以直接clone到本地。

- 命令：`git clone <仓库路径> [本地目录]`

  - 本地目录可以省略，会自动生成一个目录

  

#### 4.5.6、从远程仓库中抓取和拉取

远程分支和本地的分支一样，我们可以进行merge操作，只是需要先把远端仓库里的更新都下载到本地，再进行操作。

- 抓取 命令：`git fetch [remote name] [branch name]`
  - **抓取指令就是将仓库里的更新都抓到本地，不会进行合并**
  - 如果不指定远端名称和分支名，则抓取所有分支
- 拉取 命令：`git pull [remote name] [branch name]`
  - **啦取指令就是将远端仓库的修改拉到本地并自动进行合并，等同于fetch + merge**
  - 如果不指定远端名称和分支名，则抓取所有并更新当前分支

#### 4.5.7、解决合并冲突

在一段时间，A、B用户修改了同一个文件，且修改了同一行位置的代码，此时会发生合并冲突。

A用户在本地修改代码后优先推送到远程仓库，此时B用户在本地修订代码，提交到本地仓库以后，也需要推送到远程仓库，此时B用户晚于A用户，**故需要先拉取远程仓库的提交，经过合并后才能推送到远端分支**，如下图所示。

![](https://richard-resources.oss-cn-hangzhou.aliyuncs.com/img/202205181534407.png)

在B用户拉取代码时，因为A、B用户同一段时间修改了同一个文件的相同位置代码，故会发生合并冲突。

**远程分支也是分支，所以合并时冲突的解决方式也和解决本地分支冲突相同**，

## 5、在Idea中使用Git

### 5.1、在Idea中配置Git

安装和Intellij IDEA后，如果Git安装在默认路径下，那么idea会自动找到git的位置。

## 6. 基本linux命令

1. cd ：改变目录
2. cd ..:回退到上一个目录，直接cd进入默认目录
3. pwd：显示当前所在的目录路径
4. ls(ll):都是列出当前目录中的所有文件，只不过ll(两个ll)列出的内容更为详细
5. touch:新建一个文件，如 touch index.js
6. rm: 删除一个文件 rm index.js 就会删除index.js 文件
7. mkdir: 新建一个目录，就是新建一个文件夹
8. rm -r : 删除一个文件夹 rm -r src 删除src目录
   `rm -rf / 切勿在Linux中尝试！删除电脑中的全部文件！！`
9.  mv 移动文件， `mv index.html src`其中index.html是我们要移动的文件，src是目标文件夹。必须保证在同一目录下
10.  reset 重新初始化终端/清屏
11.  clear 清屏
12.  history 查看命令历史
13.  help 帮助
14.  exit 退出
15.  \# 表示注释