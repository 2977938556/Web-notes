## Git的基础学习

### Git基础介绍

+ Git是一个后悔药，可以后悔回去，当然现实生活中是没有的

  + ```html
    <h1>Feimao@110</h1>   2022/9/25 提交 ：“第一次提交”
    
    <h4>FeiMao@115</h4>   2022/9/25 提交："第二次提交"
    
    这个时候如果我们觉得还是第一次提交的好，那么我们就可以回退回第一个版本
    ```

    <img src="C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220925191445263.png" alt="image-20220925191445263" style="zoom: 67%;" />



+ 版本控制有两种方式一种是  集中式   的另一种是    分布式，分布式的比较好

  + 比如集中式的断网了，那么就访问不到，这样就对开发很不好
  + 分布式的就算断网了，也可以分布在 笔记本，台式机灯设备上 



## Git基础语法

+ 基础的语法

  + ls：展示目录名称 （ls  -a：显示隐藏文件      | |      ls src ：显示文件）
  + ll：展示详细的目录
  + clear：清空命令行 或者 ctrl + L
  + mkdir  "a" ：新建文件夹
  + pwd：显示当前路径 





+ Git配置的语法

    + 配置用户名称与邮箱
        + **git  config  --global user.email**    "2977938556@qq.com" ：配置邮箱
        + **git  config  --global user.name    "FeiMao"**：配置用户名 









+ 新建删除文件
  +  vim：进入文本编辑模式
  +   rm   -rf : 文件名称 ：删除文件 删除全部就写 * 
  +    touch:  文件名称：新建一个文件

  




+ 常用提交命令

  + git  status  ：查看文件状态

  + git  add  文件名称/或者写  * 可以提交全部的文件：提交文件到暂存区       

  + git   commit  -m "备注"** ：提交文件到仓库中

​    

