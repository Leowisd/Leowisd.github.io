---
title: Syncing a fork repository using rebase
tags: [Git, Github]
mathjax: true
date: 2020-07-10 23:19:48
permalink:
categories: Git/Github
description: Using rebase to sync a fork repository
image:
---
<p class="description"></p>

<img src="/images/git-github.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

After forking one repository, if this repository updated, we need to keep up-to-date with this upstream repository.

## Configuring a remote for a fork

### Check current configured remote repository for your fork.
Using `git remove -v` to check remote repository status.
```
git remote -v
> origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
> origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
```

### Create a new remote *upstream* repository
```
git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
```

### Verify
Verify the new `upstream` repository you've specified for your fork.
```
git remote -v
> origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
> origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
> upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (fetch)
> upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (push)
```

## Syncing a fork

### Fetch
Fetch the branches and their respective commits from the upstream repository. Commits to `master` will be stored in a local branch, `upstream/master`.
```
git fetch upstream
> remote: Counting objects: 75, done.
> remote: Compressing objects: 100% (53/53), done.
> remote: Total 62 (delta 27), reused 44 (delta 9)
> Unpacking objects: 100% (62/62), done.
> From https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY
>  * [new branch]      master     -> upstream/master
```
### Switch to local master
```
git checkout master
> Switched to branch 'master'
```
### Rebase the changes from upstream/master into your local master

```
git rebase -i upstream/master
```

If no conflict, move to next step.

If any conflict, figure out conflict part, then add changes.
```
git add CONFLICT_FILE
```

Continue to rebase
```
git rebase --continue
```

### Push to origin master
Push your up-to-date local repo to origin master
```
git push origin master
```

## References

* [Configuring a remote for a fork](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/configuring-a-remote-for-a-fork)
* [Syncing a fork](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork)
* [git-rebase](https://git-scm.com/docs/git-rebase)
* [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
<hr />