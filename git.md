# git笔记  
## git clone 从服务器拉取代码  
`git clone https://github.com/ChAndDx/credit.git`

## git config 配置开发者用户名和邮箱  
```
git config --global user.name "MrChen"
git config --global user.email xxx@xxx
```
### 查看配置代码  
`git config --list`

## git branch 创建、重命名、查看、删除项目分支  
### 创建名为daily/0.0.0的分支  
`git branch daily/0.0.0`

### 重命名为daily/0.0.1  
`git branch -m daily/0.0.0 daily/0.0.1`

### 查看分支列表  
`git branch`

### 删除分支  
`git branch -d daily/0.0.1`

## git checkout 切换分支  
`git checkout daily/0.0.1`

## git status 查看文件变动状态  
`git status`
```
On branch daily/2021.5.25
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        git.md

nothing added to commit but untracked files present (use "git add" to track)
```

## git add 添加文件变动到暂存区  
### 通过指定文件名git.md可以将文件添加到暂存区  
`git add git.md`
### 添加所有文件  
`git add --all`
`git add .`

## git commit 提交文件变动到版本库  
`git commit -m '提交原因'`

## git push 将本地代码改动推送到服务器  
`git push origin daily/2021.5.25`

## git fetch 将服务器上的最新代码拉取到本地  
```
git fetch <远程主机名> <分支名>
git fetch origin daily/2021.5.25
```
### 取回更新后,返回一个FETCH_HEAD,指的是某个branch在服务器上的最新状态  

### 查看刚取回的更新信息  
`git log -p FETCH_HEAD`

### 将拉取下来的最新内容合并到当前所在的分支中  
`git merge FETCH_HEAD`

## git pull = git fetch + git merge  

## git pull 将服务器上的最新代码拉取到本地合并  
`git pull <远程主机名> <远程分支名>:<本地分支名>`
`git pull origin daily/2021.5.25`

## git remote 查看项目远程地址  
`git remote -v`

## git log 查看版本提交记录  
### J往下翻,K往上翻,Q退出  
`git log`

## git tag 为项目标记里程碑  
### 列出已有的tag  
`git tag`
### 加上-l命令可以使用通配符来过滤tag
```
git tag -l "v3.3.*"
v3.3.0
v3.3.1
```
### 新建tag  
`git tag v1.0`

### 添加备注信息  
`git tag -a v1.1 -m "备注信息"`

### 查看tag详细信息  
`git show tagName`

### 给指定的某个commit号加tag  
`git tag -a v1.2 9fceb02 -m "备注信息"`

### 将tag同步到服务器  
```
git push origin v1.0 //推送单个
git push origin --tags //全部推送
```

### 切换到某个tag  
```
git checkout v1.0
git branch newbranch v1.0 //以v1.0创建分支
```

### 删除某个tag  
```
git tag -d v1.0 //本地删除
git push origin :refs/tags/v0.1.2
```























