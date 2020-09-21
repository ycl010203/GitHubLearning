### 创建仓库

$ mkdir git-tutorial
$ cd git-tutorial
$ git init

如果初始化成功，执行了git init命令的目录下就会生成.git 目录。这个.git 目录里存储着管理当前目录内容所需的仓库数据。
在Git 中，我们将这个目录的内容称为“附属于该仓库的工作树”。文件的编辑等操作在工作树中进行，然后记录到仓库中，以此管理文件的历史快照。

如果想将文件恢复到原先的状态，可以从仓库中调取之前的快照，在工作树中打开。开发者可以通过这种方式获取以往的文件。

##### 查看提交后状态

##### $ git status

On branch master

结果显示了我们当前正处于master 分支下。

Initial commit

nothing to commit (create/copy files and use "git add" to track)

接着还显示了没有可提交的内容。所谓提交（Commit），是指“记录工作树中所有文件的当前状态”。

##### 查看提交日志

##### $ git log

commit 1730ee9f35bd3a44a59449d7f2504868ed67ddea (HEAD -> master)
Author: ycl010203 <670388686@qq.com>
Date:   Mon Sep 14 10:37:05 2020 +0800

First commit

##### 



### 编写代码，添加文件（例如 README.md）

$ touch README.md

$ git status

没有添加至Git 仓库，所以显示为Untracked files。



### 提交至仓库

$ git add hello_world.cpp 

$ git commit -m "add hello world script by cpp"

git add 将hello_word.cpp 放入(文件暂存区)。

git commit -m "描述"     将文件加入暂存区。

这样一来，这个文件就进入了版本管理系统的管理之下。今后的更改管理都交由Git 进行。

##### 记述详细提交信息

直接执行git commit命令

##### $ git commit

在编辑器中记述提交信息的格式如下。
● 第一行：用一行文字简述提交的更改内容
● 第二行：空行
● 第三行以后：记述更改的原因和详细内容



### 更新github仓库

git push



### ●git log—查看提交日志

##### --只显示提交信息的第一行（哈希和作者）

$ git log --pretty=short

##### --只显示指定目录、文件的日志

$ git log README.md

##### --显示文件的改动

$ git log -p README.md

### ●git diff—查看更改前后的差别

git diff命令可以查看工作树、暂存区、最新提交之间的差别。

##### --查看当前工作树与暂存区的差别。

$ git diff

##### --查看工作树和最新提交的差别

$ git diff HEAD

##### 在执行git commit命令之前先执行git diff HEAD命令，查看本次提交与上次提交之间有什么差别，等

##### 确认完毕后再进行提交。这里的HEAD 是指向当前分支中最新一次提交的指针。



## 分支操作

在进行多个并行作业时，我们会用到分支。在这类并行开发的过程中，往往同时存在多个最新代码状态。从master 分支创建feature-A 分支和fix-B 分支后，每个分支中都拥有自己的最新代码。

master 分支是Git 默认创建的分支，因此基本上所有开发都是以这个分支为中心进行的。

### ●git branch——显示分支一览表

git branch命令可以将分支名列表显示，同时可以确认当前所在分支

$ git branch

### ●git checkout -b——创建、切换分支

以当前的master 分支为基础创建新的分支，需要用到git checkout -b命令。

##### --切换到feature-A 分支并进行提交

$ git checkout -b feature-A

##### 或者

$ git branch feature-A(创建分支)
$ git checkout feature-A(切换分支)

##### 在这个状态下像正常开发那样修改代码、执行git add命令并进行提交的话，代码就会提交至feature-A 分支。像这样不断对一个分支（例如feature-A）进行提交的操作，我们称为“培育分支”。

##### --切换回上一个分支

$ git checkout -

#### 特性分支

###### 特性分支顾名思义，是集中实现单一特性（主题），除此之外不进行任何作业的分支。

###### 在日常开发中，往往会创建数个特性分支，同时在此之外再保留一个随时可以发布软件的稳定分支。

###### 稳定分支的角色通常由master 分支担当。

###### 之前我们创建了feature-A 分支，这一分支主要实现feature-A，除feature-A 的实现之外不进行任何作业。

###### 即便在开发过程中发现了BUG，也需要再为feature-A创建新的分支，在新分支中进行修正。

