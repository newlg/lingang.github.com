---
layout: post
title: "git 的使用"
date: 2016-12-23 18:36:25 +0800
comments: true
categories:
---
## Git SSH Key 生成步骤

##### 设置Git的user name和email：

$git config --global user.name “newlg"

$git config --global user.email “mylingang@126.com"

$git config --list //查看配置信息

#####  生成密钥：

$ ssh-keygen -t rsa -C "mylingang@126.com"

按3个回车，密码为空。

最后得到了两个文件：id_rsa和id_rsa.pub

#####  把id_rsa.pub上传至git服务器

/Users/mylingang/.ssh/id_rsa //私钥位置

/Users/mylingang/.ssh/id_rsa.pub //公钥位置

#####  添加密钥到ssh：ssh-add 文件名

需要之前输入密码。

##### 在github上添加ssh密钥，这要添加的是“id_rsa.pub”里面的公钥。
打开https://github.com/ ，登陆mylingang@126.com，然后添加ssh。

##### 测试：ssh git@github.com
The authenticity of host ‘github.com (207.97.227.239)’ can’t be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added ‘github.com,207.97.227.239′ (RSA) to the list of known hosts.
ERROR: Hi tekkub! You’ve successfully authenticated, but GitHub does not provide shell access
Connection to github.com closed.




## 使用Github

##### 获取源码：
$git clone git@github.com:billyanyteen/github-services.git

##### 这样你的机器上就有一个repo了。
##### git于svn所不同的是git是分布式的，没有服务器概念。所有的人的机器上都有一个repo，每次提交都是给自己机器的repo
仓库初始化：
git init

生成快照并存入项目索引：
git add

文件,还有git rm,git mv等等…

项目索引提交：
git commit

##### 协作编程：将本地repo于远程的origin的repo合并，

推送本地更新到远程：
git push origin master

更新远程更新到本地：
git pull origin master

补充：
添加远端repo：
$git remote add upstream git://github.com/pjhyett/github-services.git

重命名远端repo：
$ git://github.com/pjhyett/github-services.git为“upstream”

## Git命令

1. $mkdir learngit //创建文件夹
2. $pwd //显示当前目录
3. $git init // 初始化Git
4. $ls -ah //显示隐藏的目录
5. $git add readme.txt //把文件添加到仓库
6. $git commit -m "wrote a readme file" //把文件提交到仓库
7. $git status //工作区的状态
8. $git diff //查看修改内容
9. $ git log //查看提交历史
10. $ git log --pretty=oneline //--pretty=oneline 单行查看
11. $ git reflog //查看命令历史
12. $ git reset --hard commit_id //回退到版本
13. HEAD当前版本 HEAD^上一个版本 HEAD^^上上一个版本 HEAD~100往上100个版本
14. 工作区和版本库(.git)
版本库中add后有为stage（或者叫index）的暂存区，commit后会创建第一个分支master，以及指向master的一个指针叫HEAD
git add //把文件修改添加到暂存区
git commit //把暂存区的所有内容提交到当前分支
简单讲：需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改
15. Git跟踪并管理的是修改，而非文件
16. $ git diff HEAD -- readme.txt //查看工作区和版本库里面最新版本的区别
17. git如何跟踪修改的 //每次修改，如果不add到暂存区，那就不会加入到commit中
18. $ git checkout -- readme.txt //丢弃工作区
19. $ git reset HEAD readme.txt //丢弃暂存区
20. $ rm test.txt //删除文件(可以从版本库中checkout)
21. $ git rm test.txt //从版本库中删除文件
22. $ git checkout -- test.txt
23. $ git remote add origin https://github.com/LensXiong/learngit.git //关联一个远程库
24. $ git push -u origin master //首次推送
25. $ git push origin master //非首次推送
26. $ git clone git@github.com:michaelliao/gitskills.git//远程克隆
## 相关命令

#### 撤销误操作

git status -s  -s表示short 第一列M表示staging 第二列M表示working

git add --file 工作区到暂存区 (working->staging)

git commit -m '' 暂存区到历史区(staging->histroy)

git commit -am 工作区到历史区(working->staging)

git checkout --file

从暂存区到工作区(staing->working)

git reset --file 从历史区到暂存区（histroy->staging）

git checkout HEAD --file 从历史区到工作区(histroy->working)
#### 移除及重命名文件

git rm file

git rm --cached file  

git mv oldfile newfile 文件重命名
#### 暂存工作区

git stach 把当前的改动压入一个栈

git stach list 显示这个栈的list

git  stach pop
#### 添加到暂存区的区别

git add -A   保存所有的修改

git add .    保存新的添加和修改，但是不包括删除

git add -u   保存修改和删除，但是不包括新建文件。
####  创建分支

创建分支： $ git branch feature/xiong-test

切换分支： $ git checkout feature/xiong-test

创建并切换分支： $ git checkout -b feature/xiong-test

推送本地更新到远程：git push origin develop

更新远程更新到本地：git pull origin develop

删除dev-xiong分支之前需要切换到别的分支develop上：git checkout develop

删除分支： $ git branch -d dev-xiong

强制删除分支： $ git branch -D dev-xiong

回退到某个版本：git reset --hard HEAD

更新版本：git pull origin develop
