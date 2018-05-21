## git 使用笔记

### 推荐教程
- [Git教程 - 廖雪峰的官方网站](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

### 查看帮助
``` shell
git help
```

``` java
public static void main(String[] args) {

}
```

### 初始配置
- 效果：在"～"目录下会生成隐藏文件: .gitconfig

- 配置用户
> $ git config --global user.name "Your Name"
> $ git config --global user.email "email@example.com"

- 查看用户
> $ git config --global user.name
> $ git config --global user.email

### 仓库创建
- 建立新仓库
> $ git init

- 从远端克隆仓库
> $ git clone https://github.com/jefshi/common-database-operate.git common-database-operate/

### 远端与本地交互操作
- 本地与远端关联
> $ git remote add origin https://github.com/hanhailong/CustomRatingBar

- 显示出详细的 remote 信息
> $ git remote -v

- 删除添加的远程库
> $ git remote remove origin

- 从远端更新到本地
> $ git pull origin master

- 从本地上传到远端
> $ git push -u origin master:master

### 本地仓库操作
- 本地添加与提交
> $ git add readme.txt
> $ git commit -m "Wrote a readme file
>
> $ git add .
> $ git commit -m "Wrote a readme file

- 撤销添加
> $ git reset HEAD readme.txt

- 查看状态：当前代码库与最新版本的简单对比
> $ # 效果：绿色表示文件被"git add", 红色表示文件没有被"git add"
> $ git status

- 查看 diff
> $ git diff
> $ git diff readme.txt

- 查看 log
> $ git log
> $ git log readme.txt

- 撤销未提交的修改
> $ git checkout readme.txt
>
> $ git reset HEAD readme.txt
> $ git checkout readme.txt

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
