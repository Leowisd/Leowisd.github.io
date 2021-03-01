---
title: React Router with MobX Doesn't Re-render Using History.push()
tags: [React, React-Router, MobX]
mathjax: true
date: 2021-02-28 21:15:13
permalink:
categories: Issues
description: Records of issues and solutions
image:
---
<p class="description"></p>

<img src="/images/react-mobx.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Issue Description

Issue happened with react-router-dom and MobX. Tryed to use `history.push()` for navigating after an action conducted. The problem is only updating the urls but components are not re-rendering.

## Solution

Used `<BrowserRouter>` as router component in application. Followed by [offical document](https://reactrouter.com/web/api/Router), need to replace it with `<Router history={history}>` because MobX was used to manage state, where `history` is return by `syncHistoryWithStore()` from `mobx-react-router`.

<hr />