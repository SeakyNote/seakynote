## git修改message

激活分支 commit amend last commit

## not valid: is this a git repository?

git clone如果需要输密码，就直接输url的形式

## git切换账号

凭据管理器删掉凭据

## git断点续传方法

https://blog.csdn.net/lgfx21/article/details/119144866

## git拉取linux问题

error: invalid path 'drivers/gpu/drm/nouveau/nvkm/subdev/i2c/aux.c'

https://kingkong.blog.csdn.net/article/details/114475070?spm=1001.2101.3001.6650.7&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-7-114475070-blog-116007384.pc_relevant_recovery_v2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-7-114475070-blog-116007384.pc_relevant_recovery_v2&utm_relevant_index=8

## 基于git的管理应用程序基线包和版本

https://www.cnblogs.com/charles8866/p/8966780.html

## TBD

https://paulhammant.com/2013/04/05/what-is-trunk-based-development/

## git工作流

https://zhuanlan.zhihu.com/p/536195762

## 四种常见的Git工作流

https://zhuanlan.zhihu.com/p/434078984

## git merge --ff/--no-ff/--ff-only 三种选项参数的区别

https://www.cnblogs.com/xiao2shiqi/p/14715119.html

## git 避免windows下换行符与Unix系列的区别

https://blog.csdn.net/fareast_mzh/article/details/99686470

## pull request和merge request的区别

https://blog.csdn.net/qq_31660535/article/details/107150627

## vscode fetch清理远端跟踪分支勾选项

Git-graph Fetch And Prune

## Git rebase is not working by conflicting in current branchGit rebase 因在当前分支中发生冲突而无法正常工作

删除merge-rebase文件

## vscode gitlens失效，怎么办This GitLens pre-release version has expired

https://blog.csdn.net/weixin_42458930/article/details/132619944

gitless

## git 上传一个空文件的解决方案，可使用命令行创建.gitkeep文件

https://dandelioncloud.cn/article/details/1525494660097392641

## gitlab加人到组和项目权限

https://gitlab.com/gitlab-org/gitlab/-/issues/23389

## Git配置中的CRLF、LF、CR

https://zhuanlan.zhihu.com/p/87199035

https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration

git config --global core.autocrlf

## git submodule无法加载

到.gitmodules文件下自行替换

## rebase问题

如果rebase的分支有多条commit的话，若rebase时提示冲突，即便解决了冲突，rebase操作生成的新节点也可能缺失部分代码，无法rebase完全。

## github token认证

https://www.cnblogs.com/yorkiiz/p/15154904.html

## git commit变成change

往回reset current branch to this commit

## 展示所有本地节点

repository Settings，第三个勾

## git-lfs问题

检出节点时直接报external filter git-lfs filter-process failed
```
git lfs install --skip-smudge
切换节点
git lfs pull
git lfs install --force
```

## 合并时报fatal: You have not concluded your merge(MERGE_HEAD exists)
```
$:git merge --abort
$:git reset --merge
$:git pull
```

## 代码审查考虑用sourcetree

## git仓库文件大小写改名问题
- windows平台下仅变更大小写不会触发git uncommit
- 如果要仅变更大小写需要先删除后重新添加

## git lfs pull拉取失败
- 可能有多个远端分支，其中某些没有对应文件
- 需要指定remote
	- 如git lfs pull origin

## Gitee 自已提交的代码提交人头像为他人、码云上独自开发的项目显示为 2 个开发者
https://blog.csdn.net/jiangyu1013/article/details/97630479
