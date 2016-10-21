---
layout: post
title: PHP 各种数据类型  系统函数输出比较
category: PHP
tags: Info
description: PHP 各种数据类型  系统函数输出比较
---

### 各种数据类型  函数输出比较

**用 PHP 函数对 $x 的比较**

```
表达式		  gettype()	  empty()	  is_null()	  isset()	boolean : if($x)

$x = "";   	  string	  TRUE        FALSE       TRUE      FALSE

$x = NULL	  NULL		  TRUE        TRUE        FALSE     FALSE

var $x;       NULL        TRUE        TRUE        FALSE     FALSE

$x 尚未定义   NULL        TRUE        TRUE        FALSE     FALSE

$x = array(); array       TRUE        FALSE       TRUE      FALSE

$x = true;    boolean     FALSE       FALSE       TRUE      TRUE

$x = false;   boolean     TRUE        FALSE       TRUE      FALSE

$x = "true";  string      FALSE       FALSE       TRUE      TRUE

$x = "false"; string      FALSE       FALSE       TRUE      TRUE

$x = 1;       integer     FALSE       FALSE       TRUE      TRUE

$x = "1";     string      FALSE       FALSE       TRUE      TRUE

$x = -1;      integer     FALSE       FALSE       TRUE      TRUE

$x = "-1";    string      FALSE       FALSE       TRUE      TRUE

$x = 0;       integer     TRUE        FALSE       TRUE      FALSE

$x = "0";     string      TRUE        FALSE       TRUE      FALSE

$x = 42;      integer     FALSE       FALSE       TRUE      TRUE

$x = "php";   string      FALSE       FALSE       TRUE      TRUE
```