​    

    + 文件监测
    
      + 【忽略文件或者需要跟踪文件】git中有一个文件叫.gitignore文件这个文件中我们可以设置不被Git跟踪的文件 这里设置(*index.html）就相当于设置index.html不被跟踪
    
        + 
    
          ```
          *.js
          !a.js
          /vendor/**/.php
          
          这里是意思就是所有的以js为后缀名的文件除了a.js 其他的文件都不被跟踪
          第三行是代表vendor中的目录中的d.text 不被跟踪 ，如果不写这个文件，那么整个文件夹都会被跟踪，中间的两个星号就是中间目录下面带.php的文件不会被跟踪
          
          ```
    
      + git   rm   --cached   index.js  这个方式是删除版本库中的文件不会将本地的文件给删除（git  rm  index.js）这个方法会将版本库和本地的文件都删除
      + git  mv  a.php  b.php：修改文件名称(当然也是可以在编辑器中修改名称的)
      + vim  index.php ：使用内置的编辑器进行修改   按 【i】进入编辑模式  按【:wq】退出编辑模式


​    

​    

    + 查看文件提交状态
        + git  log ：查看文件的提交的状态（按q退出）
        + git  log  -p：显示别人被修改的文件
        + git log - p -1  ：只查看当前文件名称
        + git   log  --name-only：查看日志提交的文件
        + git  commi   --amend ：设置提交日志的内容 
          + 如果第一次提交文件的时候后面又创建了一个文件也想归类到上一次提交的日志中那么 先将新文件提交到暂存区，在使用这个命令


​    

​     

​    

    + 管理暂存区中的文件
        + git  rm   --cached  index.js     :比如说我们提交文件到暂存区中，之后我们想要取消提交暂存区中的文件  就可以使用这个命令
        + git   reset   HEAD index.js    ：这个是在我们提交到最终仓库之后再次提交的时候就可以使用这个回退
        + git  checkout  --  index.js  :回退到之前没有修改的时候


​    

​    

+ branch分支

    + git  branch : 查看分支  必须要提交之后才可以设置分支
    + git  branch  ask  ：新建分支
    + git  checkout  master ：切换分支
    + git  checkout  -b  bbc  ：新建分支并切换分支
    + git    merge  ask ： 合并分支 （切记需要在master 主分支中进行合并）
    + git  branch  -d   ask ：删除分支
    + 解决冲突：就比如说一个资源被多个地方进行共享那么共同修改的地方会有冲突需要手动进行修改
    + git branch  --merged  ：查看已经被合并的分支
    + git branch  --no-merged  ：查看没有被合并的分支
    + git  branhc -D  ask ： 强制删除分支（比如说我们不想要这个功能模块我们就可以删除掉这个分支）
    + git的分支工作流
        + ![image-20220930190018158](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220930190018158.png)



​        

​        

​       

+ stash 零时存储区实例讲解
  + 比如说我们在master主分支新增了一个ask开发分支，如果我在ask中进行了修改文件并且提交到暂存区中，不想提交到最终的仓库中，此时切换分支会报错，所以需要使用以下的命令
  + git   stash : 将暂存区中进行缓存起来
  + git  stash list ： 查看缓存区
  + git  stash  apply : 恢复暂存区
  + git  stash  apply  stash@{编号}: 选择性的恢复暂存区
  + git  stash  drop  stash@{0}：删除暂存区 
  + git  stash  pop






+ 打标签

  + 比如我们写完一个项目后需要发布了那么我们就可以打上标签

  + git tag  v 1.0.18 : 设置标签

  + git  tag ：查看标签

  + git  tag -d  v1.0.18 ：删除标签

    

  

+ 打包发布

  +  git archive master --prefix='/feimao/'  --forma=zip > feimao.zip   : 打包成一个zip文件名称为feimao

     

+ rebase优化合并分支

  + ![image-20220930203831369](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220930203831369.png)

  + 这里出现的问题就是一开始ask 分支是指向master分支的第一个，结果后面主分支又提交了导致合并出现了问题，出现冲突
  + git  rebase  master   ：使用这个名字在次分支中进行使用并且解决冲突问题



+ 生成密钥【ssh】

  + ssh-keygen -t rsa -C   "2977938556@qq.com" : 会在账户目录下生成一个公钥和私钥
    + <img src="C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20221001090129503.png" alt="image-20221001090129503" style="zoom: 80%;" />
  + 配置密钥
    + <img src="C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20221001093458750.png" alt="image-20221001093458750" style="zoom: 50%;" />

  

  

  + 上传文件是有两种方式，**01：第一种是上传本地的仓库回去，02：另一种是将远程的仓库拉取下来  (分别都有HTTPS 和 HHS 这两种方式)**

    

    + 本地创建一个新仓库上传到github

      + ```js
        git init
        git add README.md
        git commit -m "first commit"
        git branch -M main
        git remote add origin git@github.com:2977938556/1.git
        git push -u origin main
        ```

    

    

    + 本地原有的仓库上传到 GitHub

      + ```js
        git remote add origin git@github.com:2977938556/1.git
        git branch -M main
        git push -u origin main
        ```

    

    

    

    + 远程仓库拉取到本地中（下载到GitHub 仓库中）

      + ```
        git clone git@github.com:2977938556/11.git
        git push  将本地的修改提交的数据更新到GitHub中
        ```

        

    ​	

+ 本地分支与远程GitHub分支
  + ````
    + git  remote -v  : 查看被链接的远程仓库
    + git  branch -a ： 查看远程仓库中的分支
    + 当我们在本地新建了一个分支，然后想更新到线上的github 那么就需要使用 ：git push --set-upstream origin 【分支名称】（这个命令需要在需要推送的分支上面执行）
    ````
  
  + 



+ 新手刚刚入职的时候使用GIT	
  + ````
    + + 01：首先获取远程仓库中的数据： git clone 
      + 02：将远程的分支合并到本地分支上面 ：git pull   origin  ask:ask
      + 03：将本地分支推送到远程仓库中：git push --set-upstream origin 【分支名称】  这个提示是可以通过 git  push 提示出来的
    
    ````
  
  + 

+ 远程分支的合并
  + ````
    + 01：切换到master分支中进行：git  pull 
    + 02：使用这个名字在需要合并的分支中，进行使用并且解决冲突问题：git  rebase  master   
    + 03：切换到 master 分支进行合并分支 ：git   merge ask 
    + 04：推送：git   push
    ````
  
  + 



+ 远程分支删除操作
  + git  push origin  --delete  ask











