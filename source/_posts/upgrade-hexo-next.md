---
title: upgrade-hexo-next
tags: [Hexo, NexT]
mathjax: true
date: 2020-07-09 00:28:22
permalink:
categories: Hexo Blog
description: Upgrade the version of Hexo and NexT
image:
---
<p class="description"></p>

<img src="" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->


## Upgrade Hexo to v4.0+

To upgrade to Hexo v4, change the following line in package.json in your hexo blog folder.
```
-  "hexo": "^3.9.0",
+  "hexo": "^4.0.0",
```

Then excute the following command
```
npm update
```

Excute `hexo version` under your hexo blog directory to check the version upgrade

## Upgrade NexT to v7.x from v5.x

Following [offical instruction](https://github.com/theme-next/hexo-theme-next/blob/master/docs/UPDATE-FROM-5.1.X.md) to upgrade


<hr />