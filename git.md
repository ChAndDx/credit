#git笔记
##git clone 从服务器拉取代码
`git clone https://github.com/ChAndDx/credit.git`

##git config 配置开发者用户名和邮箱
```
git config --global user.name "MrChen"
git config --global user.email xxx@xxx
```
###查看配置代码
`git config --list`

##git branch 创建、重命名、查看、删除项目分支
###创建名为daily/0.0.0的分支
`git branch daily/0.0.0`

###重命名为daily/0.0.1
`git branch -m daily/0.0.0 daily/0.0.1`

###查看分支列表
`git branch`

###删除分支
`git branch -d daily/0.0.1`

##git checkout 切换分支
`git checkout daily/0.0.1`

##git status 查看文件变动状态
`git status`
```
On branch daily/2021.5.25
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        git.md

nothing added to commit but untracked files present (use "git add" to track)
```

##git add 添加文件变动到暂存区
###通过指定文件名git.md可以将文件添加到暂存区
`git add git.md`
###添加所有文件
`git add --all`
`git add .`

##git commit 提交文件变动到版本库
`git commit -m '提交原因'`

##git push 将本地代码改动推送到服务器
`git push origin daily/2021.5.25`

##git pull 将服务器上的最新代码拉取到本地
`git pull origin daily/2021.5.25`

























