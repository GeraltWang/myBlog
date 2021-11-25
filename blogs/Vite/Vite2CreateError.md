---
title: 解决Windows下，Vue3.0的Vite2初始化项目失败的问题
date: 2021-11-12
sidebar: 'auto'
categories:
- Vite
tags:
- Vue
- Vite
publish: true
---
# 解决Windows下，Vue3.0的Vite2初始化项目失败的问题

> 在运行初始化命令后
>
> ```
> npm init vite@latest
> ```

> 报错信息如下
>
> ```
> Error: EPERM: operation not permitted, mkdir 'C:\Users\Gerald'
> 
> Install for [ 'create-vite-app@latest' ] failed with code 1
> ```

## 报错原因

截至2021年11月，Vite2 暂时不支持带空格的 windows 用户名(我的用户名是Gerald Wang)，所以才会出现以上报错，出现报错之后你会发现 C:\Users\ 目录下多了一个文件夹，文件夹名字是你用户名空格前的那个单词。

## 解决方案

使用管理员权限，打开命令行窗口，然后依次输入<b>(这里我就用我自己的用户名举例，你只需把名字替换即可)</b>

```
cmd /c mklink /J "C:\Users\GeraldWang" "C:\Users\Gerald Wang"
npm config set cache C:\Users\GeraldWang\AppData\Roaming\npm-cache
npm config set prefix C:\Users\GeraldWang\AppData\Roaming\npm
```

本质上就是创建一个没有空格的目录链接到现有的用户目录，然后再配置一下npm，指向链接目录。

最后再运行一次初始化项目命令即可

```
npm init vite@latest
```
