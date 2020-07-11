---
title: Git ignore already managed files
tags: [Git, Github]
mathjax: true
date: 2020-07-10 12:31:20
permalink:
categories: Git/Github
description: Ignore already managed files changes with Git 
image:
---
<p class="description"></p>

<img src="/images/git-github.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

When using git, we would meet a special situation. There is a necessary config file which must be exist, but each developer needs to modify it locally. In this case, this file needs to be modified times by times, which causes conflicts possibly. If wanna avoid conflicts, every developer needs to pay attention to avoid submitting this file.

Generally, we would use **.gitignore** to ignore this file. However, if this file has already pushed, and is necessary to whole project, it should be saved in git. .gitignore cannot deal with this tracked file.

In this situation, should we use two ways
* `git update-index --skip-worktree FILE_NAME` 
* `git update-index --assume-unchanged FILE_NAME`

Those commands can make git ignores some files when scanning file list. In this case, git will never care about those files even if they have changes.

## git update-index --skip-worktree

`--skip-worktree` is the flag which means the files should change locally.

That is, Use the command when you want to modify files managed by Git locally (or updated automatically) but you do not want Git to manage that change.

### Exclude from tracking
```
git update-index --skip-worktree FILE_NAME
```
### How to confirm
```
git ls-files -v | grep ^S
```
### Restore tracking
```
git update-index --no-skip-worktree FILE_NAME
```
## git update-index --assume-unchanged

`--assume-unchanged` is the flag which means the files should not change locally.

In other words, it is used when ignore files that you do not need to change locally (or should not change).

`--assume-unchanged` is used when you want to speed up Git's behavior by ignoring unnecessary files.

Also, since it is an idea to ignore local changes, git reset - hard command will delete local changes.

### Exclude from tracking
```
git update-index --assume-unchanged FILE_NAME
```
### How to confirm
```
git ls-files -v | grep ^h
```
### Restore tracking
```
git update-index --no-assume-unchanged FILE_NAME
```
## Relationship with remote repo

`--assume-unchanged` will closes tracking between this file and remote repo. It assumes that this file will never change, so pull will always get local file.

`--skip-worktree` will keep the tracking between this file and remote repo. It just tell git not to manage local changes, so pull will get latest changes and show conflicts. But because of not tracking local changes, execute `--no-skip-worktree` first then merge latest changes.

## Reference
* [How to ignore files already managed with Git locally](https://dev.to/nishina555/how-to-ignore-files-already-managed-with-git-locally-19oo)
* [Git update-index document](https://www.google.com/search?q=git+update-index&oq=git+update-index&aqs=chrome..69i57j69i59j69i64j69i60j69i61j69i60&sourceid=chrome&ie=UTF-8)

<hr />