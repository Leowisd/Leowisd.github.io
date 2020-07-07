---
title: Modify Github Pages Rep for Hexo-Blog
tags: [Hexo, Github]
mathjax: true
date: 2020-07-06 23:08:06
permalink:
categories: Hexo Blog
description: Reconstruct the rep for hexo blog to edit on muilty devices and version control
image:
---
<p class="description"></p>

<img src="/images/github_pages_hexo.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

- [Push a new branch](#push-a-new-branch)
  - [Create a new branch](#create-a-new-branch)
  - [Clone rep and modify](#clone-rep-and-modify)
  - [Push to github](#push-to-github)
- [Setup on a new device](#setup-on-a-new-device)
  - [Setup git](#setup-git)
  - [Install hexo](#install-hexo)
  - [Clone rep and deploy](#clone-rep-and-deploy)
- [Tips](#tips)

## Push a new branch

### Create a new branch

Create a new branch like `hexo` in blog rep

Set the new branch as **default branch** in settings

### Clone rep and modify

Under any local folder, clone the rep

```
git clone https://github.com/<Your username>/<Your username>.github.io.git
```

Under this local rep folder, delete all items exclude `.git` folder

Copy all items from the original blog file exclude `.deploy_git` folder. Check if there is a file called `.gitignore` and its content looks like:
```
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
```
Meanwhile, focus on if there is any `.git` folder under your theme folders. Delete them all, or you will not have your themes config on your other devices.

### Push to github
```
git add .
git commit –m "add branch"
git push
```
Push done.

You could check if all items exclude item in `.gitignore` exist in your github rep.


## Setup on a new device

### Setup git

Install git
```
sudo apt-get install git
```

Setup global config
```
git config --global user.name "yourgithubname"
git config --global user.email "yourgithubemail"
```

### Install hexo
Install NodeJS
```
sudo apt-get install nodejs
```
Install npm, maybe already exist after installing nodejs
```
sudo apt-get install npm
```
Install hexo
```
sudo npm install hexo-cli -g
```

### Clone rep and deploy

Under any folder, clone the rep
```
git clone https://github.com/<Your username>/<Your username>.github.io.git
```

Under the local rep folder
```
npm install
npm install hexo-deployer-git --save
```

Generate and deploy
```
hexo g -d
```

Then you could edit and deploy your blog as usual on this new device

## Tips

1. Commit and push src rep to github after editing
2. Pull first on blog existed device before editing

<hr />