---
title: JS日期转换,jq拼接,arr数组操作
date: 2015-09-18 17:53:14
categories: 
	- JS
tags: 
	- JS
    
---

### jq不识别拼接的对象id的解决方案
```
<div id="a1"></div>
<div id="a2"></div>
<div id="a3"></div> 
//循环给 a1 a2 a3 赋值，
for(var i=1;i<=3;i++)
{
    $("#a"+i).html("我是"+i); // 红色部分不识别。
}
```
### 解决方案如下：
```
//用ｅｖａｌ()函数，
//此处我们可以这么写
$(ｅｖａｌ("a"+i)).html("我是"+i);
//jq就识别了，知道你要找的是id等//于a1的对象了。
//切忌，不要加 # 号 。
//加的话作用就消失了，还是会返回null值的。
```

### js日期转换
```
001：
 function getddd(utcDate, format) {
            var date = new Date(parseInt(utcDate.replace("/Date(", "").replace(")/", ""), 10));
            var year = date.getFullYear();
            var month = date.getMonth() + 1;// < 10 ? "0" + (date.getMonth() + 1) : date.getMonth() + 1; 
            var currentDate = date.getDate();// < 10 ? "0" + date.getDate() : date.getDate();
            var hour = date.getHours();
            var minute = date.getMinutes();
            var second = date.getSeconds();
            var datastr = year + "-" + month + "-" + currentDate + " " + hour + ":" + minute + ":" + second;
            return formatDateTime(datastr, format);
        }
        function formatDateTime(str, format) {
            var date = new Date(str.split("-").join("/"));
            if (date.toString() == "NaN" || date.toString() == "Invalid Date") { return ""; }
            var o = {
                "M+": date.getMonth() + 1,
                "d+": date.getDate(),
                "h+": date.getHours(),
                "m+": date.getMinutes(),
                "s+": date.getSeconds()
            };
            if (/(y+)/.test(format)) {
                format = format.replace(RegExp.$1, (date.getFullYear() + "").substr(4 - RegExp.$1.length));
            }
            for (var k in o) {
                if (new RegExp("(" + k + ")").test(format)) {
                    format = format.replace(RegExp.$1, RegExp.$1.length == 1 ? o[k] : ("00" + o[k]).substr(("" + o[k]).length));
                }
            }
            return format;
        }
```

### js日期转换2 
```
JSON返回DateTime/Date('123123123')/解决办法
functionConvertJSONDateToJSDateObject(jsondate){
    vardate =newDate(parseInt(jsondate.replace("/Date(","").replace(")/",""),10));
    returndate;
}
　　只要把DateTime值传递给ConvertJSONDateToJSDateObject就可以返回Date。通过js调用。 如果想返回yyyy-MM-dd HH:mm:SS格式
?
functiongetDate(date) {
    varyear =date.getFullYear();
    varmonth = date.getMonth() +1;
    varday = date.getDate();
    returnyear +"-"+month +"-"+ day ;
}
functiongetDateTime(date) {
    varyear =date.getFullYear();
    varmonth = date.getMonth() +1;
    varday = date.getDate();
    varhh = date.getHours();
    varmm = date.getMinutes();
    varss = date.getSeconds();
    returnyear +"-"+month +"-"+ day +" "+ hh+":"+ mm +":"+ss;
}
```
### js移除数组指定元素
```
   <script type="text/javascript">
        Array.prototype.indexOf = function(val) {
            for (var i = 0; i < this.length; i++) {
                if (this[i] == val) return i;
            }
            return -1;
        };
        Array.prototype.remove = function(val) {
            var index = this.indexOf(val);
            if (index > -1) {
                this.splice(index, 1);
            }
        };

        var array = [1, 2, 3, 4, 5];
        array.remove(3);
                
    </script>
    ```
### 添加新元素
```
array.push(item1,item2……itemN);//将一个或多个元素加入数组，返回新数组的长度
array.unshift(item1,item2……itemN);//将一个或多个元素加入到数组的开始位置，原有元素位置自动后移，返回  新数组的长度
array.splice(start,delCount,item1,item2……itemN);//从start的位置开始向后删除delCount个元素，然后从start的位置开始插入一个或多个新元素
```
### 删除元素
```
array.pop();//删除最后一个元素，并返回该元素
array.shift();//删除第一个元素，数组元素位置自动前移，返回被删除的元素
array.splice(start,delCount);//从start的位置开始向后删除delCount个元素
```
### 数组的合并、截取
```
array.slice(start,end);//以数组的形式返回数组的一部分，注意不包括 end 对应的元素，如果省略 end 将复制 start 之后的所有元素
array.concat(array1,array2);//将多个数组拼接成一个数组
```
### 数组的排序
```
array.reverse();//数组反转
array.sort();//数组排序，返回数组地址
```
### 数组转字符串
```
array.join(separator);//将数组原因用separator连接起来
```





```