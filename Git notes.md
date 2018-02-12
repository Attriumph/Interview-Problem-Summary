## Git概念
Git是一种stupid content tacker， 它只是最多被用作revision control system
Git有着大量的命令，包括Porcelain（user-friendly） 和 plumbing（low-level work）两大类

## Git和SCM的区别
Git区别于SCM（software change and configuration management system）在于主要在于：git的分布式
### 传统的SGM：
* 传统scm需要每次commit前强行同步，防止丢失数据
* 每次checkout都是server repo数据的head的snapshot
* 存在single point failure
* 耗时，因为大多数的operation need communication between server and client

### Git：
* every clone is really full backup of all data
* after initial clone，almost everything operation is local
* scalable：自己可以拥有无数的branches，和别人没关系
* local has version database(存的是key和value)

      key：sha-1hash---只对content进行hash
      value：binary files， comprised of commits，trees and blobs
      1)commits是acutal git commits（当前文件的snapshot）
      2)trees：directory
      3)blobs：content of datas
 
## 常用代码：

1.常见五步：
* git init projectName
* cd projectName
* coding~~~~
* git add .

      git add 做两件事
      1)把内容做成一个blobs文件，并对内容进行hash，用它作为文件名
      2)把这个文件放到stage area(index)， update status

* git commit -m "messgae for the commit"

2.more common commands
      
      * checkout a respository:create a working copy of a respo
      git clone /path/to/repository
      git clone  username@host:/path/to/repository
      
      * push changes:send changes in local HEAD to remote respo
      git push origin master(此处master也可也是其他任意branch)
      git remote add origin <server>(when we have not clone an existing respo annd want to connect our respo to the remote)
      
      * branching 
      git checkout -b feature_x  （b--branch）
      git checkout master
      git branch -d feature_x （d--delete）
      git push origin <branch> (push local branch to server)
      
      * update and merge
      git pull (update our local branch to the newest commit)
      git merge <branch> (to merge another branch into the acctive branch)
      git diff <source_branch> <target_branch>
      
      * tagging
      git tag 1.0.0 id (get from log)
      
      *Log:study repository history
      git log
      git log --author==Mike
      git log --name-status
      git log --help
      
      * replace local changes
      git checkout -- <filename> 
      //replaces the changes in your working tree with the last content in HEAD. Changes already added to the index, as well as new   
        files, will be kept.
      
      git fetch origin
      git reset --hard origin/master
      //drop all our local changes and commits, fetch the latest history from the server and point our local master branch 

    


