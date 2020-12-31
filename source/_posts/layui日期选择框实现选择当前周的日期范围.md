---
title: layui日期选择框实现选择当前周的日期范围
date: 2020-10-01 23:47:44
categories: 前端
tags: layui
---
##### 话不多说，直接上代码

```
layui.use(['laydate'], function() {
    var laydate = layui.laydate;
    var monday = getMonday(new Date());
    var mm = layui.util.toDateString(monday,'yyyy-MM-dd')
    var sunday = GetDateStr(monday,6);
    laydate.render({
            elem: '#daterange'//绑定的html元素id
            ,type:'date'
            ,format: 'yyyy-MM-dd' //格式
            ,trigger : 'click'
            ,min:mm //最小可选择日期
            ,max:sunday //最大可选择日期
            ,range:true //设置启用日期范围
        });
 })
 //获取当前日期的周一日期
 function getMonday( date ) {
            var day = date.getDay() || 7;  
            if( day !== 1 ) 
            date.setHours(-24 * (day - 1)); 
            return date;
        }
//获取某日期的第n天后的日期
 function GetDateStr(date,n) {   
               var dd = date;  
               dd.setDate(dd.getDate()+n);  
               var y = dd.getFullYear();   
               var m = (dd.getMonth()+1)<10?"0"+(dd.getMonth()+1):(dd.getMonth()+1);
               var d = dd.getDate()<10?"0"+dd.getDate():dd.getDate();
            return y+"-"+m+"-"+d;   
        };
```