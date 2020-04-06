### 安装
    git --version

### 初始化配置
    git config --global user.name "zhourongtu"
    git config --global user.name "zhourongtu@qq.com"
    git confit --list

### 初始化仓库
    git init 

### C(新增)
    在工作目录中新增文件
    git status
    git add ...
    git commit -m msg

### U(修改)
    在工作目录中修改文件
    git status
    git add ..
    git commit -m "msg"

### D(删除 & 重命名)
    git rm 要删除的文件     git mv 老文件 新文件
    git status              git status
    git commit -m "msg"     git commit -m "msg"

### R(查询)
    git status      :查看工作目录中文件的状态（已跟踪（已提交，已暂存，已修改）未跟踪）
    git diff 
    git diff --cache
    git log --oneline

### 分支 （本质是指向提交对象的指针）
    HEAD    ·是一个指针-->默认指向master分支
            ·切换分支时，其实就是让head指向不同的分支
            ·每次有新的提交时候，HEAD带着当前指向的分支，一起往前移动
    git log --oneline --decorate --graph --all
    git branch : 查看分支列表
    git branch -v : 查看分支指向的最新提交
    git branch name : 在当前提交对象上创建新的分支
    git branch name commithash : 在制定提交对象上创建分支
    git checkout name : 切换分支  -b 新建+切换
    git branch -d name : 删除空的分支，已经合并的分支
    git branch -D name : 强制删除分支

### 切换分支
    最佳实践：每次切换分支前，当前分支，一定得是干净的（已提交状态）
    坑：
        在切换分支时，如果当前分支上有未提交的暂存（第一次），有未暂存的修改（第一次）
            这种操作会污染文件
        （提交过了则不然切走）
    动三个地方
        HEAD
        暂存区
        工作区

### 分支合并
    快进合并
    git branch merge xxx
    典型合并
        合并后，打开冲突文件，修改代码，之后选择合并
    git branch --merged 查看已经合并的分支
### git存储
    git stash保存到一个栈上
    git stash apply （相当于front
    git stash drop xxx
    git stash list
    git stash pop（相当于pop+front）

### 后悔药
    工作区
        如何撤回自己在工作目录中的修改
        git checkout --filename     
    暂存区
        如何撤回自己的暂存
        git reset HEAD filename（默认是mixed
        git restore --staged filename 
        本质：暂存和版本都是HEAD的情况
    版本库
        如何撤回自己的提交：（1.注释写错了。2.）
        git commit --amend（只能改注释的样子)
        事实上add以后再amend 可以重新提交（

### reset 
    三部曲
        第一部： git reset --soft HEAD~ (--amend)
            只动HEAD(带着分支一起移动)
            此时，工作区为新的版本，暂存区为新的版本，HEAD指向旧版本
        第二部： git reset --mixed HEAD~
            动HEAD（带着分支一起动）
            工作区为新的版本，暂存区为旧的版本，HEAD指向旧的版本
        第三部： git reset --hard HEAD~
            动HEAD
            动了暂存区
            动了工作区
            工作区为旧的版本，暂存区为旧的版本，HEAD为旧的版本

### checkout
    git checkout 分支名  &  git reset --hard commithash 
        1.checkout 只动HEAD，--hard 动HEAD，带着分支一起走
        2.checkout 对工作目录是安全的 --hard强制覆盖工作目录
    git checkout commithash --file
        更新暂存区，更新工作目录
    git checkout  -- <file>  撤回工作目录的修改
        git rest --hard commitHash --filename 
        只动工作目录

### 数据恢复
    git branch recover-branch xxxx

### TAG(标签)
    列出标签
        git tag 
        git tag -l "xxx*" //正则表达式匹配
    创建标签
        git tag xxx 打tag
    查看特定标签
        git show tagname 
        git tag xxx 哈希
    删除特定标签
        git tag -d xxx
    检出标签
        git checkout tagname -->产生头部分离
        git checkout -b "v1.0"-->再创建标签

### Git特点
    1.直接记录快照，而不是差异比较
    2.几乎所有操作都是本地执行
    3.时刻保持数据完整性
    4.多数操作仅添加数据
    5.文件三种状态

