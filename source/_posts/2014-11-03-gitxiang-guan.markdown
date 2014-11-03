---
layout: post
title: "git相关"
date: 2014-11-03 20:08:45 +0800
comments: true
categories: 
---
  　　git版本管理，平时用的比较多，zsh提供了强大的插件，告别了小乌龟时代，都是使用命令进行操作，一般都是常用命令，偶尔也会存在使用不当影响开发，这个地方简单记录一下，出现了问题也可以到这来查查，后续遇到问题在往这里添加吧，写这篇文章的目的也是为了以后少出问题，尽量不出问题，即使出了问题也能很快解决，不要影响开发效率。  
  　　`git cherry-pick <commit id>`  
   　　用于把另一个本地分支的commit修改应用到当前分支。    
   　　在本地 master 分支上做了一个commit ( 38361a68138140827b31b72f8bbfd88b3705d77a ) ， 如何把它放到 本地 develop 分支上？   
   　　$git checkout develop  
   　　$git cherry-pick 38361a68138140827b31b72f8bbfd88b3705d77a  
   　　  
   `git stash`  
   1.使用`git stash`保存当前的工作现场，那么就可以切换到其他分支进行工作，或者在当前分支上完成其他紧急的工作，比如修订一个bug测试提交。  
2.如果一个使用了一个`git stash`，切换到一个分支，且在该分支上的工作未完成也需要保存它的工作现场。再使用`git stash`。那么stash 队列中就有了两个工作现场。  
3.可以使用`git stash list`,查看stash队列。  
4.如果在一个分支上想要恢复某一个工作现场怎么办：先用`git stash list`查看stash队列。确定要恢复哪个工作现场到当前分支。然后用`git stash pop stash@{num}`。num 就是你要恢复的工作现场的编号。  
5.如果想要清空stash队列则使用`git stash clear`。  
6.同时注意使用`git stash pop`命令是恢复stash队列中的stash@{0}即最上层的那个工作现场。而且使用pop命令恢复的工作现场，其对应的stash 在队列中删除。使用`git stash apply stash@{num}`方法除了不在stash队列删除外其他和`git stash pop` 完全一样。  　　
  
  **Git如何进行分支管理？**  
     1、创建分支  
     创建分支很简单：`git branch <分支名>`  
     2、切换分支  
     `git checkout <分支名>`  
     该语句和上一个语句可以和起来用一个语句表示：git checkout -b <分支名>  
     3、分支合并  
     比如，如果要将开发中的分支（develop），合并到稳定分支（master），  
     首先切换的master分支：`git checkout master`。  
     然后执行合并操作：`git merge develop`。  
     如果有冲突，会提示你，调用`git status`查看冲突文件。  
     解决冲突，然后调用`git add`或`git rm`将解决后的文件暂存。  
     所有冲突解决后，`git commit` 提交更改。  
     4、分支衍合  
     分支衍合和分支合并的差别在于，分支衍合不会保留合并的日志，不留痕迹，而 分支合并则会保留合并的日志。  
     要将开发中的分支（develop），衍合到稳定分支（master）。  
     首先切换的master分支：`git checkout master`。  
     然后执行衍和操作：`git rebase develop`。  
     如果有冲突，会提示你，调用`git status`查看冲突文件。  
     解决冲突，然后调用`git add`或`git rm`将解决后的文件暂存。  
     所有冲突解决后，`git rebase --continue` 提交更改。  
     5、删除分支  
     执行`git branch -d <分支名> ` 
     如果该分支没有合并到主分支会报错，可以用以下命令强制删除`git branch -D <分支名>  `  
     6、查看所有分支  
     执行`git branch -a`
       
   **git常用命令，在这里做个记录，没有什么实际意义**  
   1、全局配置  
   `git config -global user.name "yangnan"`  
   `git config -global user.email "xjxyyn@126.com"`  
   2、创建项目  
   `mkdir MyProject`   
   `git init`  初始化  
   `git add .` 添加文件  
   `git commit -m "初始化"` 提交到本地仓库  
   `git remote add origin git@github.com:lanmo/WebSocketDemo.git`  添加远程仓库  
   `git push origin master` 提交到远程仓库