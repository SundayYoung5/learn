

# Git学习笔记

## 一、初识Git

### 1.Git是什么？

​	Git是世界上目前最先进的**分布式**版本控制系统。

### 2.什么是版本控制系统？

​	简单来说就是用于多人协同开发项目的技术。比如在一个项目组中多人协同完成开发任务，可以记录我们每次的文件改动，还可以让同事们协助编辑，这样就不用自己管理一堆类似的文件，也不需要把文件传来传去，我们如果想要查看某次改动，只需要在版本控制系统中看一眼就可以，十分的方便快捷，用起来如下表。

| 版本 | 文件名     | 改动人 | 说明                | 日期     |
| ---- | ---------- | ------ | ------------------- | -------- |
| V1   | Hello.java | 张三   | 输出hello，张三     | 2023/5/1 |
| V2   | Hello.java | 张三   | 改为hello，zhangsan | 2023/5/5 |
| V3   | Hello.java | 李四   | 增加hello,lisi      | 2023/5/6 |
| V4   | Hello.java | 张三   | 删除hello,lisi      | 2023/5/8 |

### 3.Git是怎么来的？

​	想必大家都听过Linux操作系统，Linux自1991年创建以来，经过多年的发展已经成为最大的服务器系统软件。Linux操作系统是靠全世界热心的志愿者参与建设的，那么世界各地的人都在为Linux系统编写代码，那Linux操作系统是如何管理的呢？事实上，在2002年之前，是由Linus本人手工合成的，但是Linux已经发展几十年了，代码库的庞大已经不能让linus通过手工的方式去管理代码了。一家好心的企业BitKMover出于好心，将自家的商用版本控制系统免费授权给Linux社区使用，但是Linux社区里面的大哥太多了，直接破解了商用版本控制系统BitKeeper，BitMover公司一气之下扬言要收回Linux社区的免费使用权。谁知Linus又高又硬，不仅没有道歉并且仅**用了两周时间自己用C写了一个分布式版本控制系统，这就是Git！**在一个月内Linux系统的源码就已经使用Git来进行管理了。后来Git迅速成为最流行的分布式版本控制系统，尤其是2008年，GitHub网站上线了，它为开源项目免费提供Git存储，无数开源项目开始迁移至GitHub，包括jQuery，PHP，Ruby等等。不知道现在BitMover公司有没有后悔，不过这也告诉我们一个道理，大神就是大神！

![image-20230519104121077](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519104121077.png)

### 4.集中式版本控制系统和分布式版本控制系统比较

**（1）集中式版本控制系统**

所有版本的数据都保存在服务器上，开发者从服务器上更新或者上传自己的代码。

所有的版本数据都存在服务器上，开发者自己的电脑上只有之前同步的版本，如果不联网，用户就看不到历史版本。

如果所有的数据都保存在一个单一的服务器上，那么这个服务器发生损坏就可能丢失掉所有的数据，当然可以定期备份。

代表的产品有：SVN、CVS、VSS

缺点：**需要联网使用**，如果网络不好，访问速度会变慢。

![image-20230518150756123](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518150756123.png)

![image-20230518150812728](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518150812728.png)

（2）分布式版本控制系统（Git）

所有的版本信息仓库全部同步到本地的每个用户，这样每个开发者在本地就可以查看所有版本历史。

可以在离线的情况下在本地提交，只需要在联网的时候push到相应的服务器或者用户那里就可以了。

由于每个用户存放的都是所有版本的数据，只要有一个用户的设备没有问题就可以恢复所有的数据，不会因为服务器损坏或者网络问题，造成不能工作。

小问题就是每个人都拥有所有版本的代码，有一定的安全隐患，同事会占用多一点本地内存（基本上没啥缺点）

![image-20230518151845428](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518151845428.png)

![image-20230518151903116](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518151903116.png)

为啥分布式控制系统也需要“中央服务器”？

​	在实际使用分布式版本控制系统的时候，其实很少在两人之间的电脑上推送版本库的修改，因为可能你们俩不在一个局域网内，两台电脑互相访问不了，也可能今天你的同事病了，他的电脑压根没有开机。因此，**分布式版本控制系统通常也有一台充当“中央服务器”的电脑，但这个服务器的作用仅仅是用来方便“交换”大家的修改，没有它大家也一样干活，只是交换修改不方便而已**。

SVN的服务器和GitHub的区别

```txt
集中式和分布式的区别是：
你的本地是否有完整的版本库历史！
假设SVN服务器没了，那你丢掉了所有历史信息，因为你的本地只有当前版本以及部分历史信息。
假设GitHub服务器没了，你不会丢掉任何git历史信息，因为你的本地有完整的版本库信息。你可以把本地的git库重新上传到另外的git服务商。
```

## 二、Git的使用

### **1.Git的下载与安装**

