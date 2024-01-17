---
title: php伪协议
date: 2024-01-01 13:25:12
tags: learning
categories: web
---

php://input	可以访问请求的原始数据的只读流，在POST请求中访问POST的data部分，在enctype="multipart/form-data" 的时候php://input 是无效的。

php://output	只写的数据流，允许以 print 和 echo 一样的方式写入到输出缓冲区。

php://fd	(>=5.3.6)允许直接访问指定的文件描述符。例如 php://fd/3 引用了文件描述符 3。

php://memory php://temp	(>=5.1.0)一个类似文件包装器的数据流，允许读写临时数据。两者的唯一区别是 php://memory 总是把数据储存在内存中，而 php://temp 会在内存量达到预定义的限制后（默认是 2MB）存入临时文件中。临时文件位置的决定和 sys_get_temp_dir() 的方式一致。



php://filter	(>=5.0.0)一种元封装器，设计用于数据流打开时的筛选过滤应用。对于一体式（all-in-one）的文件函数非常有用，类似 readfile()、file() 和 file_get_contents()，在数据流内容读取之前没有机会应用其他过滤器。

php://filter参数详解

​			php://filter 参数	描述
​			resource=<要过滤的数据流>	必须项。它指定了你要筛选过滤的数据流。
​			read=<读链的过滤器>	可选项。可以设定一个或多个过滤器名称，以管道符（*\	*）分隔。
​			write=<写链的过滤器>	可选项。

构造payload如下

?file=php://filter/read=convert.base64-encode/resource=flag.php  

