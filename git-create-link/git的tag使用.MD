<!--
 * @Author: your name
 * @Date: 2019-12-04 21:15:48
 * @LastEditTime: 2019-12-04 21:28:33
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \informal-essay\git-create-link\git的tag使用.MD
 -->
## git打上tag

### https://img.shields.io/badge/tag-Tag-green.svg    命令

git tag

加上-l命令可以使用通配符来过滤tag

### 新建tag

使用git tag命令跟上tag名字，直接创建一个tag。

git tag v1.0

上面创建一个名为v1.0的tag。使用git 

还可以加上-a参数来创建一个带备注的tag，备注信息由-m指定。如果你未传入-m则创建过程系统会自动为你打开编辑器让你填写备注信息。

git tag -a tagName -m "my tag"

### 查看tag详细信息

git show命令可以查看tag的详细信息，包括commit号等。

git show tagName

查看v1.0tag的详细信息及查看带备注的v1.1的详细信息

注::tag最重要的是有git commit号，后期我们可以根据这个commit号来回溯代码。

### 给指定的某个commit号加tag

打tag不必要在head之上，也可在之前的版本上打，这需要你知道某个提交对象的校验和（通过git log获取，取校验和的前几位数字即可）。

git tag -a v1.2 9fceb02 -m "my tag"

### 将tag同步到远程服务器

同提交代码后，使用git push来推送到远程服务器一样，tag也需要进行推送才能到远端服务器。
使用git push origin [tagName]推送单个分支。

git push origin v1.0

推送本地所有tag，使用git push origin --tags。

### 切换到某个tag

跟分支一样，可以直接切换到某个tag去。这个时候不位于任何分支，处于游离状态，可以考虑基于这个tag创建一个分支。

### 删除某个tag

#### 本地删除

git tag -d v0.1.2 

#### 远端删除

git push origin :refs/tags/<tagName>

git push origin :refs/tags/v0.1.2

