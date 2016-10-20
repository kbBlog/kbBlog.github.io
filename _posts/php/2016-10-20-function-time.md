---
layout: post
title: 获取指定年月周期的时间戳
category: PHP
tags: Function
description: 获取指定年月周期的时间戳
---

	/**
	* 计算每个月有几周及每周的起始时间和结束时间
	* @param srting $month 时间：2016-01
	* @return array
	*/
	
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

	/**
	 *
	 * 获取指定年月的开始和结束时间戳
	 *
	 * @param int $y    年份
	 * @param int $m    月份
	 * @return array(开始时间,结束时间)
	 */
	 
	function mFristAndLast($y = 0,$m = 0){
		$y = $y ? $y : date('Y');
		$m = $m ? $m : date('m');
		$d = date('t', strtotime($y.'-'.$m));
		return array("firsttime"=> strtotime($y.'-'.$m),"lasttime"=> mktime(23,59,59,$m,$d,$y));
	}

	/**
	 *
	 * 获取指定年月的开始和结束时间戳
	 *
	 * @param int $time 当月任意时间戳
	 * @return array(开始时间,结束时间)
	 */
	 
	function mFristAndLastTime($time = 0){
		$time = $time ? $time : time();
		$y = date('Y', $time);
		$m = date('m', $time);
		$d = date('t', $time);
		returnarray("firsttime"=>mktime(0,0,0,$m,1,$y),"lasttime"=>mktime(23,59,59,$m,$d,$y));
	}