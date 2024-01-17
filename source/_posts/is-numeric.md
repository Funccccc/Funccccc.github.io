---
title: is_numeric()
date: 2024-01-09 14:12:57
tags:
categories:
---

is_numeric

    一、基本使用
    二、16进制绕过
    三、科学计数法绕过
    四、字符串
    五、is_int()和is_numeric()的区别
    六、type_digit()和is_numeric()的区别

is_numeric() 可以检测「变量」是否为「数字」或数字字符串。

语法

bool is_numeric( $var )

    1

参数

    $var ：需要检测的变量

返回值

布尔类型

    返回 true ：整形、浮点型、整形字符串、浮点型字符串
    其他 false

一、基本使用

「整形」、「浮点型」以及他们的字符串形式，都返回 true 。

实例：

var_dump(is_numeric(1));
var_dump(is_numeric(1.1));
var_dump(is_numeric('1'));
var_dump(is_numeric('1.1'));

    1
    2
    3
    4

输出：

bool(true)
bool(true)
bool(true)
bool(true)

    1
    2
    3
    4


二、16进制绕过

is_numeric() 会对「16进制」（0x开头）返回 true 。数值型和字符型都可以。

实例：

var_dump(is_numeric(0x7e));
var_dump(is_numeric('0x7e'));

    1
    2

输出：

bool(true)
bool(true)

    1
    2

绕过思路：把 '1 or 1' 这类payload转成16进制，再传给 is_numeric() ，实现绕过。

三、科学计数法绕过

is_numeric() 会对「科学计数法」（0e开头）返回 true 。数值型和字符型都可以。

并且，0e开头的值，强制转换成int类型后，都是1。

实例：

var_dump(is_numeric(0e123));
var_dump(is_numeric('0e123'));
echo (int)is_numeric(0e123).PHP_EOL;
echo (int)is_numeric(0e9999).PHP_EOL;
echo (int)is_numeric('0e123');

    1
    2
    3
    4
    5

输出：

bool(true)
bool(true)
1
1
1

    1
    2
    3
    4
    5

绕过思路：遇到 (int)is_numeric($_GET['a']) 这类情况时，可以使用传入 0exxx 格式的参数来绕过。

四、字符串

「数字」和「字母」组合的字符串，无论是否以数字开头，都返回 false。

实例：

var_dump(is_numeric('1a'));
var_dump(is_numeric('a1'));

    1
    2

输出：

bool(false)
bool(false)

    1
    2


五、is_int()和is_numeric()的区别

is_int() 和 is_numeric() 都可以 “判断变量是否为数字”。

但 is_int() 必须是「整形」才返回 true ，其他类型都返回 false；
而 is_numeric() 对「浮点型」 和「数值型字符串」也返回 true 。

实例：

var_dump(is_numeric(1.1));
var_dump(is_int(1.1));
var_dump(is_numeric('1'));
var_dump(is_int('1'));

    1
    2
    3
    4

输出：

bool(true)
bool(false)
bool(true)
bool(false)

    1
    2
    3
    4


六、type_digit()和is_numeric()的区别

type_digit() 和 is_numeric() 都可以 “判断变量是否为数字”。

但 type_digit() 只有在字符串中全是「数字」才会返回 true ，整型、浮点型、甚至包含正负符号的值都返回 false。
而 is_numeric() 对整型、浮点型、以及包含正负符号的值都返回 true 。

实例：

var_dump(is_numeric('1'));
var_dump(ctype_digit('1'));

var_dump(is_numeric(1));
var_dump(ctype_digit(1));

var_dump(is_numeric('1.1'));
var_dump(ctype_digit('1.1'));

var_dump(is_numeric('-1'));
var_dump(ctype_digit('-1'));

var_dump(is_numeric('+1'));
var_dump(ctype_digit('+1'));

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14

输出：

bool(true)
bool(true)
bool(true)
bool(false)
bool(true)
bool(false)
bool(true)
bool(false)
bool(true)
bool(false)

