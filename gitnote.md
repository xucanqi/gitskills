2020年 3月8日    ~3月10日                

==git 学习笔记==    

--------------------
[仓库地址 ]: https://github.com/xucanqi/gitskills

其中“51note”为自己的学习笔记，改名为test1、test2的文件为学习github的使用时所作的测试，往后还将继续学习和测试，所以不作删除 

--------------------------------
## 命令表

| 命令                       | 执行的操作                           |
| -------------------------- | ------------------------------------ |
| git add 文件名             | 文件添加到缓存区                     |
| git add .                  | 将所有文件添加到缓存区               |
| git commit -m " "          | 提交到分支                           |
| git status                 | 查询仓库当前状态                     |
| git diff                   | 查看所修改的内容                     |
| Esc;   :wq;   enter        | 强制性写入文件并退出                 |
| git log                    | 显示从最近到最远的**提交**日志       |
| git reflog                 | 查看历史输入命令                     |
| git reset --hard 版本号    | 回退到此版本                         |
| cat 文件名                 | 查看此文件                           |
| git rm 文件名              | 删除文件（rm即remove）               |
| git push origin master     | 把本地master分支最新修改推送至GitHub |
| git clone                  | 克隆本地库                           |
| git branch 分支名          | 创建分支  **不加名称是查看分支表**   |
| git checkout/switch 分支名 | 切换到分支                           |
| git merge 分支名git        | 合并指定分支到当前分支               |
| git remote                 | 查看远程库信息                       |
| git rebase                 | 把分叉的提交历史“整理”成一条直线     |
| git tag 标签名             | 新建标签  **不加名称是查看标签表**   |
| git show 标签名            | 查看标签信息                         |
| git push origin 标签名     | 推送本地标签                         |

-----------------------------------------------------

## GIT ^分布式版本控制系统^  

 ### **与集中式版本控制系统的区别**：  

  ==集中式==：顾名思义，将版本库**集中存放在中央服务器**。工作时从中央服务器获得最新版本，工作后又要把文件推送给中央服务器。最大的缺点就是==需要联网==。  

  ==分布式==：工作时无需联网，每个电脑都是完整的版本库。多人协作则采用互相推送的方式。因此若自己电脑损坏不用担心数据丢失，只需要从其他人那里复制，较为安全。  

 ### **特点**：  

 无需联网、安全性高、分支管理强大等   

 ### **版本库的注意事项**：  

  1.只能跟踪文本文件的改动，无法记录图片、视频、word（二进制文件）文件的变化  

  2.不能使用windows自带记事本编辑文本文件  
 ### **把文件放入git仓库**：  
 （如文件名为“pay”）  
  1.==git add== pay.md//把文件添加到仓库  
  2.==git commit== -m"wrote a pay file" // -m 后面输入的是本次提交的说明，方便找到改动记录 另外，commit可以一次提交多个文件  

命令执行成功后，出现以下结果：  

 > git commit -m "wrote a pay file"
 [master (root-commit) 6095629] wrote a pay file
 ==1 file changed==, 1 insertion(+)
 create mode 100644 pay.md

**git仓库在本地分为三个工作区域：工作目录、暂存区、资源库**。  
**工作流程一般为**：    

1. 在工作目录中添加、修改文件；（modified）
2. 将需要进行版本管理的文件放入暂存区域；（staged）
3. 将暂存区域的文件提交到资源库；(committed)



 ### **修改已提交文件**：  

（提交文件名为pay）

  修改后，输入==git status==:查询仓库当前状态：

  >  git status
  > On branch master
  > Changes not staged for commit:
  >   (use "git add <file>..."  to update what will be committed)  
  >   (use =="git restore <file>..."== to discard changes in working directory)
  >         **==modified==**:   pay.md
  >
  > no changes added to commit (use "git add" and/or "git commit -a")

  **此时若直接在仓库存放地址中添加一个文件，结果为**：

  > git status
  >On branch master
  >Changes not staged for commit:
  >  (use "git add <file>..." to update what will be committed)
  >  (use "git restore <file>..." to discard changes in working directory)
  >        modified:   pay.md
  >
  >**Untracked files**:(没有包含在仓库里的未知文件)
  >  (use "git add <file>..." to include in what will be committed)
  >        test.md
  >
  >no changes added to commit (use "git add" and/or "git commit -a")

