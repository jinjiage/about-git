# about-git
## git介绍.
**概述.**
![git](doc/git.png)

- git是一种围绕文件系统（用hash代表文件系统及提交）及其构建的树形结构，来跟踪和管理变更的版本控制系统；
- git中包含工作区、暂存区、版本区、本地分支、远程分支、远程库等实体，同时提供了丰富的命令来操作这些实体；
- git中保存着每次提交记录，每个提交由提交hash来表示，所有的提交hash构成一棵树；
- git中每个提交hash下面挂接着文件系统，文件系统包含目录树hash及文件hash，每个hash唯一标识目录树及文件；

---

**Git vs Svn**
![](doc/svn_git1.png)
![](doc/svn_git_server1.png)
![](doc/svn_git2.png)
![](doc/svn_git_server2.png)
*参考文章：[SVN与Git比较的优缺点差异](https://www.cnblogs.com/Sungeek/p/9152223.html)*

## git命令讲解.
![git command](doc/有关Git.png)
### git help -a
![git help](doc/git_version.PNG)

### git cat-file [option] hash
	git中比较底层的命令，用于查看hash对象的类型、内容等信息，通过这个命令，我们可以查看提交hash、版本区文件系统及文件的挂接联系，进一步了解git的内部原理
	
	- git cat-file -t hash #显示hash对象类型：提交hash为commit、文件hash为blob、目录树hash为tree
	
	- git cat-file -p hash #显示hash对象的内容
	
![git](doc/git-cat-file.PNG) 

### git log
	
	显示当前分支按时间排序的提交函数	

### git show

### git merge

### git rebase

### git ls-tree [option] 提交hash

	显示版本区的文件系统，通过git cat-file命令讲解，我们已经可以获知版本区的文件系统，但每次都要通过查看提交hash的内容来间接获取会比较麻烦，而git ls-tree就是为了简化此操作
	
	- git ls-tree -r #递归显示文件系统

### git ls-files

	显示暂存区的文件系统

##  git高级技巧
### 拆分仓库
	cd about  #例如我的一个仓库about
	git subtree split -P 有关编译原理 -b about-compiler #我要把‘有关编译原理’目录独立出来，在about仓库中新建一个分支为about-compiler存放与‘有关编译原理’有关的信息
	cd ..
	mkdir about-compiler
	cd about-compiler
	git init
	git pull ../about about-compiler #从about本地仓库中拉取之前的about-compiler分支，即与‘有关编译原理’有关的所有信息
	git remote add origin https://github.com/yejinlei/about-compiler.git   #事先在github上创建独立项目
	git push origin -u master

	#慎重选择，删除about中与‘有关编译原理’有关的信息
	git filter-branch -f --index-filter "git rm -r -f -q --cached --ignore-unmatch 有关编译原理" --prune-empty HEAD

## 图解git.
![git command](doc/git_workflow1.png)

## git工作流.
### git flow
![git flow](doc/git_flow.png)
- Vincent Driessen提出的一个分支管理的策略,应用这个规范可以使得版本库的演进保持简洁，主干清晰，各个分支有不同的职责，在很大程度上减少冲突的产生 *
- git flow使用原则
  - master分支是线上稳定分支，release通常用作测试分支，develop分支是开发应用的主分支
  - 所有的功能开发都在feature分支进行，然后合并到develop分支
  - release分支发布后出现问题，直接在release分支修改，避免develop分支代码污染

## git资源
1. **Git Doc**，[en](https://git-scm.com/docs)
2. **Pro Git**，[zh](https://git-scm.com/book/zh/v2)、[en](https://git-scm.com/book/en/v2)
3. **沉浸式学习Git**，[zh](http://higrid.net/hi/books/gitimmersion)
4. **Git Magic魔法**，[zh](http://higrid.net/hi/books/gitmagic)
5. **Git权威指南**
6. **Git团队协作**
7. **Git Community Book**，[zh](http://gitbook.liuhui998.com/)