---
layout: post
title: PHP 关于时间戳函数大全
category: PHP
tags: Function
description: PHP 关于时间戳函数大全
---

	
	/**
	* 计算每个月有几周及每周的起始时间和结束时间
	* @param srting $month 时间：2016-01
	* @return array
	*/

```php	
	function get_weekinfo($month){
		$weekinfo = array();
		$end_date = date('d',strtotime($month.' +1 month -1 day'));
		for ($i = 1; $i < $end_date ; $i = $i + 7) {
			$w = date('N',strtotime($month.'-'.$i));

			$weekinfo[] = array( //周期
				strtotime($month.'-'.$i.' -'.($w - 1).' days'), //开始时间
				strtotime($month.'-'.$i.' +'.(7 - $w).' days') //结束时间
			);
		}
		return $weekinfo;
	}
```

	/**
	 *
	 * 获取指定年月的开始和结束时间戳
	 *
	 * @param int $y    年份
	 * @param int $m    月份
	 * @return array(开始时间,结束时间)
	 */
	 
```php	 
	function mFristAndLast($y = 0,$m = 0){
		$y = $y ? $y : date('Y');
		$m = $m ? $m : date('m');
		$d = date('t', strtotime($y.'-'.$m));
		return array("firsttime"=> strtotime($y.'-'.$m),"lasttime"=> mktime(23,59,59,$m,$d,$y));
	}
```

	/**
	 *
	 * 获取指定年月的开始和结束时间戳
	 *
	 * @param int $time 当月任意时间戳
	 * @return array(开始时间,结束时间)
	 */

```php	 
	function mFristAndLastTime($time = 0){
		$time = $time ? $time : time();
		$y = date('Y', $time);
		$m = date('m', $time);
		$d = date('t', $time);
		returnarray("firsttime"=>mktime(0,0,0,$m,1,$y),"lasttime"=>mktime(23,59,59,$m,$d,$y));
	}
```

	/**
	 * 时间转化
	 * @param int $time 时间
	 * @return string
	 */

```php	 
	function tranTime($time) {
		$ytime = date("Y-m-d H:i", $time);
		$mtime = date("m-d H:i", $time);
		$htime = date("H:i", $time);
		$time = time() - $time;
		if ($time < 60) {
			$str = '刚刚';
		} elseif ($time < 60 * 60) {
			$min = floor($time / 60);
			$str = $min . '分钟前';
		} elseif ($time < 60 * 60 * 24) {
			$h = floor($time / (60 * 60));
			$str = $h . '小时前 ' . $htime;
		} elseif ($time < 60 * 60 * 24 * 3) {
			$d = floor($time / (60 * 60 * 24));
			if ($d == 1)
				$str = '昨天 ' . $mtime;
			else
				$str = '前天 ' . $mtime;
		}elseif($time < 60 * 60 * 24 * 30 * 12){
			$str = $mtime;
		} else {
			$str = $ytime;
		}
		return $str;
	}
```

```php
<?php

	echo '今天是'. date('Y年m月d日 '). ' 星期' . cnWeek(date('Y-M-d'));
	
	/*
	*	时间戳显示星期
	*/
	function cnWeek($date)
	{
	  $arr = array('天','一','二','三','四','五','六');
	  return $arr[date('w',strtotime($date))];
	}

	?>
```
```php
	<?php $arr=array("天","一","二","三","四","五","六"); echo date("Y年m月d日").'&nbsp;&nbsp;'."星期".$arr[date("w",strtotime(date("Y-m-d")))]; ?>
```