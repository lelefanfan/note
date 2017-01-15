#utils — 工具库

[TOC]

##浏览器检测
该对象为`var Browser = new Object();`，包含五个属性：

###Browser.isMozilla
是否为？？？
###Browser.isIE
是否为IE浏览器
###Browser.isFirefox
是否为火狐浏览器
###Browser.isSafari
是否为Safari（苹果）浏览器
###Browser.isOpera
是否为Opers（欧朋）浏览器

##实用工具
该对象为`var Utils = new Object();`，包含14个方法：

###htmlEncode(val) - html编码
将 `&`、`"`、`<`、`>`4个符号转为html实体代码
###trim(val) - 清除
清除字符串两边空白的字符
###isEmpty(val) - 检测是否为空
###isNumber(val) - 检测是否为数值型？？？
###isInt() - 检测是否为Int型？？？
###isEmail() - 检测是否为Email格式
###isTel() - 检测是否为电话格式
###fixEvent() - 获取事件对象？？？
###srcElement() - 获取事件目标对象？？？
###isTime() - 检测是否为时间格式  
匹配格式为：`2016-01-01 22:30`
###x() - 鼠标x轴坐标
###y() - 鼠标y轴坐标
###request() - ？？？
###$() - 根据元素id获取DOM对象

##实用函数
###rowindex(tr)
###document.getCookie(sName)
###document.setCookie(sName, sValue, sExpires)
###document.removeCookie(sName,sValue)
###getPosition(o)
###cleanWhitespace(element)









<style>
    h1,h2,h3,h4,p,strong { font-family: "Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif }
    p { font-size: 16px; }
    code { color: #c7254e; background-color:#f9f2f4 !important; }
    .toc ul { list-style-type: none; margin-bottom: 15px; font-size:18px; font-family:"Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif;  }
</style>
<link href="http://cdn.bootcss.com/highlight.js/9.7.0/styles/vs.min.css" rel="stylesheet">
<script src="http://cdn.bootcss.com/highlight.js/9.7.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>