###### 基于特定主题的作业在特性分支中进行，主题完成后再与master 分支合并。只要保持这样一个开发流程，就能保证master 分支可以随时供人查看。

#### 主干分支

###### 主干分支是特性分支的原点，同时也是合并的终点。通常人们会用master 分支作为主干分支。主干分支中并没有开发到一半的代码，可以随时供他人查看。

###### 有时我们需要让这个主干分支总是配置在正式环境中，有时又需要用标签Tag 等创建版本信息，同时管理多个版本发布。拥有多个版本发布时，主干分支也有多个。

### ●git merge——合并分支

##### 首先切换到master 分支。

$ git checkout master

##### 为了在历史记录中记录下本次分支合并，需要创建合并提交。因此，在合并时加上--no-ff参数。

$ git merge --no-ff feature-A

##### 随后编辑器会启动，用于录入合并提交的信息。

###### 默认信息中已经包含了是从feature-A 分支合并过来的相关内容，所以可不必做任何更改。将编辑器中显示的内容保存，关闭编辑器

##### 这样一来，feature-A 分支的内容就合并到master 分支中了。（本地合并并没有到网上）

### ●git log --graph——以图表形式查看分支

敲回车退出

## 更改提交的操作

### ●git reset——回溯历史版本

###### Git 的另一特征便是可以灵活操作历史版本。借助分散仓库的优势，可以在不影响其他仓库的前提下对历史版本进行操作。

###### 在这里，为了让各位熟悉对历史版本的操作，我们先回溯历史版本，创建一个名为fix-B 的特性分支。

##### --回溯到创建feature-A 分支前

###### 回溯到上一节feature-A 分支创建之前，创建一个名为fix-B 的特性分支。

###### 要让仓库的HEAD、暂存区、当前工作树回溯到指定状态，需要用到git rest --hard命令。只要提供目标时间点的哈希值A，就可以完全恢复至该时间点的状态。

$ git reset --hard 2f81f3ce3ad1ec95ccfbef06bd5be1b2d8585c1d

##### --创建并转换到fix-B 分支

$ git checkout -b fix-B

###### 对文件修改后 通过git add 放暂存区， git commit -m "描述"提交到本地

#### 转换到feature-A分支合并后的状态

##### git log命令只能查看以当前状态为终点的历史日志。

##### 所以这里要使用git reflog命令，查看当前仓库的操作日志。在日志中找出回溯历史之前的哈希值，

通过git reset --hard命令恢复到回溯历史前的状态。

$ git reflog
30ca4da (HEAD -> fix-B) HEAD@{0}: commit: Fix B
2f81f3c (master) HEAD@{1}: checkout: moving from master to fix-B
2f81f3c (master) HEAD@{2}: reset: moving to 2f81f3ce3ad1ec95ccfbef06bd5be1b2d8585c1d
b7c04e6 HEAD@{3}: merge feature-A: Merge made by the 'recursive' strategy.
2f81f3c (master) HEAD@{4}: checkout: moving from feature-A to master
857b446 (feature-A) HEAD@{5}: commit: add feature-A
2f81f3c (master) HEAD@{6}: checkout: moving from master to feature-A
2f81f3c (master) HEAD@{7}: commit: add index
1730ee9 HEAD@{8}: commit (initial): First commit

最前面的7个字符就是哈希值（git reset --hard输入4位以上就可）

$ git checkout master
$ git reset --hard 83b0b94

##### 将HEAD、暂存区、工作树恢复到master与feature-A合并后的状态。

#### 接下来合并fix-B分支，并与（master与feature-A合并后的状态）一起合并，并消除冲突

$ git merge --no-ff fix-B

冲突解决后，执行git add命令与git commit命令。然后用 git log --branch查看分支情况

### ●git commit --amend——修改提交信息


我们将上一条提交信息记为了"Fix conflict"，但它其实是fix-B 分支的合并，解决冲突只是过程之一，这样标记实在不妥。于是，我们要修改这条提交信息。

$ git commit --amend

执行上面的命令后，编辑器就会启动。编辑器中显示的内容如上所示，其中包含之前的提交信息。请将提交信息的部分修改为Merge branch 'fix-B'，然后保存文件，关闭编辑器。

