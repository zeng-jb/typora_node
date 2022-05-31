## git基本操作

### 1.工作流程

- git仓库（存放用户提交的文件）
- 暂存区（临时的git仓库，存放临时被修改的文件）
- 工作目录（平时写代码的地方）

![img](https://gitee.com/zeng-jiabin/typora_imgs/raw/master/PCAutor/20191219141352260.png)

![工作流程](https://gitee.com/zeng-jiabin/typora_imgs/raw/master/PCAutor/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3BzcHh1YW4=,size_16,color_FFFFFF,t_70.png)

1. 用户先将工作目录提交到（add）暂存区
2. 确认提交后可将暂存区的文件提交至（push）git仓库

注意：为了高效，如果文件没有修改，提交文件夹时，Git不在重新存储文件，而是保留一个链接指向之前的存储文件。重新存储的都是修改过的文件。

### 2.Git安装

去[官网](https://git-scm.com/)下载对应自身系统就行啦，安装过程选项默认即可。

安装完成后右键会有git GUI 和git Bash 两个标识。一般用Git Bash Here

查看git版本 `git --version`

### 3.使用前配置

先配置用户姓名和邮箱

-  `git config --global user.name xxx`
- `git config --global user.email xxx@xxx.com`

查看配置信息

- `git config --list`



### 4.Git提交文件步骤

- 初始化Git仓库： `git init`
- 查看文件状态：`git status`
- 添加文件到缓存区： `git add 文件名` 或 `git add .` (当前文件夹所有内容)
- 向仓库提交代码： `git commit -m 提交信息`
- 查看提交记录： `git log`
- 发布到仓库： `git push -u origin master`



### 5.Git撤销

1. `git checkout 文件名` 当你在功能时，开发到一半，你可以向暂存区中添加已修改的文件，然后回到工作目录继续开发。继续开发的过程中发现代码有问题，这时候就可以利用撤销，将之前暂存区中的文件覆盖工作目录的文件，这样就可以将代码恢复到之前开发到一半的状态。**注意这个指令不会影响暂存区的文件**

2. `git rm --cached 文件名` ||| `git rm -r --cached 文件夹` 删除暂存区的文件或文件夹
3. `git reset --hard commitId` 将git仓库的指定时段的文件恢复出来，先使用git log 查询提交的记录，查看cimmintid。注意此方法将恢复之前提交的数据，假设你有四次提交的记录，你恢复到了第二次，那么第三四次的记录会被清除。



### 6.Git分支

git分支相当于一个当前工作目录的副本

分支的优点就是可以在相同的环境或不同的环境下进行不同的开发
比如说现在需要在同一个文件下开发功能和修改bug，这时就可以利用分支，分开开发。互不影响，提高工作效率。

#### 1.分支结构

- **主分支（`master`）**：第一次向 git 仓库中提交代码时会自动生成
- **开发分支（`develop`）**：作为开发的分支，基于`master` 分支创建
- **功能分支（`feature`）**：作为开发功能的分支，基于开发分支创建
- **其他分支**：分支可以灵活运用。储存软件的不同版本等，都可以使用分支。

#### 2.分支基本命令

- 查看分支： `git branch`
- 创建分支：`git branch 分支名称`
- 切换分支：`git checkout 分支名称`