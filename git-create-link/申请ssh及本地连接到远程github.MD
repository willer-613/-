<!--
 * @Author: your name
 * @Date: 2019-12-04 20:17:37
 * @LastEditTime: 2019-12-04 22:39:34
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \informal-essay\git-create-link\申请ssh及本地连接到远程github.MD
 -->
# 申请ssh及本地连接到远程github

### ![命令](https://img.shields.io/badge/SSH2Github-如何是本地git连接到远程git库-green.svg  "如何新建SSH分支便于本地git连接到远程github库")


## 申请和设置github


>[Github](https://github.com/)  该过程请自行参考

* 使用gitbash设置用户名和邮箱，打开gitbash，输入命令设置用户名和邮箱

        $ git config --global user.name "your name"
        $ git config --global user.email "your email"
## 生成ssh配置

>通过邮箱名称生成ssh key，在输入第一行命令后火提示输入保存key的地址，根据自己的结构指定文件的地址，

    $ ssh-keygen -t rsa -C "xxx@gmail.com"
    Generating public/private rsa key pair.
    Enter file in which to save the key (/c/Users/kf/.ssh/id_rsa): D:/ssh/github
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:
    Your identification has been saved in D:/ssh/github.
    Your public key has been saved in D:/ssh/github.pub.
    The key fingerprint is:
    SHA256:8J70WllHBwvnolh+LVG2pIOMKRkhzJibLjyoiZNBXvA 
    xxx@gmail.com
    The key's randomart image is:
    +---[RSA 2048]----+
    |   =. o.    . *  |
    | .o o. o + . O + |
    |  oo  + o + = = .|
    | .oE   + + . * . |
    |=..     S o + o  |
    |++.    o o + o   |
    |o=.     o +      |
    |*        o       |
    | .      .        |
    +----[SHA256]-----+
## 配置github ssh
* 执行成功后，生成目录下会生成两个文件，一个是私钥一个是公钥，找到后缀是 .pub 的公钥文件，拷贝全部文件内容到github中，具体方法是在github页面中Settings > SSH and GPG keys > New SSH key 中设置，title内容随意设置。

## 配置本地ssh
* 执行ssh-add -l 查看本地ssh配置情况

      $ ssh-add -l

>如果返回如下，则说明配置正确

    2048 SHA256:8J70WllHBwvnolh+LVG2pIOMKRkhzJibLjyoiZNBXvA /d/ssh/github (RSA)
>如果返回下面一句话，这说明没有起效

    Could not open a connection to your authentication agent.

>需要执行如下语句：

    $ ssh-agent bash
    $ ssh-add /d/ssh/github
    
>验证连接ssh配置成功后验证是否能够正确连接github

    $ ssh -T git@github.com
    Hi xxx! You've successfully authenticated, but GitHub does not provide shell access.
>与github同步将本地项目上传到github

    $ git remote add origin git@github.com:your_project.git  
    $ git push -u origin master 
    
>如果本地没有则先下载到本地再同步

    $ git clone your_project.git  
    $ git push -u origin master