现在执行git log --graph命令，可以看到提交日志中的相应内容也已经被修改。

### ●git rebase -i——压缩历史（慎用慎用）

##### 在合并特性分支之前，如果发现已提交的内容中有些许拼写错误等，不妨提交一个修改，然后将这个修改包含到前一个提交之中，压缩成一个历史记录。

###### 创建feature-C 分支

###### 在README.md 文件中添加一行文字，并且故意留下拼写错误，以便之后修正。

将git add 与 git commit整合起来提交，  git commit -am "描述"

$ git commit -am "Add feature-C"

##### 修正拼写错误，并用git查看差别

$ git diff

##### 然后进行提交。

git commit -am "Fix typo"

###### 错字漏字等失误称作typo，所以将提交信息记为"Fix typo"

##### 更改历史

将"Fix typo"修正的内容与之前一次的提交合并，在历史记录中合并为一次完美的提交。

$ git rebase -i HEAD~2

##### 用上述方式执行git rebase命令，可以选定当前分支中包含HEAD（最新提交）在内的两个最新历史记录为对象，并在编辑器中打开。

#### 将要删除的记录中的最前的pick改写成fixup

###### 这样一来，Fix typo 就从历史中被抹去，也就相当于Add feature-C中从来没有出现过拼写错误。这算是一种良性的历史改写。

#### 合并至master 分支

## 推送至远程仓库

###### 在GitHub 上新建一个仓库。为防止与其他仓库混淆，仓库名请与本地仓库保持一致，即git-tutorial。

###### 创建时请不要勾选Initialize this repository with a README 选项。因为一旦勾选该选项，GitHub 一侧的仓库就会自动生成README 文件，从创建之初便与本地仓库失去了整合性。虽然到时也可以强制覆盖，但为防止这一情况发生还是建议不要勾选该选项，直接点击Create repository 创建仓库。

### ●git remote add——添加远程仓库

$ git remote add origin git@github.com:ycl010203/git-tutorial.git

###### Git 会自动将远程仓库的名称设置为origin（标识符）。

### ●git push——推送至远程仓库

$ git pull origin master --allow-unrelated-histories

#### --推送至master 分支

$ git push -u origin master

##### 报错，处理方法，先

##### $ git pull origin master --allow-unrelated-histories

--allow-unrelated-histories 把网上的分支获取下来，与本地强行合并

##### 然后再

$ git push -u origin master

-u参数可以在推送的同时，将origin 仓库的master 分支设置为本地仓库当前分支的upstream（上游）。添加了这个参数，将来运行git pull命令从远程仓库获取内容时，本地仓库的这个分支就可以直接从origin 的master 分支获取内容，省去了另外添加参数的麻烦

#### --推送至master 以外的分支

我们在本地仓库中创建feature-D 分支，并将它以同名形式push 至远程仓库。

$ git checkout -b feature-D

###### 在本地仓库中创建了feature-D 分支，现在将它push 给远程仓库并保持分支名称不变。

#### 原始提交至远程仓库

$ git push -u origin feature-D

## 从远程仓库获取

在另一个目录下新建一个本地仓库，学习从远程仓库获取内容的相关操作。这就相当于我们刚刚执
行过push 操作的目标仓库又有了另一名新开发者来共同开发。

### ●git clone——获取远程仓库

切换到其他目录下，将GitHub 上的仓库clone 到本地。注意不要与之前操作的仓库在同一目录下。

$ git clone git@github.com:ycl010203/git-tutorial.git

$ cd git-tutorial

###### 进入本地仓库时，会默认处于master 分支下，同时系统会自动将origin 设置成该远程仓库的标识符。也就是说，当前本地仓库的master 分支与GitHub 端远程仓库（origin）的master 分支在内容上是完全相同的。

### --git branch -a查看当前分支的相关信息。添加-a参数可以同时显示本地仓库和远程仓库的分支信息。

$ git branch -a

* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/feature-D
  remotes/origin/master

##### 本地head指向master ，远程仓库分支信息

### --获取远程的feature-D 分支(并创建)

$ git checkout -b feature-D origin/feature-D

