#lib_time时间函数库

[TOC]

##简介
EC时间函数API。

##gmtime — 获得当前格林威治时间的时间戳

**语法：** 
`gmtime()`

**返回值**
字符串，格林威治时间的时间戳

**说明**
返回自从 Unix 纪元（格林威治时间 1970 年 1 月 1 日 00:00:00）到当前时间的秒数。 

##server_timezone — 获得服务器的时区

**语法：** 
`server_timezone()`

**返回值**
字符串，服务器的时区。

**说明**
根据时区不同返回不同值。 


##local_mktime — 生成一个用户自定义时区日期的GMT时间戳

**语法：** 
`local_mktime($hour = NULL , $minute= NULL, $second = NULL,  $month = NULL,  $day = NULL,  $year = NULL)`

**参数**
@param int hour：时
@param int minute：分
@param int second：秒
@param int month：月
@param int day：日
@param int year：年

**返回值**
字符串，根据参数转换的Unix时间戳。


##local_date — 将GMT时间戳格式化为用户自定义时区日期

**语法：** 
`local_date($format, $time = NULL)`

**参数**
@param string format：格式符，参考php的`date()`函数
@param int time：该参数必须是一个GMT的时间戳

**返回值**
字符串，用户自定义时区日期。


##gmstr2time — 转换字符串形式的时间表达式为GMT时间戳

**语法：** 
`gmstr2time($str)`

**参数**
@param string str：字符串形式的时间表达式为，可以参考php的`strtotime()`函数

**返回值**
字符串，GMT时间戳。


##local_strtotime — 将一个用户自定义时区的日期转为GMT时间戳

**语法：** 
`local_strtotime($str)`

**参数**
@param string str：用户自定义时区的日期转

**返回值**
字符串，GMT时间戳。


##local_gettime — 获得用户所在时区指定的时间戳

**语法：** 
`local_gettime($timestamp = NULL)`

**参数**
@param int timestamp：该时间戳必须是一个服务器本地的时间戳

**返回值**
字符串，GMT时间戳。


##local_getdate — 获得用户所在时区指定的日期和时间信息

**语法：** 
`local_getdate($timestamp = NULL)`

**参数**
@param int timestamp：该时间戳必须是一个服务器本地的时间戳

**返回值**
？？？



<style>
    h1,h2,h3,h4,p,strong { font-family: "Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif }
    p { font-size: 16px; }
    code { color: #c7254e; background-color:#f9f2f4 !important; }
    .toc ul { list-style-type: none; margin-bottom: 15px; font-size:18px; font-family:"Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif;  }
</style>
<link href="http://cdn.bootcss.com/highlight.js/9.7.0/styles/vs.min.css" rel="stylesheet">
<script src="http://cdn.bootcss.com/highlight.js/9.7.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>