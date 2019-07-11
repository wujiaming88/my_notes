# Git常用命令

## 合并多个commit

### git rebase

#### 从 HEAD 版本开始往过去数3个版本

	git rebase -i HEAD~3
	
#### 指名要合并的版本之前的版本号


	git rebase -i 3a4226b 		#请注意3a4226b这个版本是不参与合并的，可以把它当做一个坐标
	
执行了rebase命令之后，会弹出一个窗口

	pick 3ca6ec3   '注释**********'
	
	pick 1b40566   '注释*********'
	
	pick 53f244a   '注释**********'

将pick改为squash或者s,之后保存并关闭文本编辑窗口即可

	pick 3ca6ec3   '注释**********'
	
	s 1b40566   '注释*********'
	
	s 53f244a   '注释**********'
	
## 克隆远程项目分支到本地对应分支

1. 克隆远程项目 `git clone`
2. 查看远程所有分支 `git branch -r`
3. 建立本地分支 `git checkout –b 本地分支名 远程分支名`

## 使用远程仓库强制覆盖本地

	git reset --hard origin/master 

## 查看某文件的修改历史
### git log

#### git log -- filename 
> 查看文件相关的commit记录

#### git log -p filename
> 查看该文件每次提交的diff

#### git show commit-id filename
> 查看某次提交中的某个文件变化

#### git show commit-id
> 根据commit-id查看某个提交 

#### git log 的常用选项


|选项|	说明|
|:------|:------|
|-p|按补丁格式显示每个更新之间的差异|
|--stat|显示每次更新的文件修改统计信息|
|--shortstat|只显示 --stat 中最后的行数修改添加移除统计|
|--name-only|仅在提交信息后显示已修改的文件清单|
|--name-status|显示新增、修改、删除的文件清单|
|--abbrev-commit|仅显示 SHA-1 的前几个字符，而非所有的 40 个字符|
|--relative-date|使用较短的相对时间显示（比如，“2 weeks ago”)|
|--graph|显示 ASCII 图形表示的分支合并历史|
|--pretty|使用其他格式显示历史提交信息。可用的选项包括 oneline，short，full，fuller 和 format（后跟指定格式）|
|-(n)|仅显示最近的 n 条提交|
|--since, --after|仅显示指定时间之后的提交|
|--until, --before|仅显示指定时间之前的提交|
|--author|仅显示指定作者相关的提交|
|--committer|仅显示指定提交者相关的提交|
|--grep|仅显示含指定关键字的提交|
|-S|仅显示添加或移除了某个关键字的提交|


	
	