##### -b 参数的后面是本地仓库中新建分支的名称。新建分支名称后面是获取来源的分支名称。例子中指定了origin/feature-D，就是说以名为origin 的仓库（这里指GitHub 端的仓库）的feature-D 分支为来源

### --向本地的feature-D 分支提交更改

对 README.md作修改

###### git diff 查看更改

$ git diff

$ git commit -am "Add feature-D"

### --推送feature-D 分支（非原始提交至仓库）

$ git push



### ●git pull——获取最新的远程仓库分支

###### 这边的本地仓库中只创建了feature-D 分支，并没有在feature-D 分支中进行任何提交。然而远程仓库的feature-D 分支中已经有了我们刚刚推送的提交。这时我们就可以使用git pull 命令，将本地的feature-D 分支更新到最新状态。当前分支为feature-D 分支。

$ git pull origin feature-D

今后只需要像平常一样在本地进行提交再push 给远程仓库，就可以与其他开发者同时在同一个分支中进行作业，不断给feature-D 增加新功能。
如果两人同时修改了同一部分的源代码，push 时就很容易发生冲突。所以多名开发者在同一个分支中进行作业时，为减少冲突情况的发生，建议更频繁地进行push 和pull 操作。

## GitHub的功能（技巧）

##### 1、shift +/键盘快捷键，按照快捷键提示直接输入 字母键，不用按 ctrl 和shift

##### 2、文件内容的左侧会显示该文件的行号。假如我们点击第10 行的行号， 这一行就会被高亮标记为黄色， 同时URL 末尾会自动添加“#L10”。使用这个URL，程序员们在交流时，就可以将讨论明确指向某一行。另外，如果将“#L10”改成“#L10-15”，则会标记该文件的第10 ～ 15 行。

##### 3、通过部分名称搜索文件

在仓库页面试着按下键盘的t 键，然后输入要找的目录或文件的部分名称。筛选器会在仓库的目录和文件中进行筛选，搜索出您要找的文件。这种方式要比一级级查看目录和文件快得多，请积极利用。

##### 4、查看差别

###### a、查看master 分支与feature-D分支之间的差别

https://github.com/ycl010203/git-tutorial/compare/master...feature-D

###### b、查看master 分支在最近7 天内的差别

http://github.com/ycl010203/git-tutorial/compare/master@{7.day.ago}...master

###### c、查看与指定日期之间的差别

http://github.com/ycl010203/git-tutorial/compare/master@{2020-10-15}...master

## Issue

开发者们为了跟踪BUG 及进行软件相关讨论，进而方便管理，创建了Issue。

GitHub 的Issue 及评论可以使用GFMA 语法进行描述，从而获得丰
富的表现力。比如像图5.10 中那样描述，然后点击Preview，就可以看
到图5.11 中那种标记后的效果。

### ●添加标签以便整理(在右侧)

Issue 可以通过添加标签（Label）来进行整理。

添加标签后，Issue的左侧就会显示标签。点击页面左侧的标签，还可以只显示
该类标签的Issue。
标签可以自由创建。既可以按语言和技术分类，也可以按照BUG、任务、备忘等作业类型分类。各位可以按照需要选择便于整理的标签。

##### 提个小建议：其实在Issue 比较少的情况下不必每个都添加标签，大可等Issue 积攒到一定数量，只有进行筛选才能清晰把握时再添加标签。

### ●为特定代码添加issue

github还支持您为仓库中或者是pull request中的特定代码行添加issue

###### 要为特定的代码添加一个issue，首先需要找到存储该代码的文件或者是pull request

###### \* 通过点击代码前面的行数的标号高亮代码（如果要选中多行，则需先选定起始行，再通过shift和左键点击结束行行号即可）

\* 选中后点击左部的下拉菜单，选中open new issue，之后稍加编辑后即可提交

##### 同样，我们可以通过为一个issue添加代码链接来添加代码

##### 操作同上，只是在最后的菜单选择中，选中copy permalink，之后粘贴到issue中即可。

### ●添加里程碑以便管理

设置里程碑，就可以用Issue 来管理任务。

把 issue加入里程碑，通过里程碑来管理issue

### ●通过提交信息操作Issue（p120没看懂）

##### 在相关Issue 中显示提交



## Pull Request

##### Pull Request 是用户修改代码后向对方仓库发送采纳请求的功能，也是GitHub 的核心功能。

