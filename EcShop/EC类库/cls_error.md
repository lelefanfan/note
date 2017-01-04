#ecs_error类库

[TOC]

##简介
用户级错误处理类

##ecs_error — 构造函数

**语法：** 
`ecs_error($tpl)`

**参数：**
@param string tpl：指定错误模板路径

**返回值**
无

**说明**
设置用于显示错误的模板


##add — 添加一条错误信息

**语法：** 
`add($msg, $errno=1)`

**参数：**
@param string/array msg：错误信息
@param int errno：错误编号

**返回值**
无

**说明**
如果 `$msg` 是数组类型，就把它与 `$this->_message` 合并，如果 `$msg` 是字符串类型，就直接赋值给  `$this->_message` 。然后再设置 `$this->error_no` 错误编号。


##clean — 清空错误信息

**语法：** 
`clean()`

**返回值**
无

**说明**
将属性 `$this->_message` 设置为空数组，将属性 `$this->error_no`  设置为0。


##get_all — 获取全部错误信息

**语法：** 
`get_all()`

**返回值**
数组类型：一个包含全部错误信息的数组

**说明**
将 `$this->_message` 属性值返回。


##last_message — 返回最后一条错误信息

**语法：** 
`last_message()`

**返回值**
字符型：返回最后一条错误信息

**说明**
将 `$this->_message` 数组最后一条信息返回。



##show — 显示错误信息

**语法：** 
`show($link = '', $href = '')`

**参数：**
@param string link：错误信息提示文字
@param string href：错误信息跳转地址

**返回值**
无

**说明**
如果不存在smarty引擎，直接输出错误信息，如果存在，显示错误模板，并注入相关变量。




<style>
    h1,h2,h3,h4,p,strong { font-family: "Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif }
    p { font-size: 16px; }
    code { color: #c7254e; background-color:#f9f2f4 !important; }
    .toc ul { list-style-type: none; margin-bottom: 15px; font-size:18px; font-family:"Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif;  }
</style>
<link href="http://cdn.bootcss.com/highlight.js/9.7.0/styles/vs.min.css" rel="stylesheet">
<script src="http://cdn.bootcss.com/highlight.js/9.7.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>