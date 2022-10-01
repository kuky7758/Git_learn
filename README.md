# Git_learn
学习Git记录

实用主义
准备阶段
进入 Git官网 下载合适你的安装包，安装好 Git 后，打开命令行工具，进入工作文件夹（为了便于理解我们在系统桌面上演示），创建一个新的demo文件夹。

图片
进入 Github网站 注册一个账号并登录，进入 我的博客，点击 Clone or download ，再点击 Use HTTPS ，复制项目地址 https://github.com/gafish/gafish.github.com.git 备用。

再回到命令行工具，一切就绪，接下来进入本文的重点。

常用操作
所谓实用主义，就是掌握了以下知识就可以玩转 Git，轻松应对90%以上的需求。以下是实用主义型的Git命令列表，先大致看一下

git clone
git config
git branch
git checkout
git status
git add
git commit
git push
git pull
git log
git tag
接下来，将通过对 我的博客 仓库进行实例操作，讲解如何使用 Git 拉取代码到提交代码的整个流程。

git clone
“从git服务器拉取代码
git clone https://github.com/gafish/gafish.github.com.git
代码下载完成后在当前文件夹中会有一个 gafish.github.com 的目录，通过 cd gafish.github.com 命令进入目录。

git config
“配置开发者用户名和邮箱
git config user.name gafish
git config user.email gafish@qqqq.com
每次代码提交的时候都会生成一条提交记录，其中会包含当前配置的用户名和邮箱。

git branch
“创建、重命名、查看、删除项目分支，通过 Git 做项目开发时，一般都是在开发分支中进行，开发完成后合并分支到主干。
git branch daily/0.0.0
创建一个名为 daily/0.0.0 的日常开发分支，分支名只要不包括特殊字符即可。

git branch -m daily/0.0.0 daily/0.0.1
如果觉得之前的分支名不合适，可以为新建的分支重命名，重命名分支名为 daily/0.0.1

git branch
通过不带参数的branch命令可以查看当前项目分支列表

git branch -d daily/0.0.1
如果分支已经完成使命则可以通过 -d 参数将分支删除，这里为了继续下一步操作，暂不执行删除操作

git checkout
“切换分支
git checkout daily/0.0.1
切换到 daily/0.0.1 分支，后续的操作将在这个分支上进行

git status
“查看文件变动状态
通过任何你喜欢的编辑器对项目中的 README.md 文件做一些改动，保存。

git status
通过 git status 命令可以看到文件当前状态 Changes not staged for commit: （改动文件未提交到暂存区）

On branch daily/0.0.1
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
    modified:   README.md
no changes added to commit (use "git add" and/or "git commit -a")
git add
“添加文件变动到暂存区
git add README.md
通过指定文件名 README.md 可以将该文件添加到暂存区，如果想添加所有文件可用 git add . 命令，这时候可通过 git status 看到文件当前状态 Changes to be committed: （文件已提交到暂存区）

On branch daily/0.0.1
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
    modified:   README.md
git commit
“提交文件变动到版本库
git commit -m '这里写提交原因'
通过 -m 参数可直接在命令行里输入提交描述文本

git push
“将本地的代码改动推送到服务器
git push origin daily/0.0.1
origin 指代的是当前的git服务器地址，这行命令的意思是把 daily/0.0.1 分支推送到服务器，当看到命令行返回如下字符表示推送成功了。

Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 267 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local objects.
To https://github.com/gafish/gafish.github.com.git
 * [new branch]      daily/0.0.1 -> daily/0.0.1
现在我们回到Github网站的项目首页，点击 Branch:master 下拉按钮，就会看到刚才推送的 daily/00.1 分支了

git pull
“将服务器上的最新代码拉取到本地
git pull origin daily/0.0.1
如果其它项目成员对项目做了改动并推送到服务器，我们需要将最新的改动更新到本地，这里我们来模拟一下这种情况。

进入Github网站的项目首页，再进入 daily/0.0.1 分支，在线对 README.md 文件做一些修改并保存，然后在命令中执行以上命令，它将把刚才在线修改的部分拉取到本地，用编辑器打开 README.md ，你会发现文件已经跟线上的内容同步了。

如果线上代码做了变动，而你本地的代码也有变动，拉取的代码就有可能会跟你本地的改动冲突，一般情况下 Git 会自动处理这种冲突合并，但如果改动的是同一行，那就需要手动来合并代码，编辑文件，保存最新的改动，再通过 git add . 和 git commit -m 'xxx' 来提交合并。

git log
“查看版本提交记录
git log
通过以上命令，我们可以查看整个项目的版本提交记录，它里面包含了提交人、日期、提交原因等信息，得到的结果如下：

commit c334730f8dba5096c54c8ac04fdc2b31ede7107a
Author: gafish <gafish@qqqq.com>
Date:   Wed Jan 11 09:44:13 2017 +0800
    Update README.md
commit ba6e3d21fcb1c87a718d2a73cdd11261eb672b2a
Author: gafish <gafish@qqqq.com>
Date:   Wed Jan 11 09:31:33 2017 +0800
    test
.....
提交记录可能会非常多，按 J 键往下翻，按 K 键往上翻，按 Q 键退出查看

git tag
“为项目标记里程碑
git tag publish/0.0.1
git push origin publish/0.0.1
当我们完成某个功能需求准备发布上线时，应该将此次完整的项目代码做个标记，并将这个标记好的版本发布到线上，这里我们以 publish/0.0.1 为标记名并发布，当看到命令行返回如下内容则表示发布成功了

Total 0 (delta 0), reused 0 (delta 0)
To https://github.com/gafish/gafish.github.com.git
 * [new tag]         publish/0.0.1 -> publish/0.0.1
.gitignore
“设置哪些内容不需要推送到服务器，这是一个配置文件
touch .gitignore
.gitignore 不是 Git 命令，而在项目中的一个文件，通过设置 .gitignore 的内容告诉 Git 哪些文件应该被忽略不需要推送到服务器，通过以上命令可以创建一个 .gitignore 文件，并在编辑器中打开文件，每一行代表一个要忽略的文件或目录，如：

demo.html
build/
以上内容的意思是 Git 将忽略 demo.html 文件 和 build/ 目录，这些内容不会被推送到服务器上