在Pull Request 页面能够列表查看当前处于Open 状态的Pull Request。通过点击页面左部和上部的选项可以进行筛选和重新排列。
在列表中点击特定的Pull Request 就会进入详细页面。页面上方显示着这次是从谁的哪个分支向谁的哪个分支发送了PullRequest。下面，我们对各个标签（Tag）页进行讲解。

##### 获取diff 格式与patch 格式的文件

对长期投身于软件开发的人来说，有时可能会希望以diff 格式文件和patch 格式文件的形式来处理Pull Request。
举个例子，假设Pull Request 的URL 如下所示。 https://github.com/用户名/仓库名/pull/28

如果想获取diff 格式的文件，只要像下面这样在URL 末尾添加.diff 即可。https://github.com/用户名/仓库名/pull/28.diff

同理， 想要patch 格式的文件， 只需要在URL 末尾添加.patch 即可。https://github.com/用户名/仓库名/pull/28.patch

#### Conversation

在Conversation 标签页中，可以查看与当前Pull Request 相关的所有评论以及提交的历史记录。人们在这里添加评论互相探讨，发送提交落实讨论内容的整个过程会按时间顺序列出，供用户查看。各位在查看过程中如果有自己的想法，不妨积极地添加评论参与探讨。提交日志的右侧有该提交的哈希值，点击链接即可确认相应提交的详细信息。

###### 引用评论

###### 在Conversation 中人们通过添加评论进行对话。这里有一个简单方法可以帮您引用某个人的评论。选中想引用的评论然后按R 键，被选择的部分就会自动以评论语法写入评论文本框

#### Commits

在Commits 标签页中，按时间顺序列表显示了与当前Pull Request相关的提交。标签上的数字为提交的次数。每个提交右侧的哈希值可以连接到该提交的代码。

###### 在评论中应用表情

###### 在评论中输入“:”（冒号）便会启动表情自动补全功能。只要输入几个与该表情相关的字母，系统就会为您筛选自动补全的对象。选择想要的表情，其相应代码（前后都有冒号的字符串）便会插入到文本框中。

#### Files Changed

###### Files Changed 标签页中可以查看当前Pull Request 更改的文件内容以及前后差别。标签上的数字表示新建及被更改的文件数。

##### 默认情况下系统会将空格的不同也高亮显示，所以在空格有改动的情况下会难以阅读。这时只要在URL 的末尾添加“?w=1”就可以不显示空格的差别。

###### 将鼠标指针放到被更改行行号的左侧，我们会看到一个加号。点击这个加号可以在代码中插入评论。这样，评论是针对哪行代码的就一目了然了。



## Wiki

Wiki 是一个使用简单的语法就能编写文档的功能。所有有权限的人都可以对文章进行修改，所以比较适合多人共同编写文章的情况。

创建、编辑文档时不必另外启动软件，用起来十分方便，非常适合用来针对更新频率较高的软件进行文档等信息方面的汇总。与Issue 和Pull Request 相同，Wiki 也支持GFM 语法，所以可以轻
松创建表现力丰富的文档。点击页面右上角的New Page 按钮便可以创建新的Wiki 页。

Wiki 功能本身的数据也在Git 中进行管理。点击Clone URL 按钮可以将当前Wiki 的Git 仓库URL 复制到剪贴板中。用户能够通过clone操作获取Wiki 仓库，然后在本地创建、编辑页面，进行提交再push，便可以完成对Wiki 的创建及编辑工作。

一般情况下，Wiki 中记载着软件相关的FAQ、文档、代码示例及解说等信息。各位在使用GitHub 上开发的软件前，建议先查看一遍Wiki。

##### 在Wiki 中显示侧边栏（待尝试）

所有Wiki 页面都可以显示侧边栏。做法很简单，只要创建名为“_sidebar”的页面即可。_sidebar 页不会显示在Pages 的页面一览中。在编辑各页面时页面下部会附加Sidebar 段（图a），用户可以在这里编辑侧边栏的内容。



## Network

以图表形式显示包括克隆仓库在内的所有分支的提交。从图上可以直观地看出每个人做了多少工作。
将鼠标指针停留在表中提交或合并的点上，可以查看相应的参考内容。



