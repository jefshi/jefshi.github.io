## git 使用笔记

### 推荐教程
- [Git教程 - 廖雪峰的官方网站](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

### 名词解释与目录结构

#### .git 目录
/stage 或 /index：暂存区，具体见名称解释
/HEAD：版本指针
/config：配置文件

#### 名词解释
1. 工作区（Working Directory）：就是你在电脑里能看到的目录，不解释
2. 版本库（Repository）：就是 .git 目录
3. 暂存区：命令``` git add .```就是将修改内容放置到暂存区，而命令```git commit```则是将暂存区的内容提交到当前分支

### 初始配置
效果：在"～"目录下会生成隐藏文件: .gitconfig

``` shell
# 配置用户
git config --global user.name "Your Name"
git config --global user.email "email@example.com"

# 查看用户
git config --global user.name
git config --global user.email
```

### 仓库创建

``` shell
# 建立新仓库
git init

# 从远端克隆仓库
git clone https://github.com/jefshi/common-database-operate.git common-database-operate/
```

### 远端与本地交互操作

``` shell
# 本地与远端关联
git remote add origin https://github.com/hanhailong/CustomRatingBar

# 显示出详细的 remote 信息
git remote -v

# 删除添加的远程库
git remote remove origin

# 从远端更新到本地
git pull origin master

# 从本地上传到远端
git push -u origin master:master
```

备注：
1. [origin]：

### 本地仓库操作

#### 1. 查看帮助
``` shell
# 查看帮助
git help
```

#### 2. 添加与提交

``` shell
# 添加与提交
git add readme.txt
git commit -m "Wrote a readme file"

git add .
git commit -m "Wrote a readme file"
```

#### 3. 对比与日志

``` shell
# 查看状态：当前代码库与最新版本的简单对比
git status

git status readme.txt

# 查看 diff
git diff

git diff readme.txt
```
说明：
1. 绿色表示文件被"git add", 红色表示文件没有被"git add"

``` shell
# 查看 log
git log
git log readme.txt

# 一行显示 log，只显示哈希值和提交说明
git log --pretty=oneline

git log --online
```

#### 4. 版本与版本回退

``` shell
# 版本回滚
git reset --hard HEAD^

git reset --hard 1094a # 1094a 是版本号，就是 commit id

# 查看 commit 历史，用于获取版本号
git reflog
```
说明：
1. HEAD: 表示当前版本，HEAD^：表示上一个版本，HEAD^^：表示上上一个版本，HEAD~100：表示上上上...（100个上）个版本
2. 版本号写前几位即可
3. 版本回滚后 git log 就只显示到指定回滚的版本号，即不含被回滚的版本号 log 信息
4. git reflog 可以查看所有的版本号（含被回滚的）

``` shell
# 撤销添加
git reset HEAD readme.txt

# 撤销未提交的修改
git checkout readme.txt

git reset HEAD readme.txt
git checkout readme.txt
```

#### 创建分支

``` shell
# 查看分支
git branch

# 创建分支
git branch deve

# 切换分支
git checkout deve

# 创建 + 切换分支
git checkout -b deve

# 合并某分支到当前分支
git merge deve

# 删除分支
git branch -d deve
```

备注说明：
1. deve：是分支名称，自定义
2. git branch：当前分支前面会标一个*号

### 添加Git忽略配置
由目录下的[.gitignore]文件确定，使用规则如下：

通配符：
- / ：表示目录
- \* ：匹配多个字符
- ? ：匹配单个字符
- ! ：包含单个字符的匹配列表
- [] ：表示不忽略(跟踪)匹配到的文件或目录

详细说明：
- 一行一个忽略项
- 配置按从上到下进行规则匹配的，意味着如果前面的规则匹配的范围更大，则后面的规则将不会生效
- 规则【build/*】: 等同于【build】，忽略根目录或某一目录下的[build]，以及其下的全部内容
- 规则【/.idea/*】: 等同于【/idea】，忽略根目录下的[.idea]，以及其下的全部内容
- 以下规则，表示忽略全部内容，但是不忽略[.gitignore]文件
> /*
> !.gitignore