### **查看具体修改内容**：  
(==相对于上次提交==)

  输入==git diff==  ：**(其中加减号对应文段的添加删除)**

  >  git diff
  > **diff --git a/pay.md b/pay.md**
  > index 3975f66..830c9eb 100644
  > --- a/pay.md
  > +++ b/pay.md
  > @@ -1 +1,3 @@
  > -I will pay you back for what you did to me.
  > \ No newline at end of file
  > +i feel so tired.But I have to keep on.
  > +
  > +i can do it.
  > \ No newline at end of file
  > **diff --git a/test.md b/test.md**
  > index 33cbb87..e3d211f 100644
  > --- a/test.md
  > +++ b/test.md
  > @@ -1 +1,3 @@
  > -test
  > \ No newline at end of file
  > +test
  > +
  > +even though
  > \ No newline at end of file

 ### **查看提交日志**：
 输入==git log==(显示内容太多此处省略)  

 **如果内容过多**，可以输入 git log --pretty=oneline 

### **返回之前的版本**：  

  输入==git reset== --hard 版本号/HEAD^（HEAD表示最新提交的版本，上标表示上一版本 ）  

  **如果返回上一个版本的版本，而最新的版本找不到**：    

  在命令窗口中往上搜索最新版本的版本号即可返回“未来”版本  

  **如果在上一个情况下并且已经关闭了命令窗口**：  

  输入==git reflog== ，从中可得知对应要返回的版本号

###  **删除文件**：
 输入==git rm==文件名 （注意，误删后的恢复只能恢复到文件已提交的最新版本）    





-------------------------------------

## GitHub 远程库的使用  

### 关联一个远程库:  

输入：git remote add origin git@github.com:用户名 /仓库名字.git   

 git remote add origin git@github.com:xucanqi/gitskills.git

### 从远程库克隆：  

1. **git clone git@github.com:地址/创建的新仓库的名字.git**  


### 创建分支：  
在Git里，master分支叫主分支。    

**创建**：输入==git branch== 分支名  

**切换**：==git checkout==  分支名   （ 加上 -b 表示创建并切换）

或者 ==git switch -c== 分支名

**查看所有分支**：==git branch==  （当前分支有`*`）  

**删除分支**：==git branch -d==  分支名    

### 合并分支：  
**合并指定分支到当前分支**：==git merge== 分支名  
==此时若在fast forward模式下删除分支后悔丢掉分支信息==   

**禁用fast forward模式**：（有利于团队开发）  
输入：==git merge --no-ff -m== " "  分支名 （此次创建一个新的commit，加上-m参数）  

### 多人协作：  

查看远程库信息： git remote （加-v 显示更详细信息）  

推送分支：==git push origin== 分支名    

从远程抓取分支：==git pull==  

**多人协作的工作模式通常是这样**：

1. 首先，可以试图用`git push origin `分支名 推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin `推送就能成功！

如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to 分支名 origin/分支名`



---------------------------------------------------------------
##  产生的疑问或遇到的问题：  

1. 提交时没有输入提交说明  
2. 如果在工作区修改文件但不保存，能不能显示已修改  
3. 在克隆一个仓库时，出现**Are you sure you want to continue connecting (yes/no/[fingerprint])?**
4. 在创建版本库时一直提示没有用户名
5. 连接远程库时一直报错

--------------------------------------------------------------

## 解决问题：  

1. 出现界面：
```
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
# Your branch is up to date with 'origin/master'.
```
无法进行操作；  
查阅资料后，点击esc；输入 ：wq； 点击回车；即可退出该界面 

2. 实际尝试后，发现并没有显示已修改  
3. 原因是本地仓库和远程的SSH不匹配，直接点击yes。解决了问题。了解得知若输入yes没法解决，可以重新配置ssh：  
   - ls -al ~/.shh
   - ssh-keygen -t rsa -C "邮箱"
   - cat ~/.shh/id_rsa.pub (生成新的ssh)
   - 在github中设置新的ssh，复制新生成的ssh  

4.重新输入多次、修改用户名、修改邮箱……某一次成功了，可能是邮箱问题或者格式问题  

5.可能是地址输入错误（origin老打错）等原因。重新输入多次仍然报错。中间经历了删除ssh重新建立等过程。最后：  

输入：  

-  git remote -v  查看远程地址  
- git remote rm origin  删除添加的远程地址  
- git reomte add origin git@github.com:xucanqi/gitskills.git  重新输入地址  
- 成功  

-----------------------

## 感受

   接触git的使用和github网站自己很乐在其中，特别是在抱着疑问输入指令验证猜测的过程，是恍然大悟或者是果然如此，都令我感到十分兴奋。  但是周一周二课程几乎是满课，给我探索github留下的时间不多，而且学习过程中尝试的太多消耗了较多时间。  

​     创建命令表为以后搜索命令提供了便利，而笔记中记录下输入命令相应的结果则使自己对命令的执行更加清晰。  在搜索资料和阅读git bash的过程中遇到了一些不认识的单词，给阅读带来了困难，从中看出自己在相关方面的词汇量不够，有待加强。  

​    由于完成其他作业时间有限，标签管理和自定义git只能一带而过，记录相关命令。

