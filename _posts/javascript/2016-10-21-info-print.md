---
layout: post
title: Javascript 打印输出所有对象的属性和方法
category: Javascript
tags: Info
description: Javascript 打印输出所有对象的属性和方法
---

### JS 输出对象的所有属性及方法 无非是用到了for(var i in o) {i + ':' + o[i]} 语法

```js
<script>
function strobj(o){
    var temp = '';
    var t,a = [];
    for(var i in o) {
        try {
            if(typeof(o[i]) == "function")
            {
                t = '""'+i+'""' + ':' + 'function(){<em>[native code]</em>}' + '';
            }
            else if(Object.prototype.toString.call(o[i]) === '[object Array]') //数组
            {
                var p,b = [];
                for(var j in o[i]) {
                    if(isNaN(o[i][j])){ p = '"' + o[i][j] + '"'; } else { p = '' + o[i][j] + ''; }
                    b.push(p);
                }
                t = '""'+i+'""' + ':[' + b.join(',') + ']';
            }
            else
            {
                if(typeof(o[i]) == 'object') //对象,其他
                {
                    t = '""'+i+'""' + ':' + strobj(o[i]) + '';
                }
                else
                {
                    if(isNaN(o[i])){ t = '""'+i+'""' + ':"' + o[i] + '"'; } else { t = '""'+i+'""' + ':' + o[i] + ''; }
                }
            }
            a.push(t); t = '';
        }
        catch(e)
        {
            alert(e.message);
        }
    }
    temp = "{" + a.join(', ') + "}";
    return temp;
}

//var obj = {name:'alonely', age:24};
var obj = {name:'alonely', age:24, email:['test1@163.com','weed2@gmail.com'], family:{parents:['父亲','母亲']}, func:function(){} };
document.write(strobj(obj));
</script>
```