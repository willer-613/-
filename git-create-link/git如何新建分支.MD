<!--
 * @Author: your name
 * @Date: 2019-12-04 20:40:02
 * @LastEditTime: 2019-12-04 20:40:59
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \informal-essay\git-create-link\git如何新建分支.MD
 -->
# git如何新建分支

##  1) 切换到基础分支，如主干

git checkout master

##  2）创建并切换到新分支

git checkout -b panda

git branch可以看到已经在panda分支上

##  3)更新分支代码并提交

git add *

git commit -m "init panda"

git push origin panda

##  4)在git代码管理界面经可以看到panda分支了，成功~~