## Settings

1. #### Options

   - ##### Settings

     在这里可以修改仓库名称，设置显示仓库URL 时默认显示的分支。

   - ##### Features

     这里可以更改Wiki 和Issue 的相关设置。如果想关闭某些功能，只要取消已勾选的相应复选框，该功能就会从菜单中移除，无法使用。

   - ##### GitHub Pages

     GitHub 有一个名为GitHub Pages 的仓库，用户可以利用该仓库中的资料创建Web 页，用来发布仓库中软件的相关信息。如果已经创建过GitHub Pages，则会显示相应URL。点击Automatic Page Generator 即可以自动创建GitHub Pages。

   - ##### Danger Zone

     这里都是一些需要格外留意的设置。在这里，用户可以将仓库改为私有或是变更仓库所有者，甚至删除仓库本身。这些设置有可能影响到其他人，在变更时一定要谨慎。

2. #### Collaborators

   用户主要在这里设置仓库的访问权限。如果仓库隶属于个人账户，那么可以添加GitHub 的用户名，赋予该用户直接读写仓库的权限。

   不过，如果仓库隶属于Organization 账户，则需要先创建Team，然后赋予该Team 读写仓库的权限。像这样使用Organization 账户可以高效地设置仓库权限，在公司等多人共同进行开发的组织中，建议使用Organization 账户。

3. #### Webhooks & Services

   在这个页面中，用户可以添加Hook 让GitHub 仓库与其他服务集成。通过Add webhook 可以添加用户自己的webhook。通过Configureservices 则可以从GitHub 事先列出的可以集成的服务中进行选择。能与GitHub 集成的服务非常多，其中还包括邮件及IRC 等社交服务，建议各位不要错过这个设置。在如此大量的服务当中，相信各位能找到自己正在使用的工具。

4. #### Deploy Keys

   在这个页面中，用户可以添加用于部署的公开密钥，允许以只读方式访问仓库。设置公开密钥后，用户可以使用私有密钥通过ssh 协议clone 仓库。要注意的是，这里添加的公开密钥·私有密钥对无法再添加到其他仓库。使用Deploy Keys 功能时，需要给每个仓库赋予不同的密钥对。



## 尝试pull Requset（124）

##### Pull Request 是自己修改源代码后，请求对方仓库采纳该修改时采取的一种行为。

###### 在GitHub 上发送Pull Request 后，接收方的仓库会创建一个附带源代码的Issue，我们在这个Issue 中记录详细内容。这就是Pull Request。

###### 发送过去的Pull Request 是否被采纳，要由接收方仓库的管理者进行判断。一般只要代码没有问题，对方都会采纳。如果有问题，我们会收到评论。

###### 只要Pull Request 被顺利采纳，我们就会成为这个项目的Contributor（贡献者）

### 发送Pull Request 前的准备

#### ●Fork

把仓库fork到自己的github上来

#### ●clone

将在自己github上的该仓库clone 到本地

#### ●branch

##### -为何要在特性分支中进行作业

当前Git 的主流开发模式都会使用特性分支。在GitHub 上发送Pull Request 时，一般都是发送特性分支。这样一来，Pull Request 就拥有了更明确的特性（主题）。让对方了解自己修改代码的意图，有助于提高代码审查的效率。

##### -确认分支

查看一下clone 出的仓库的分支。

$ git branch -a

##### -创建特性分支

我们创建一个名为work 的分支，用来发送Pull Request。

$ git checkout -b work

##### -添加代码后提交修改

$ git commit -am "add my impression"

##### -创建远程分支

$ git push origin work



### 发送Pull Request

先切换到work分支 通过compare 比较与主分支区别

###### 确认想要发送的Pull Request 的内容差别无误后，请点击Create Pull Request。随后显示的表单用于填写请求对方采纳的评论。现在让我们在评论栏中简明扼要地描述本次进行Pull Request 的理由。



### 让Pull Request 更加有效的方法

