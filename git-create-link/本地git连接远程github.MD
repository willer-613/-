<!--
 * @Author: your name
 * @Date: 2019-12-04 20:18:52
 * @LastEditTime: 2019-12-04 20:32:33
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \informal-essay\git-create-link\本地git连接远程github.MD
 -->
# 步骤

## 一、设置git的user name和email
如果你是第一次使用，或者还没有配置过的话需要操作一下命令，自行替换相应字段。

git config --global user.name "XXXX"
git config --global user.email  "XXX@gmail.com"

说明：git config --list 查看当前Git环境所有配置，还可以配置一些命令别名之类的。

## 二、检查是否存在SSH Key
cd ~/.ssh
ls
或者
ll
//看是否存在 id_rsa 和 id_rsa.pub文件，如果存在，说明已经有SSH Key

### 如果没有SSH Key，则需要先生成一下
 ssh-keygen -t rsa -C "XXXXX@gmail.com"

 ## 三、获取SSH Key
 cat id_rsa.pub
//拷贝秘钥 ssh-rsa开头

## 四、GitHub添加SSH Key
GitHub点击用户头像，选择setting--->>>新建一个SSH Key--->>取个名字，把之前拷贝的秘钥复制进去，添加就好啦。

## 五、验证和修改
测试是否成功配置SSH Key

ssh -T git@github.com

//运行结果出现类似如下
Hi XXXXXX! You've successfully authenticated, but GitHub does not provide shell access.

之前已经是https的链接，现在想要用SSH提交怎么办？
直接修改项目目录下 .git文件夹下的config文件，将地址修改一下就好了。

## 六、好，我们先来看下完成这篇文章的学习需要准备哪些东西。自然是一个本地的git仓库。

mkdir git-test
cd git-test
git init
touch README.md

执行了这几行命令之后，我们还需要在Github和码云上分别新建两个远程仓库。到这里我们就有了一个差不多的本地环境。下面我们就一起来看下是通过怎样的操作来实现陈BOSS的需求的。

##### 如何在一个项目中添加两个远程仓库 
git remote add [shortname] [url]

PS：我们解释一下这行命令的两个参数，第一个参数其实就是我们后面推送到这个远程仓库的时候都使用这个名称来代替仓库地址，第二个参数就是远程仓库的地址了，这句命令应该很好理解。

然后就在本地仓库根目录执行了下面两行命令，为本地仓库添加了两个远程仓库。

git remote add gitee https://gitee.com/XXXX/git-test.git
git remote add github https://github.com/XXXX/git-test.git

然后我们修改README文件后，可以分别往两个仓库推送代码。

git add *
git commit -m "first commit"
git push -u github master
git push -u gitee master

通过两句git push命令我们确实可以向两个远程仓库推送代码，但是作为一个喜欢偷懒的程序员的同学绝不满足于此，于是他就想有没有一种方式可以一句命令就同时push到两个远程仓库。于是乎就有了下面的操作。修改了.git/config文件中的内容。原文件内容如下：
 
    [core]
    repositoryformatversion = 0
    filemode = false
    bare = false
    logallrefupdates = true
    symlinks = false
    ignorecase = true
[remote "gitee"]
    url = https://gitee.com/xxxx/git-test.git
    fetch = +refs/heads/*:refs/remotes/gitee/*
[remote "github"]
    url = https://github.com/xxxx/git-test.git
    fetch = +refs/heads/*:refs/remotes/github/*
[branch "master"]
    remote = gitee
    merge = refs/heads/master

    修改如下

    [core]
    repositoryformatversion = 0
    filemode = false
    bare = false
    logallrefupdates = true
    symlinks = false
    ignorecase = true
[remote "origin"]
    url = https://gitee.com/xxxx/git-test.git
    url = https://github.com/xxxx/git-test.git
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master

只是将两个remote合并成了一个而已，然后再执行git push命令就会发现，会一次性向两个仓库push代码了