（1）可以去Git官网进行下载，[Git - Downloads (git-scm.com)](https://git-scm.com/downloads)

（2）官网下载太慢，我们可以使用淘宝镜像下载：http://npm.taobao.org/mirrors/git-for-windows/在下载比较慢的时候我们可以去找镜像。

**官网下载：**

![image-20230518154434724](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518154434724.png)

**淘宝镜像下载：**

![image-20230518154948942](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518154948942.png)

安装：无脑下一步即可，安装完毕就可以使用了。

![image-20230518155718936](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518155718936.png)

我们一般需要关注以下三个程序：

**Git Bash**: Unix与Linux风格的命令行，使用的最多，推荐的最多。

**Git CMD**: Windows风格的命令行。

**Git GUI**：图形界面的Git,不建议初学者使用，今尽量先熟悉常用命令。

### 2.常用的Linux命令

1、cd : 改变目录

2、cd : 回退到上一个目录，直接cd进入默认目录

3、pwd : 显示当前所在的目录路径。

4、ls(ll) : 都是列出当前目录中的所有文件，只不过ll(两个l)列出的内容更加详细。

5、touch : 新建一个文件 如touch index.js 就会在当前目录下新建一个index.js文件。

6、rm : 删除一个文件，rm index.js 就会把index.js文件删除。

7、mkdir : 新建一个目录，就是新建一个文件夹。

8、rm -r : 删除一个文件夹，rm -r src 删除scr目录

```
rm -rf / 切勿在Linux中使用！作用是删除电脑中的全部文件。
```

9、mv移动文件，mv index.html src index.html  src 是目标文件夹，这样写必须保证文件和目标文件在同一目录下面。

10、reset重新初始化终端/清屏。

11、clear清屏。

12、history查看命令历史。

13、help帮助。

14 、exit退出。

15、#表示注释。

### 3.设置用户名与邮箱

```
git config --global user.name "yourName" #名称
git config --global user.email "xxx@qq.com" #邮箱
```

![image-20230518164020298](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518164020298.png)

设置完成后我们可以查询一下是否设置成功

```
git config --global --list
```

![image-20230518164120056](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518164120056.png)

为什么要设置用户名和邮箱？

​	因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。

​	注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上**所有的Git仓库都会使用这个配置**，当然也可以对某个仓库指定不同的用户名和Email地址。

### 4.创建版本库

​	什么是版本库？

​	版本库又叫做仓库，英文名repository,你可以简单理解成一个目录，这个目录里面所有的文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻进行“还原”。

通过git init 命令把目录变成Git可以管理的仓库。

![image-20230518165836112](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518165836112.png)

在执行玩git init的命令后会发现在文件夹中多了一个.git的文件，这个目录是git来跟踪管理版本库的，没事千万不要手动修改这个目录文件里的文件，不然改乱了，就把git库给破坏了。

​	如果没有看见这个.git目录，那是因为这个目录默认是隐藏的，用ls -ah命令就可以查看。

​	![image-20230518170752710](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518170752710.png)

创建一个readme.txt文件，内容如下：

![image-20230518171548603](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518171548603.png)

第一步，用命令 git add 告诉Git，把文件添加到仓库：

```
git add readme.txt
```

![image-20230518171747031](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518171747031.png)

执行上面的命令，没有任何显示，这就对了，Linux中“没有消息就是好消息”，说明添加成功。

第二部，用git commit告诉git，把文件提交到仓库去：

```
git commit -m "wrote a readme file"
```

![image-20230518172205769](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518172205769.png)

​	简单解释一下git commit 命令，-m后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的内容，这样就能从历史中很方便的找到修改记录。

​	`git commit`命令执行成功后会告诉你，`1 file changed`：1个文件被改动（我们新添加的readme.txt文件）；`2 insertions`：插入了两行内容（readme.txt有两行内容）。

 为什么Git添加文件需要add,commit一共两步呢？

 因为commit可以一次提交很多文件，所以你可以多次add不同的文件，比如：

```
git add file1.txt
git add file2.txt file3.txt
git commit -m "add 3 files."
```

### 5.版本之间的切换

**1.版本的回退**

​	在上面的步骤下，修改readme.txt文件，修改的内容如下：

![image-20230518210844895](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518210844895.png)

我们继续修改readme.txt文件，然后git add 和 git commit :

![image-20230518211729338](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518211729338.png)

![image-20230518211740168](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518211740168.png)

在实际的开发工作中，我们的脑子不可能记住每个版本改了哪些内容，但是版本控制系统中的某个命令可以告诉我们历史记录，在git中我们使用git log命令查看

![image-20230518211709056](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518211709056.png)

git log 可以看到从最近到最远的提交日志，如果嫌输出的信息太多的话可以可以在git log后面加上--pretty=oneline

![image-20230518212446084](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518212446084.png)

大家可以看到的是，commit id都是一大串，而不是1、2、3、4……这样递增的，commit id 是一个SHA1计算出来的，用十六进制表示，不采用递增这种简单的id号的原因是因为同一个版本库可能有多个人在使用这样命名容易冲突。

我们现在想将readme.txt文件回退到上一个版本买也就是append GPL的那个版本，我们需要怎么做呢？

（1）我们首先需要知道当前版本是哪个版本，在git中用HEAD表示当前版本。我们可以看到当前版本是append GPL

![image-20230518214024798](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518214024798.png)

（2）HEAD表示的是当前版本，HEAD^表示的就是上一个版本，上上个版本就是HEAD^^,那要是往上100个版本怎么写呢？HEAD~100

（3）现在我们需要把当前版本回退到上一个版本，我们可以使用git reset 命令：

```
注意在这个地方要加上--hard
```

![image-20230518214635793](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518214635793.png)

我们可以查看一下日志记录：发现已经回退到了上一个版本。

![image-20230518214815847](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518214815847.png)

![image-20230518214921995](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518214921995.png)

（4）我们可以发现最新的那个版本append GPL已经看不到了，那么我们怎么才能再切回来呢？

方法一：在当前命令行窗口没有关的情况下，我们往上滑动，可以找到append GPL那个提交版本的commit id.

![image-20230518215248176](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518215248176.png)

那么根据这个id我们就可以退回到我们最新提交的append GPL的那个版本。

![image-20230518215420625](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518215420625.png)

版本号没必要写很全，git会自动去找，但是也不能过于短，不然会找到多个版本号，就无法确定是哪一个了。我们现在去看一下当前是哪个版本：回退成功。

![image-20230518215725543](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518215725543.png)

方法二：在当前窗口关闭的情况下，我们可以打开一个新的Git Bash界面，我们可以使用git reflog来记录我们每一次的命令，在找到最新版本的commit id 后我们可以再采用方法一中的方式回到最新的版本。

![image-20230518220652291](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518220652291.png)

**Git的版本回退原理：**

在Git内部有一个HEAD指针指向当前版本，当我们需要进行版本回退的时候，仅仅改变指针的指向就可以了，所以在Git中版本的回退速度是很快的，同时把工作区的内容给更新了。

![image-20230518221318471](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230518221318471.png)

**git log 和 git reflog的区别：**

​	**git log 和 git reflog的最大区别是能不能查询到被删除的 commit 记录和 reset 的操作记录，log不能，而reflog可以；所以以后要买后悔药就去找reflog。**

2.工作区和暂存区之间的概念

Git和其他的版本控制系统如SVN的一个不同之处就是有暂存区的概念。

**工作区（Working Directory）**

就是咋们电脑可以看到的目录，就相当于一个文件夹，我就是我们平时放代码的地方：

![image-20230519094253998](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519094253998.png)

**版本库（Repository）**

​	在我们的文件夹中也就是工作区里，有一个.git文件，这个就不算工作区，而是git的版本库。

​	在Git的版本库里面有很多的东西，其中最重要的就是stage（或者叫index）的暂存区，还有Git为我们创建的第一个分支master,以及指向master分支的指针Head

​	![image-20230519100021759](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519100021759.png)

![image-20230519100246017](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519100246017.png)

大致的工作流程以及不同指令之间进行的切换

![image-20230519100529346](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519100529346.png)

- Workspace：工作区，就是你平时存放项目代码的地方 
- Index / Stage：暂存区，用于临时存放你的改动，事实上它只是一个文件，保存即将提 交到文件列表信息
-  Repository：仓库区（或本地仓库），就是安全存放数据的位置，这里面有你提交到所有 版本的数据。其中HEAD指向最新放入仓库的版本 
- Remote：远程仓库，托管代码的服务器，可以简单的认为是你项目组中的一台电脑用于 远程数据交换

现在我们来实际操作一下：

第一步：我们可以用git status来看一下状态，发现现在工作区是“干净”的，没有对工作区做出任何修改。

![image-20230519102128101](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519102128101.png)

第二步：现在我们在工作区添加一个新的文件，license.txt内容随便写点。

![image-20230519102707996](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519102707996.png)

```
LICENSE还没有使用git add命令添加过，也就是只存在于工作区而不在暂存区，所以它的状态是Untracked
```

第三步：我们使用 git add命令将license文件添加到暂存区。

![image-20230519103252331](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519103252331.png)

![image-20230519103936290](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519103936290.png)

我们可以看到文件已将被添加到了暂存区，但是还没有被提交（没有被提交到本地库）。

第四步：我们将暂存区的文件进行提交，然后使用git status看一下状态。

![image-20230519103639189](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519103639189.png)

![image-20230519104009185](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519104009185.png)

现在暂存区的东西都被提交了，没有任何东西了。

3.管理修改

​	第一步：我们在readme.txt文件里面新增加一行内容。

![image-20230519105458977](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519105458977.png)

然后我们将readme.txt文件添加到暂缓区中，并查看一下状态。

![image-20230519110140792](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519110140792.png)

第二步：我们把文件文件内容改一下，并进行提交，然后查看一下版本库的状态。

![image-20230519111342389](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519111342389.png)



![image-20230519111503081](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519111503081.png)

我们的第二次修改没有被提交，原因是因为我们在第二次修改之后，没有将第二次的修改文件add到暂存区，所以在提交之前我们应该将文件add到在暂存区，然后一次性提交。

提交后，用`git diff HEAD -- readme.txt`命令可以查看工作区和版本库里面最新版本的区别：

![image-20230519112347034](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519112347034.png)

我们可以看到工作区域的文件有一个红色感叹号！

![image-20230519112435467](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519112435467.png)

我们可以直接add，然后提交到版本库里面去。

![image-20230519112703527](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519112703527.png)

4.撤销修改

命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销。（**下面的两种情况都是撤销工作区的修改**）

情况一：当我们在工作区的文件添加了一些不该加的内容，在还没add和提交的时候，你可以自己手动删除，或者使用命令git checkout -- readme.txt 撤销刚刚的修改。这样工作区的内容就会回到和版本库一样的状态。（这个时候加入暂存区是空的，那么撤回的版本就是到最近一次的commit记录）

![image-20230519134323535](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519134323535.png)

![image-20230519135015706](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519135015706.png)

情况二：正确的版本已经add到了暂存区，然后你又在工作区中对文件做了修改，现在想要撤回到暂存区的那个版本

当然我们还是使用git checkout --readme.txt这个命令来进行撤销。（这个时候暂存区是有内容的，因为我们进行了add操作，这个时候使用撤回命令撤回到工作区的就是暂存区的内容）

![image-20230519135642310](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519135642310.png)

在这个使用git checkout -- readme.txt这个文件的时候，大家需要注意的是--后面需要有一个空格，否则会报错。

总之，git checkout -- readme.txt就是让这个文件回到最近一次`git commit`或`git add`时的状态。



**撤销暂存区的修改**

![image-20230519141424387](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519141424387.png)



你一个不小心把这个文件添加到了暂存区里面去，这种大逆不道的话可不能被老板给看到，那我们怎么才能撤回暂存区的修改呢？

![image-20230519141631664](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519141631664.png)

我们可以看到文件只是被我们add到了暂存区，还没有提交到分支上面，咋们还有抢救的机会这个时候我们可以使用git reset HEAD readme.txt就可以把暂存区的修改给撤销掉。

![image-20230519142003465](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519142003465.png)

现在已经撤回到了工作区，那么怎么撤销工作区的修改呢？看上面git checkout -- readme.txt

**如果已经进行了提交但是还没有推送到远程仓库，怎么办呢？**

这个时候咋们可以使用版本的回退，上面有讲，命令 git reset --hard HEAD^，如果推送到了远程库直接GG。

总结：

- 1.没有`git add`时，用`git checkout -- file`
- 2.已经`git add`时，先`git reset HEAD <file>`回退到1.，再按1操作
- 3.已经`git commit`时，用`git reset`回退版本

5.删除文件

我们先在工作区新建一个文件test.txt

![image-20230519143949473](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519143949473.png)

一般情况下，我们通常直接在文件管理器中把没用的文件删了，或者用`rm`命令删了：

![image-20230519144409423](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519144409423.png)

git知道我们删除了哪个，我们可以选择删除或者删除版本库中的该文件。

恢复：因为版本库中这个文件还存在所以我们可以使用git checkout -- test.txt文件进行撤回。

删除版本库：使用git rm test.txt 然后 commit一下就可以了。现在文件就从版本库中删除掉了。

![image-20230519144921975](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519144921975.png)

```
 小提示：先手动删除文件，然后使用git rm <file>和git add<file>效果是一样的。
```

 **注意：从来没有被添加到版本库就被删除的文件，是无法恢复的！**

## 三、远程仓库

为什么需要远程仓库？这里的远程仓库以GitHub为例

​	你已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步，这样，GitHub上的仓库既可以作为备份，又可以让其他人通过该仓库来协作，真是一举多得。

### 1.添加远程仓库

首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库: 我们输入仓库名，其他的配置保持默认，点击创建。

![image-20230519154915500](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519154915500.png)

根据GitHub的提示，在本地的仓库运行下面命令

```
git remote add origin https://github.com/SundayYoung5/learngit.git
```

![image-20230519155435973](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519155435973.png)

这个命令的意思是将本地的版本库和远程的仓库关联起来。

添加后，远程库的名字就是`origin`，这是Git默认的叫法，也可以改成别的，但是`origin`这个名字一看就知道是远程库。

​	 我们把本地仓库的内容推送到远程，使用的是git push命令，实际上是把当前分支master推送到远程。

​	由于远程仓库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送到远程的新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后推送或者拉取的时候就可以简化命令。

下面我们可以把本地所有库的内容推送到远程库上面

```
git push -u origin master
```

如果用户是第一次提交，可能会设计到重新登录和输入密码的情况，具体解决办法参考下面这篇博客：

https://blog.csdn.net/qq_46780256/article/details/127285058

![image-20230519164148241](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519164148241.png)

推送成功后，我们立刻可以在GitHub的页面中看到远程库已经和本地库一模一样了。

从现在起，只要本地做了提交，我们都可以通过命令

```
git push origin master
```

把本地分支的最新修改推送到GitHub，现在你就拥有了真正的分布式版本库。

### 2.删除远程库

​	如果我们添加时地址写错了，或者就是想删除远程仓库可以使用git remote rm <name>命令，在使用前可以先用git remote -v查看远程版本库的信息：

![image-20230519170042859](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519170042859.png)



然后，根据名字删除，我们刚刚在连接远程库的时候名字叫做origin:

```
git remote rm origin
```

此处的删除是解除和本地的远程绑定关系，并不是真正意义上的删除了远程库。远程库本身是没有任何改动的。要删除真正的远程仓库，我们需要去GitHub上进行删除操作。

### 3.从远程仓库克隆

（1）在GitHub上创建一个新的仓库

![image-20230519172202302](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519172202302.png)

（2）我们可以使用ssh或者https进行克隆，使用ssh进行克隆的速度要比https链接克隆的速度快。

```
git clone 链接
```

![image-20230519172303900](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519172303900.png)

![image-20230519172345186](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519172345186.png)

![image-20230519172411700](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230519172411700.png)

可以看到克隆成功。

## 四、分支管理

什么是分支？

分支就是科幻电影里面的平行宇宙，当你正在电脑前努力学习Git的时候，平行宇宙的你正在努力学习SVN。如果两个平行宇宙相互不干扰，那没也没啥影响，不过在某个时间节点，两个平行宇宙合并了，结果你即学会了Git又学会了SVN。

![image-20230521175257243](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230521175257243.png)

其他的版本控制系统也有分支比如SVN，但是用过之后我们就会发现，这些版本控制系统创建和切换分支的速度很慢，简直让人无法忍受，但是Git的分支是与众不同的，无论创建、切换和删除分支，Git都能在1秒钟内完成切换。

### 1.创建与分支的合并

​	master分支是是一条线，Git用master指向最新的提交，再用HEAD指向master,就能确定当前分支，以及当前分支的提交点，每次提交,master分支就会向前移动一步，这样，随着你不断的提交，master分支的线也会越来越长。

![image-20230521181516689](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230521181516689.png)

​	当我们创建了一个新的分支，例如dev时，Git新建了一个指针叫dev,指向master的相同提交，再把HEAD指向dev,就表示当前分支在一个dev上：创建一个分支很快，因为除了增加一个dev指针，改改HEAD的指向，工作区的文件没有任何的变化。

![image-20230521181709354](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230521181709354.png)

​	当HEAD指正指向dev分支的时候，对工作区的修改和提交就是针对dev分支了，比如新提交一次后，dev指针往前移动一步，而master指正不变：
​	![image-20230521182017091](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230521182017091.png)

​	假如我们在dev上的工作完成了，就可以把dev合并到master上。Git是怎么完成合并的呢？

​	最简单的方法就是把master指向dev的当前提交，就完成了合并。

![image-20230521182226000](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230521182226000.png)

​	为什么说Git合并分支的速度很快！因为改改指针就可以，而工作区的内容则可以做到不变。

​	合并完分支后，我们可以删除dev分支。删除dev分支就是把dev的指针给删掉，删除后，我们就剩下一条master分支：

​	![image-20230521182557619](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230521182557619.png)

下面我们来实际操作一下：
首先我们创建dev分支，然后切换到dev分支，切换的命令如下：

```
git checkout -b dev
```

![image-20230522134608761](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522134608761.png)

```
git checkout 命令加上-b参数表示创建并切换，相当于下面的两条命令：
git branch dev
git checkout dev
```

可以使用

```
git branch命令会列出所有的分支，是当前分支的话前面会有一个*的符号，现在我们的修改提交都是在dev分支上。
```

![image-20230522134916864](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522134916864.png)

我们现在对readme.txt文件加上一行Creating a new branch is quick.

![image-20230522135628745](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522135628745.png)

选择我们将当前分支切换到master分支上，然后readme.txt文件中新增加的一行内容会不见。

![image-20230522135858146](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522135858146.png)

![image-20230522135921469](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522135921469.png)

那主分支上的刚刚添加的内容为什么会不见呢？

​	因为刚刚提交的内容在dev分支上，而master分支此刻的提交点并没有变：

![image-20230522140108395](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522140108395.png)

那么怎么才能让主分支上拥有dev分支上刚刚提交的内容呢？

​	我们需要把dev分支上的工作成果合并到master分支上去。

![image-20230522140303764](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522140303764.png)

```
git merge命令用于合并指定分支到当前分支，我们可以知道的是，当前分支是master分支，我们在合并后可以去看一下readme.txt文件中新添加的内容就有了。
```

![image-20230522140450238](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522140450238.png)

我们可以注意到这个Fast-forward信息，Git告诉我们，这次的合并是“快进模式”，也就是直接把master指向dev的当前提交，所以合并的速度是非常快的。

![image-20230522140650853](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522140650853.png)

在分支合并完成后，我们就可以放心的删除dev分支了![image-20230522141108073](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522141108073.png)

![image-20230522141217942](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522141217942.png)

```
git branch -d 可以用来删除分支，我们可以看到，删除后就只剩下主分支。
```

在Git中，创建和删除分支的速度都很快，所以Git鼓励你使用分支完成某个任务，合并后再删除分支，这和直接在master分支上工作的效果是一样的，但是过程会更加的安全。

**分支的切换**

![image-20230522141847827](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522141847827.png)

```
git checkout既可以用来进行版本回退，也可以用来进行分支的创建和切换，实际上最新版本的Git提供了git switch 命令来切换分支。
```

![image-20230522142219649](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522142219649.png)

创建并切换新的dev分支，可以使用

```
git Switch -c dev
```

直接切换到已有分支

```
git switch master
```

![image-20230522142409374](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522142409374.png)

### 2.合并冲突的解决

准备一个新的分支feature1分支，继续我们新的分支开发：

![image-20230522143520632](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522143520632.png)

然后我们将read.txt文件的最后一行改为Creating a new branch is quick AND simple.然后提交

![image-20230522143707591](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522143707591.png)

现在我们切换到master分支

![image-20230522143831193](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522143831193.png)

Git会提示我们当前的master分支比远程的master分支要超前一个提交。

我们现在在master分支上把readme.txt文件的最后一行改为

```
Creating a new branch is quick & simple.
```

现在我们进行一次提交

![image-20230522144127917](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522144127917.png)

现在，master分支和feature1分支各自都分别有新的提交，变成了这样：

![image-20230522144220685](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522144220685.png)

在这种情况下，Git无法执行”快速合并“，只能试图将各自的修改合并起来，但是这种合并可能会有冲突。

![image-20230522144351550](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522144351550.png)

我们可以看到在合并的时候，readme.txt文件存在冲突，我们需要将冲突手动解决后再提交。

我们在看一下readme.txt文件，可以看到冲突的内容。

![image-20230522144527043](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522144527043.png)

Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容，我们修改如下后保存，然后再进行提交。

现在master分支和feature1分支就变成了下图所示：

![image-20230522145122897](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522145122897.png)

我们可以使用git log --graph可以看到分支的合并情况：

![image-20230522145234123](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522145234123.png)

最后删除feature1分支

![image-20230522145404178](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522145404178.png)

### 3.分支策略管理

 我们前面提到过，通常在分支合并的时候，采用的是Fast-forward模式，但是在这种模式下，删除分支后会丢掉分支的信息。

​	我们如果强制禁用Fast-forward模式，Git就会在merge时生成一个新的commit,这样，从分支历史上就可以看出分支的信息，

我们一般采用--no-ff的方式git merge这样就可以强制禁用Fast forward.

 第一步：我们先创建一个dev分支并修改readme.txt文件，并提交。

![image-20230522151304174](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522151304174.png)

第二步：现在我们切回到master分支，准备合并dev分支，请注意--no-ff参数，表示禁用Fast forward。

![image-20230522152015709](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522152015709.png)

  现在我们使用命git log --graph命令查看一下分支历史

![image-20230522152147817](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522152147817.png)

我们可以看到，不使用Fast forward模式，merge后就像这样：

![image-20230522152337706](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522152337706.png)

**分支策略**

1.master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活。

2.那我们在哪进行开发呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本。

3.项目的团队成员都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了，所以团队合作看起来就像是下图：
![image-20230522153946749](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522153946749.png)

**小结：**

Git分支是十分强大的，在团队开发中应该被充分的使用。合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast-forward合并就看不出曾经做过合并。

### 4.Bug分支

​	在日常开发中，我们难免会碰到bug,有了bug我们就需要去修复，我们可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。

​	当我们接到一个修复代号为101的bug时，我们可以创建一个issue-101来修复它，但是我们在dev上进行的工作还没有提交。

![image-20230522161150529](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522161150529.png)

我们可以使用git stash功能，把当前的工作现场给“储藏”起来，等以后恢复现场后继续工作。

 现在假设我们需要在master分支上修复，并完成合并，最后删除issue-101分支：
![image-20230522162148109](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522162148109.png)

![image-20230522162326057](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522162326057.png)

现在bug修复完成了，我们可以切回dev分支继续工作了，但是我们可以发现工作区是干净的，那么我们刚刚的工作现场存到哪去了呢？

![image-20230522162601835](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522162601835.png)

我们可以使用下面的命令进行查看

```
git stash list
```

![image-20230522162945977](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522162945977.png)

 我们可以看到，工作现场还在，Git把stash内容存放在某个地方了，但是需要恢复一下，有两个办法：
	1.用**git stash apply**恢复，但是恢复后，stash内容并不删除，我们需要使用**git stash drop**来删除。

​	2.另一种方式是用git stash pop ,恢复的同时把stash内容也删了。

 	3.我们可以用多次stash,恢复的时候，先用git stash list查看，然后恢复指定的stash,用命令:

```
git stash apply stash@{0}
```

![image-20230522163626825](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522163626825.png)

我们刚刚是在master分支修复的bug，我们的dev分支也是在修复前的master分支上分出来的，也就是说刚刚修复的master分支上的bug其实在dev分支上也是存在的？

那么怎么在dev分支上修复同样的bug?

重复操作一次还是又更加简便的方法，当然是有更简单的方法。

```
同样的bug,要在dev上修复，我们只需要把刚刚的提交修改“复制”到dev分支。注意：我们只需要复制刚刚修复bug的那个提交，并不是把整个master分支merge过来。
```

为了操作方便，Git专门提供了一个**git cherry-pick**命令，让我们能复制一个特定的提交到当前的分支：e04e60e2

![image-20230522165712777](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522165712777.png)

```
git cherry-pick 4c805e2
```

### 5.Feature分支

​	在正式的项目开发中，我们总会需要添加很多新功能进去，我们肯定不能因为开发一个新分支而把主分支给搞坏了，所以我们现在一般都会新建一个feature分支，在这个上面进行开发，完成后合并，最后删除feature分支。

​	现在我们有了一个新的开发任务，代号为Vulcan的新功能，该计划用于下一代的星际飞船，所以我们可以创建一个分支用于开发了：
​	![image-20230522172909778](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522172909778.png)

现在开发完毕，已经添加完成也提交了。

![image-20230522173550564](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230522173550564.png)

现在准备切回dev，准备合并，但在这时候，由于预算不足，新功能需要被取消掉。

```
如果git branch -d feature-vulcan可以删除分支，如果删不掉可以强制进行删除git branch -D feature-vulcan来强删除。
```

![image-20230523084022095](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523084022095.png)

### 6.多人协助

​	当我们从远程仓库clone时，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且，远程仓库的默认地址是origin。要查看远程信息库的信息，使用**git remote**：
![image-20230523085150117](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523085150117.png)

​	或者我们可以使用**git remote -v**显示更加详细的信息：
![image-20230523085248854](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523085248854.png)

​	上面显示了可以抓取和推送的origin的地址。如果没有推送权限，就看不到push的地址。

​	**（1）推送分支**

​	推送分支就是把该分支上的所有本地提交都推送到远程库。在推送时，要指定本地分支，这样，Git就会把该分支推送到远程对应的远程分支上。

推送主分支

```
git push origin master
```

推送其他分支

```
git push origin dev
```

但是并不是所有的分支都需要往远程推送，那么，哪些分支需要推送，哪些不需要呢？

- master分支是主分支，因此要时刻与远程同步。
- dev分支是开发分支，团队所有成员都需要在上面工作，所以需要远程同步。
- bug分支用于在本地修复bug,就没必要推到远程了，除非老板要看你每周修复了几个bug。
- feature分支是否推送到远程，取决于你是否和你的小伙伴合作在上面开发。

总之，就是在Git中，分支完全可以在本地自己操作，是否需要推送，完全取决于我们自己。

**（2）抓取分支**

​	现在我们在另一个文件夹中模拟，其他人克隆工作。

![image-20230523091322914](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523091322914.png)

​	当我们从远程clone时，默认情况下，我们只能看到master分支。不信我们可以使用git branch命令进行查看。

![image-20230523093426411](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523093426411.png)

​	现在，大家需要在dev分支上开发，我们就必须创建远程的origin的dev分支到本地，于是可以用下面的这个命令来创建本地dev分支。

```
git checkout -b dev origin/dev
```

![image-20230523093509044](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523093509044.png)

现在你的同事在dev上修改，然后还把dev分支push到远程：

![image-20230523094028313](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523094028313.png)

现在你的同事已经向origin/dev分支推送了他的提交，而我们也需要对这个文件做出修改，并试图推送：
![image-20230523094910046](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523094910046.png)

推送发生了失败，Git已经提示了我们，先用git pull把最新的提交从origin/dev抓下来，然后在本地合并，冲突解决，再推送：

![image-20230523095154764](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523095154764.png)

我们发现git pull也失败了，根据提示，原因是没有指定dev与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：
![image-20230523095402543](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523095402543.png)

我们在pull一下

![image-20230523095511235](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523095511235.png)

这次pull成功，但是合并有冲突，需要手动解决一下，解决的方法和分支管理中解决冲突的方法一样。解决后，提交再push:
![image-20230523100019901](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523100019901.png)

提交成功。

因此，多人协助的工作模式通常是这样的：
1.首先，可以试图用**git push origin <branch-name>**推送自己的修改；

2.如果推送失败，因为远程分支比我们的本地要更新，需要先用git pull试图合并；

2.如果合并有冲突，则解决冲突，并在本地添加提交；

4.没有冲突或者解决掉冲突后，再用**git push origin <branch-name>**推送就能成功。

如果git pull 提示no tracking information,则说明本地分支和远程分支的链接没有创建，用命令：这就是多人协作的工作模式。

**git branch --set-upstream-to <branch-name> origin/<branch-name>**

### 7.Rebase

​	多人在同一个分支上协作时，很容易出现冲突，即使没有冲突，最后push的童鞋不得不先pull，在本地合并，然后才能push成功。

![image-20230523102724060](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523102724060.png)

怎么才能让这个线变直一点呢？

我们可以使用git rebase命令。

rebase操作可以把本地未push的分叉提交历史整理成直线。

rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

![image-20230523103944267](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523103944267.png)

可以看到的是远程的提交历史也是一条直线。

```
git rebase --quit
```

![image-20230523104155701](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523104155701.png)

上面的命令可以退出rebase。

## 五、标签管理

什么是标签管理？

​	发布一个版本的时候，我们通常会先在版本库中打一个标签（tag）,这样就唯一确定了打标签时刻的版本。

​	Git的标签虽然是版本库的快照，但其实它就是指向commit的指针（分支是可以移动的，但是标签是不会移动的），所以创建标签和删除标签都输瞬时完成的。

​	**创建标签**

​	在Git中打标签是比较简单的，首先我们需要切换到要打标签的分支上。

![image-20230523110427197](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523110427197.png)

默认标签是打在最新提交的commit上的。有时候，如果忘了打标签，比如，现在已经是星期五，但是周一的标签没有打，怎么办？

方法是找到历史提交的commit id 然后打上标签就行了。

![image-20230523111033949](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523111033949.png)

注意：标签不是按时间顺序列出，而是按字母排序的。可以用git show <tagname>查看标签信息。

还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字

![image-20230523111616419](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523111616419.png)

```
注意：标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签。
```

**操作标签**

如果标签打错了，也可以删除：

```
git tag -d v0.1
```

![image-20230523112004760](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523112004760.png)

因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。

如果要推送某个标签到远程，使用命令git push origin <tagname>

![image-20230523112216385](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523112216385.png)

或者，一次性推送全部尚未推送到远程的标签：
![image-20230523112552074](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523112552074.png)

如果标签已经推送到了远程，要删除远程标签就麻烦了一点，先从本地删除。

![image-20230523112741889](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523112741889.png)

然后再从远程删除。删除命令也是push,但是格式如下：
![image-20230523112847907](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523112847907.png)

要看看远程是否删除了标签，可以登录GitHub进行查看。

## 六、使用GitHub

​	**GitHub简介：**

​	我们一直使用GitHub作为免费的远程仓库，如果是个人的开源项目。如果是个人开源项目，放到GitHub上是完全没有问题的，然后GitHub还是一个开源协作的社区，通过GitHub，既可以让别人参与你的开源项目，也可以参与别人的开源项目。

- ​	在GitHub上可以任意Fork开源仓库
- ​	自己拥有Fork后的仓库的读写权限
- ​    可以推送pull request给官方仓库来贡献代码

## 七、使用Gitee

​	在使用GitHub的时候我们最常遇到的情况就是访问的速度太慢，有时候还会出现无法连接等情况。那么我们就可以使用国内的Git托管服务----Gitee

## 八、自定义Git

​	Git有很多可配置项，比如让Git显示颜色，会让命令看起来更加的醒目。

```
git config --global color.ui true
```

### 1.忽略特殊文件

​	为什么要忽略特殊文件？

​	有些时候，我们必须把某些文件放到Git工作目录中，但又不能提交它们，比如保存了数据库密码的配置文件等等，每次git status都会显示Untracked files……，有强迫症的兄弟们肯定受不了。

在Git中我们可以在Git的根目录下创建一个特殊的.gitignore文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。

​	我们不需要从头写.gitignore文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。

**忽略文件的原则是：**
1.忽略操作系统自动生成的文件，比如缩略图等。

2.忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那么自动生成生成的文件就没有必要放进版本库，比如java编译产生的.class文件。

3.忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

### 2.配置别名

​	在Git中我们可以简化指令的操作，我们可以设置别名简化命令的操作。

​	![image-20230523143309944](C:\Users\86150\AppData\Roaming\Typora\typora-user-images\image-20230523143309944.png)

类似于这样的操作还有很多。

比如：

```
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch
```

### 3.搭建Git服务器

​	GitHub就是一个免费托管开源代码的远程仓库，但是对于公司来说，产品的源码一般是商业机密，如果公司不想给GitHub交保护费，那就只能自己搭建一台Git服务器作为私有仓库使用，搭建Git服务器需要准备一台Linux机器。

最后常用的Git命令清单可以点击这个链接下载：

https://liaoxuefeng.gitee.io/resource.liaoxuefeng.com/git/git-cheat-sheet.pdf

本文为廖雪峰老师Git教程的学习笔记，大家可以看廖雪峰老师写的Git教程通俗易懂，强烈推荐https://www.liaoxuefeng.com。