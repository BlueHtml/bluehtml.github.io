---
layout: post
title:  "使用Github Actions来完成有道云笔记每日签到"
categories: 技术
tags: github github-action
excerpt: 本文主要介绍下如何使用Github Actions来完成有道云笔记每日签到。
---

* content
{:toc}

## 前言

项目地址：<https://github.com/BlueHtml/Note163Checkin>

该项目使用Github Actions来完成有道云笔记每日签到，每天定时运行，无需服务器。

注意：**并非全自动，需要使用Fiddler或其他抓包工具获取到Cookie**

## 一、Fork 仓库

打开<https://github.com/BlueHtml/Note163Checkin>，**点击右上角的`Fork`**
![Fork](https://img.guoqianfan.com/note/2020/08/fork.png)

## 二、添加 Secret

**`Settings`->`Secrets`->`New secret`，添加以下Secret：**
- `Conf`：其值如下：
    ```json
    {
    	"Users": [{
    			"Name": "CC", //自定义名字，选填
    			"Cookie": "YNOTE_LOGIN=true; YNOTE_SESS=v2|abc" //有道云笔记客户端抓包的cookie
    		}, {
    			"Name": "MM",
    			"Cookie": "YNOTE_LOGIN=true; YNOTE_SESS=v2|123"
    		}
    	],
    	"ScKey": "", //server酱sckey，不填不开启
    	"ScType": "Failed" //通知类型. Always:始终通知; Failed:失败时通知; 不填/其他:不通知;
    }
    ```

**步骤图示如下：**
![添加Secret](https://img.guoqianfan.com/note/2020/08/添加secret.png)

## 三、启用 Action

**点击`Actions`，再点击`I understand my workflows, go ahead and enable them`**
![启用Action](https://img.guoqianfan.com/note/2020/08/启用action.png)

**注意**：Fork 的仓库上的 GitHub Actions 的**定时任务不会自动执行**，必须要手动触发一次后才能正常工作。

所以 Fork 之后，点击自己仓库右上角的`Star`，`Star`你的仓库，这是为了触发 Github Action 第一次执行，之后就会自动执行定时任务。
![Star](https://img.guoqianfan.com/note/2020/08/star.png)

## 四、查看运行结果

**`Actions`->`Checkin`->`build`**，能看到下图，表示运行成功（注意：由于 .NET Core会输出默认日志，请**滚动到最下面查看实际运行结果**）
![查看Action运行记录](https://img.guoqianfan.com/note/2020/08/查看action运行记录.png)

## 注意事项

并非全自动，需要使用Fiddler或其他抓包工具获取到Cookie。

每天运行一次，在上午9:00-9:45之间。

也可以点击右上角的`Star`手动运行。
![Star](https://img.guoqianfan.com/note/2020/08/star.png)

## 参考

参考了以下项目：
- [ydao](https://github.com/yygtboy/ydao/)
- [node-script](https://github.com/SunSeekerX/node-script)
- [youdaoyun](https://github.com/hezhizheng/youdaoyun)
