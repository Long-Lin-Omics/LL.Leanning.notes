<br>
<br>


<div align="center">
  <img src="Picture1.png" alt="图片说明" width="500"/>
</div>

<br>
<br>

---

## **创建新的repo并推送到github.com** 

```
#in github.com
login and create an repository with a README
add your ssh public keys to get recognized by github.com

#in local computer
git clone git@github.com:username/repo_name.git # by ssh. https one is slower.
cd repo_name
#creat everything you want to include. you con use git to track versions during the process
git add .
git commit -m 'first time submmit to the repository'
git remote -v #should show the origin has been bound. 
git push -u origin main
```



```
#in local computer
cd the_folder_want_to_give
git init
git add .
git commit -m 'comments' 

#in github.com
add your ssh public keys to get recognized by github.com
create a repo

#back in local computer
#binding the remote repo
git remote add origin git@github.com:username/repo_name.git
git push -u origin main     # -u for first time push 
```
`git push -u origin master` if you see `master` from `git branch`


---

## **check where you are**

`git status` to know what is the process your workspace is in

`git diff $file` check the changes made to a file 

`git log`  check commit history for current process. optional: `--pretty=oneline`

`git reflog` check every activity you did.

`git diff HEAD -- $file`  查看工作区和版本库里面最新版本的区别. `--` 是当前分支？

## **配置Git**
```
git config --global user.name "Your name"
git config --global user.email "email@eexample.com"

#information stored at ~/.gitconfig
```



## **commit a deletion** 

在workspace删除文件， then `git rm <file>` and then `git commit -m "comment"`



## **return to a version**
```
git reset --hard `commit id`  ## 本质是移动HEAD指针(即master branch)

```
```
--hard	#回退到上个版本的已提交状态
--soft	#回退到上个版本的未提交状态
--mix	#回退到上个版本已添加但未提交的状态
```

special commit id
```
HEAD^		# last committed status
HEAD^^		# version before last version
HEAD~100	# 100th backwards version
first few digits are enough
```
### 撤销修改
`git restore --staged <file>...` to unstage. 把add到暂存区的修改撤销掉（unstage），重新放回工作区
`git restore <file>...` to discard changes in working directory 本质是让这个文件回到最近一次git commit或git add时的状态。是用版本库里的版本替换工作区的版本。 `--` 是当前分支？


## binding workspace to a remote repository
```
git remote -v  #check the information of remote repository

git remote rm origin # delete it if the remote is wrong
git remote add origin git@github.com:username/repo_name.git

or 

git remote set-url origin git@github.com:username/repo_name.git
```


