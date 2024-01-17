---
title: Http请求头
date: 2024-01-01 17:05:58
tags:
categories: ctf
---

GET /Secret.php HTTP/1.1



Referer告诉服务器该网页是从哪个页面链接过来的

Referer:https://Sycsecret.buuoj.cn



User-Agent：Mozilla/5.0 (平台) 引擎版本 浏览器版本号

User-Agent::" Syclover" browse



X-Forwarded-For（XFF）:获得HTTP请求端的真实IP

X-Forwarded-For :127.0.0.1
