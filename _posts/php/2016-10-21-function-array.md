---
layout: post
title: PHP 关于二维数组的一些操作函数
category: PHP
tags: php
description: PHP 关于二维数组的一些操作函数
---

```php
	/**
	 * 二维数组按指定的键值排序
	 * @param array $array 指定二维数组
	 * @param string $keys 指定排序键值
	 * @param string $type 排序
	 */
	function array_sort($array, $keys, $type = 'asc'){
		if(!isset($array) || !is_array($array) || empty($array)){
			return '';
		}
		if(!isset($keys) || trim($keys)==''){
			return '';
		}
		if(!isset($type) || $type=='' || !in_array(strtolower($type),array('asc','desc'))){
			return '';
		}
		$keysvalue=array();
		foreach($array as $key=>$val){
			$val[$keys] = str_replace('-','',$val[$keys]);
			$val[$keys] = str_replace(' ','',$val[$keys]);
			$val[$keys] = str_replace(':','',$val[$keys]);
			$keysvalue[] =$val[$keys];
		}
		asort($keysvalue); //key值排序
		reset($keysvalue); //指针重新指向数组第一个
		foreach($keysvalue as $key=>$vals) {
			$keysort[] = $key;
		}
		$keysvalue = array();
		$count=count($keysort);
		if(strtolower($type) != 'asc'){
			for($i=$count-1; $i>=0; $i--) {
				$keysvalue[] = $array[$keysort[$i]];
			}
		}else{
			for($i=0; $i<$count; $i++){
			$keysvalue[] = $array[$keysort[$i]];
			}
		}
		return $keysvalue;
	}
```

```php
	/**
	 * 对多位数组进行排序
	 * @param $multi_array 数组
	 * @param $sort_key需要传入的键名
	 * @param $sort排序类型
	 */
	function multi_array_sort($multi_array, $sort_key, $sort = SORT_DESC) {
		if (is_array($multi_array)) {
			foreach ($multi_array as $row_array) {
				if (is_array($row_array)) {
				$key_array[] = $row_array[$sort_key];
				} else {
				return FALSE;
				}
			}
		} else {
			return FALSE;
		}
		array_multisort($key_array, $sort, $multi_array);
		return $multi_array;
	}

```

```php	
	/**
	 * 二维数组剔除重复值
	 * @param array $array2D 二维数组
	 * @param bool $stkeep 判断是否保留一级数组键
	 * @param bool $ndformat 判断是否保留二级数组键
	 * @return array
	 */
	function unique_arr($array2D, $stkeep = false, $ndformat = true){

		// 判断是否保留一级数组键 (一级数组键可以为非数字)
		if($stkeep) $stArr = array_keys($array2D);
		// 判断是否保留二级数组键 (所有二级数组键必须相同)
		if($ndformat) $ndArr = array_keys(end($array2D));
		//降维,也可以用implode,将一维数组转换为用逗号连接的字符串
		foreach ($array2D as $v){
			$v = join(",",$v);
			$temp[] = $v;
		}
		//去掉重复的字符串,也就是重复的一维数组
		$temp = array_unique($temp);
		//再将拆开的数组重新组装
		foreach ($temp as $k => $v)
		{
			if($stkeep) $k = $stArr[$k];
			if($ndformat)
			{
				$tempArr = explode(",",$v);
				foreach($tempArr as $ndkey => $ndval) $output[$k][$ndArr[$ndkey]] = $ndval;
			}
			else $output[$k] = explode(",",$v);
		}
		return $output;
	}
```

```php
	/**
	 * 对查询结果集进行排序
	 * @param array $list 查询结果
	 * @param string $field 排序的字段名
	 * @param string $sortby 排序类型 （asc正向排序 desc逆向排序 nat自然排序）
	 * @return array
	 */
	function list_sort_by($list, $field, $sortby = 'asc')
	{
		if (is_array($list))
		{
			$refer = $resultSet = array();
			foreach ($list as $i => $data)
			{
				$refer[$i] = &$data[$field];
			}
			switch ($sortby)
			{
				case 'asc': // 正向排序
					asort($refer);
					break;
				case 'desc': // 逆向排序
					arsort($refer);
					break;
				case 'nat': // 自然排序
					natcasesort($refer);
					break;
			}
			foreach ($refer as $key => $val)
			{
				$resultSet[] = &$list[$key];
			}
			return $resultSet;
		}
		return false;
	}
```