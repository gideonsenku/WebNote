## Git笔记

- 文件的rename

  git mv readme readme.md 

- 历史记录

  git log

  git log --online（简洁）

  git log -n4 --online (行数)

  git log --oneline --all --n4 --graph(graph图形化)

  

- gitk(图形化工具)
- git commit -am：合并add 操作并提交

### 版本对象

git内部的tree和blob

一次commit仅有一个tree

一个文件夹也会有一个tree

blob代表某个文件，而文件内容相同时，git只会给一个blob，提高性能



- git cat-file -t [hashkey]：显示对象的类型。
- git cat-file -p [hashkey]：根据对象的类型，以优雅的方式显式对象内容。
- git cat-file -s [hashkey]：显示对象的大小。

#### 分离头指针

git checkout [hashkey]

切换至master时git会做垃圾回收，没有连接任何的branch

#### HEAD

标志commit的hashkey

可以使用HEAD代表目前的commit，HEAD^^或者HEAD~2代表HEAD的爷爷！

git diff HEAD HEAD^^

#### 分支

- git branch

- git checkout -b

#### 修改最新的commit

git commit --amend