1. #### 在开发过程中发送 Pull Request进行讨论

   我们虽然可以像本次示例一样等代码完成后再发送Pull Request，但在实际开发过程中，这样做很可能导致一个功能在完成后才收到设计或实现方面的指正，从而使代码需要大幅更改或重新实现。

   在GitHub 上，我们可以尽早创建Pull Request，从审查中获得反馈，让大家在设计与实现方面思路一致，借此逐渐提高代码质量。这个方法在团队开发大型项目时尤其有效。

   只要在想发起讨论时发送Pull Request即可，不必等代码最终完成。即便某个功能尚在开发之中，只要在PullRequest 中附带一段简单代码让大家有个大体印象，就能获取不少反馈。
   如果在Pull Request 中再加入直观易懂的Tasklist，就能很清楚反映出哪些功能已经实现，将来要做哪些工作。这不但能加快审查者的工作效率，还能作为自己的备忘录使用。

   从反馈中，我们不但能获得对自己所提议的新功能的支持和相关改善意见，有时还会被人指出自己没注意到的失误，或者准备编写的代码与其他成员重复等。这样一来，我们最终所完成的代码的质量一定会比原先高出许多。

   向发送过Pull Request 的分支添加提交时，该提交会自动添加至已发送的Pull Request 中。

   这一方法要求尽早发送Pull Request，越早效果越明显。另外还有一件事要记住，就是千万不要在Pull Request 中添加无关的修改。处理与主题无关的作业请另外创建分支，不然会让原本清晰的讨论变得一团糟。

2. #### 明确标出“正在开发过程中”

   为防止开发到一半的Pull Request 被误合并，一般都会在标题前加上“[WIP]”字样。（应该是commit的描述）WIP 是Work In Progress 的简写，表示仍在开发过程中。等所有功能都实现之后，再消去这个前缀。

   这种在代码库中边讨论边开发的开发流程，要比以往在完成之后审查再反馈的流程高效得多。这个方法已经被应用到众多的软件开发现场。通过这一方法，开发者可以体验GitHub 上独有的速度感。各位请务必加以实践。

3. #### 不进行 Fork 直接从分支发送 Pull Request（128）

   一般说来，在GitHub 上修改对方的代码时，需要先将仓库Fork 到本地，然后再修改代码，发送Pull Request。但是，如果用户对该仓库有编辑权限，则可以直接创建分支，从分支发送Pull Request。利用这一设计，团队开发时不妨为每一名成员赋予编辑权限，免去Fork 仓库的麻
   烦。这样，成员在有需要时就可以创建自己的分支，然后直接向master分支等发送Pull Request。

### 仓库的维护

Fork 或clone 来的仓库，一旦放置不管就会离最新的源代码越来越远。下面就让我们学习如何让仓库保持最新状态。

通常来说clone 来的仓库实际上与原仓库并没有任何关系。所以我们需要将原仓库设置为远程仓库，从该仓库获取（fetch）数据与本地仓库进行合并（merge），让本地仓库的源代码保持最新状态。

1. #### 仓库的 Fork 与 clone

   将octocat/Spoon-Knife 作为原仓库，在GitHub 上进行Fork（fork到自己仓库），然后（从自己仓库克隆）clone。

   $ git clone git@github.com:hirocastest/Spoon-Knife.git

   $ cd Spoon-Knife

2. #### 给原仓库设置名称

   我们给原仓库设置upstream 的名称，将其作为远程仓库。

   $ git remote add upstream git://github.com/octocat/Spoon-Knife.git

   今后，我们的这个仓库将以upstream 作为原仓库的标识符。这个环境下只需要设定一次。

3. #### 获取最新数据

   下面我们从远程仓库实际获取（fetch）最新源代码，与自己仓库的分支进行合并。要让仓库维持最新状态，只需要重复这一工作即可。

   $ git fetch upstream

   $ git merge upstream/master

   我们通过 git fetch 命令获取最新的数据，将upstream/master 分支与当前分支（master）合并。



## 接收Pull Request（133）

1. #### 采纳Pull Request 的方法

   在采纳Pull Request 的内容之前，请尽量将接收到的Pull Request 拿到本地开发环境中进行检
   查，确认是否能够正常运行以及代码是否安全。

   或者用将要在第8 章中介绍的Jenkins 等持续集成工具进行自动测试，保证新代码不破坏原有
   功能之后，再合并进仓库。

   ##### 在本地开发环境中检查接收到的Pull Request

