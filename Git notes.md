## Git概念
Git是一种stupid content tacker， 但是它最多被用作revision control system
Git有着大量的命令，包括Porcelain（user-friendly） 和 plumbing（low-level work）两类

Git区别于SCM（software change and configuration management system）在于主要在于分布式
传统sgm需要每次commit前强行同步，防止丢失数据
每次checkout都是server repo数据的head的snapshot
single point failure
耗时：大多数的operation need communication between server and client

Git：
every clone is really full backup of all data
after initial clone，almost everything operation is local
scalable：自己可以拥有无数的branches，和别人没关系

这些因为本地端有version database(存的是key和value)
key：sha-1hash---只对content进行hash
value：binary files（commits，trees，blobs）
commits是acutal git commits（当前文件的snapshot）
trees：目录
blobs：content of datas

常见代码：
常见五步：
* git init projectName
* cd projectName
* coding~~~~
* git add .
* git commit -m "messgae for the commit"
git push origin master(此处也可也是其他任意branch)

git checkout -b feature_x
git checkout master
git branch -d feature_x
git push origin <branch>

git pull
git merge <branch>
git diff <source_branch> <target_branch>

git log
git log --author==Mike
git log --name-status
git checkout -- <filename>

git fetch origin
git reset --hard origin/master


更多代码：
git clone /path/to/repository

git add 做两件事
1.把内容做成一个blobs文件，并对内容进行hash，用它作为文件名
2.把这个文件放到stage area， update status
