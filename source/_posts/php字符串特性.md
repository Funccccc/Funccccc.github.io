---
title: php查询字符串特性
date: 2024-01-08 19:44:22
tags:
categories:
---

PHP将查询字符串（在URL或正文中）转换为内部$_GET或关联数组$_POST。值得注意的是，查询字符串在解析的过程中会将某些字符删除或用下划线代替。
例如：
/?foo=bar变成Array([foo]=> “bar”)。
/? foo=bar变成Array([foo]=> “bar”)。 //?号后有一个空格
/?+foo=bar变成Array([foo]=> “bar”)。 //?号后有一个+号