2. #### 采纳Pull Request 前的准备

   除确认Pull Request 送来的代码是否运行正常外，各位还请在代码审查上也多花些心思。GitHub 上可以快速高效地审查代码。

   - ##### 代码审查  

    在GitHub 上可以对Pull Request 的具体的某行代码进行评论。发出评论之后相关人员会立刻接到Notifications，无论是PullRequest 的发送方还是接收方，都能迅速反馈。

   - ##### 查看图片的差别

     可以通过提交日志的Image View Mode Demo 来体验操作。

     ###### 2-up 可以同时显示一张旧图片和一张新图片，从而完成对比

     ###### Swipe 可以在分界线左右两侧分别显示旧图片和新图片。鼠标可以拖动分界线左右移动，帮助用户对比细节差异和细微的颜色差异。

     ###### Onion Skin 能够将新旧两张图片重叠放置，分阶段从旧图片慢慢过渡至新图片，用户可以自由调节过渡比例。通过这一功能，用户能够一步步确认新图片相对于旧图片的变化。

     ###### Difference 功能让笔者都感到吃惊，它能够直接抽出两张图片不一样的部分进行比较。

3. #### 在本地开发环境中反映 Pull Request的内容

   下面我们来讲解收到Pull Request 后在本地开发环境中进行实际检查的流程。在本示例中，Pull Request 接收方的用户名为ituring，发送方的用户名为“PR 发送者”。

   - ##### 将接收方的本地仓库更新至最新状态

     ###### 首先，将Pull Request 接收方的仓库clone 到本地开发环境中。如果已经clone 过，那么请进行fetch merge 等操作更新至最新状态。

     如果没克隆过

     $ git clone git@github.com:ituring/first-pr.git

     $ cd first-pr

   - ##### 获取发送方的远程仓库

     将Pull Request 发送方的仓库设置为本地仓库的远程仓库，获取发送方仓库的数据。

     $ git remote add PR发送者 git@github.com:PR发送者/first-pr.git
     $ git fetch PR发送者

     现在我们获取了Pull Request 发送方仓库以及分支的数据（PR 发送者/work）。

   - ##### 创建用于检查的分支

     前面我们只获取了远程仓库的数据，这些数据尚未反映在任何一个分支中。因此我们需要创建一个分支，用来模拟采纳Pull Request 后的状态。由于这是我们第一个Pull Request，分支名就叫pr1。

     $ git checkout -b pr1

   - ##### 合并

     下面要将已经fetch 完毕的“PR 发送者/work”的修改内容与pr1分支进行合并。

     $ git merge PR发送者/work

     pr1 分支中就加入了“PR 发送者/work”分支的修改内容。

     本示例中我们只修改了index.html 文件，所以检查一下index.html有没有显示错误即可。

     在实际开发中，各位需要通过自动测试等手段检查软件是否能正常运行。

   - ##### 删除分支

     检查结束后pr1 分支就没用了，可以直接删除。我们切换至pr1 之外的分支，运行下面的代码。
     $ git branch -D pr1

### 采纳Pull Request(139)

完成上述内容后，如果Pull Request 的内容没有问题，大可打开浏览器找出相应的Pull Request 页面，点击Merge pull request 按钮，随后Pull Request 的内容会自动合并至仓库。

不过，由于我们已经在本地构筑了相同的环境，只要通过CLI 进行合并操作再push 至GitHub，Pull Request 中就会反映出Pull Request 被采纳后的状态。这个状态对应到本示例中就是“PR 发送者/
work”分支合并到gh-pages 分支。

- #### 合并到主分支

  切换至gh-pages 分支。

  $ git checkout gh-pages

  然后合并“PR 发送者/work”分支的内容。

  （$ git remote add PR发送者 git@github.com:PR发送者/first-pr.git
  $ git fetch PR发送者

  如果没有进行这两步必须加上）

  $ git merge PR送信者/work

- #### push修改内容

  现在只剩下push 一步了，不过为保险起见，我们先查看本地 gh-pages 与GitHub 端仓库origin/gh-pages 代码的差别。

  $ git diff origin/gh-pages

  确认没有目的之外的差别后，进行push。

  $ git push

  用这种方法处理后，仓库的Pull Request 会自动从Open 状态变为Close 状态。

  以上便是安全接收Pull Request 的流程

  

