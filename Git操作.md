# Git操作

### 6行配置
查看版本：`git --version`
```bash
git config --global user.name 你的英文名
git config --global user.email 你的邮箱
git config --global push.default simple
git config --global core.quotepath false
git config --global core.editor "code --wait"
git config --global core.autocrlf input
```
查看配置：`git config --global core.autocrlf input`
### git本地操作
#### 场景一：版本控制(切换)
`mkdir demo-1`
`cd demo-1`
`touch index.html`
`code . `   // 用vscode打开当前目录
`git init ` // 创建.git空目录(本地仓库)，存放代码快照
`ls -a`   // 显示 . 开头的文件
`git status`  // 查看哪些没提交
`git add index.html ` // 告诉git哪些文件要提交
`git add .`   //提交当前目录
`git add *`  // 所有文件，.开头的文件除外(.gitignore)
新建.gitignore文件，将不要add的文件写入.gitignore
常见的不用提交的有：node_modules, .DS_Store, .idea, .vscode
git add * 和 git add . 都会排除掉.gitignore里的文件


`git commit -m "版本1"`  // 提交，复制一份快照到.git; 如果-m 后的字符串没空格不用加引号
`git commit -v`   // --verbose 冗长的，可以回顾刚刚改了什么，把提交理由写的更详细(推荐)
`git log`  // 查看当前版本之前的提交记录， q退出
`git reset --hard xxxxxx`   // commit 序号, 一般前6位(完整序号也行)，回到指定版本号；如果有文件处于add状态，未commit，会被删掉
`git reflog` // 查看所有历史提交记录


如果不小心把一个文件夹git init了
直接`rm -rf .git`就可以了
#### 场景二： 2条线开发
`git branch x`   // 创建x支线
`git checkout x `  // 切换到x直线开发
`git checkout master`  // 切换到主线
每条支线都可以分别git add 和 git commit
各分支独立互不影响
`git branch`   // 查看有多少分支


#### 场景三： 分支合并
`git checkout master`
`git merge x`  // 将对x的更改作用到master上(新增/修改/删除文件)
有冲突(两分支对同一文件做了修改)
git status  // 查看哪个文件有冲突
手动更改文件，删掉不要的标记====<<<<>>>>
`git add 修改的文件`
`git commit` // 提交合并，不带任何参数
`git status -sb`  // 显示简化信息
`git branch -d x ` // 删掉x分支


总结：
git add 添加的是文件的变化，删除也要git add 
常用的是`git add .` 和 `git commit -v`


### git远程操作
#### 配置SSH
推荐用SSH方式; HTTPS每次都要输入密码，很麻烦
原理：私钥在你电脑上，公钥在GitHub上，公钥和私钥可相互解密
生成密钥：
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
~/ssh目录生成两个文件
id_rsa 私钥(不能给任何人看)
id_rsa.pub 公钥(复制到github上)
测试是否配对成功：`ssh -T git@github.com`


#### 上传
在github新建repo
新建后，根据提示，在本地仓库执行：
`git remote add origin git@xxxxxxx`
`git push -u origin master  ` // 如果你提交的分支不叫master, 要改成你的分支

上传到第二个repo
`git remote add origin2 git@xxxxxxx`
`git push -u origin2 master  `

`git remote -v` 查看远程地址，可以看到上传到了哪些仓库
`git push origin master`  // 将之后的更新上传到指定的repo
`git push origin2 master`

上传其他分支：
方法一
`git checkout x`
`git push -u origin x ` // 每个分支第一次提交都要这样，以后就直接git push
方法二
`git push origin x:x`   // 将本地x分支上传到远程x分支

如果远程仓库有更新，要先pull后push
每次push都只是把本地的一条分支上传到远程repo


本地仓库是可以随意移动位置的


#### 下载
下载别人的代码要Https，自己的可以用SSH
git clone git@xxxxxxx
git clone git@xxxxxxx yyy  // 重命名目录为yyy
git clone git@xxxxxxx .    // 将.git下载到当前目录(最好是空目录)


#### 简化命令
```bash
touch ~/.bashrc  # 新建bash配置文件

echo 'alias ga="git add"'>> ~/.bashrc
echo 'alias gc="git commit -v"'>> ~/.bashrc
echo 'alias gl="git pull"'>> ~/.bashrc
echo 'alias gp="git push"'>> ~/.bashrc
echo 'alias gco="git checkout"'>> ~/.bashrc
echo 'alias gst="git status -sb"'>> ~/.bashrc

source ~/.bashrc  # 每次更改都要source一下
```
美化git log
在~/.bashrc里添加
```bash
alias glog="git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit -- | less"
```
之后source ~/.bashrc


#### 通灵术
git add 文件
git stash // 将add的文件藏到隐秘空间
git stash pop // 将隐藏的文件召唤出来

