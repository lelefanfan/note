#cls_ecshop类库

[TOC]

##简介
ecshop基础类。

##ECS — 构造函数

**语法：** 
`ECS($db_name, $prefix)`

**参数：**
@param string db_name：数据库名称
@param string prefix：数据库表名称前缀

**返回值**
无

**说明**
初始化，对 `$this->db_name` 和 `$this->prefix` 进行赋值。


##table — 为表名称添加前缀

**语法：** 
`table($str)`

**参数：**
@param string str：数据表名称

**返回值**
返回添加表前缀后的表名称


##compile_password — 编译密码

**语法：** 
`compile_password($pass)`

**参数：**
@param string pass：被编译的密码

**返回值**
返回md5编译后的密码


##get_domain — 获取当前域名

**语法：** 
`get_domain()`

**返回值**
返回当前网站域名


##url — 获取url地址

**语法：** 
`url()`

**返回值**
返回当前网站域名,**好像根后台有点关系，有待进一步了解****。


##http — 获取当前环境的 HTTP协议方式

**语法：** 
`http()`

**返回值**
返回协议方式： 'https://'或 'http://'


##data_dir — 设置data目录路径

**语法：** 
`data_dir($sid = 0)`

**参数：**
@param int sid：？？？应该是session id，根据session id创建data目录。

**返回值**
data目录地址


##image_dir — 设置image目录路径

**语法：** 
`image_dir($sid = 0)`

**参数：**
@param int sid：？？？应该是session id，根据session id创建image目录。

**返回值**
image目录地址


<style>
    h1,h2,h3,h4,p,strong { font-family: "Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif }
    p { font-size: 16px; }
    code { color: #c7254e; background-color:#f9f2f4 !important; }
    .toc ul { list-style-type: none; margin-bottom: 15px; font-size:18px; font-family:"Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif;  }
</style>
<link href="http://cdn.bootcss.com/highlight.js/9.7.0/styles/vs.min.css" rel="stylesheet">
<script src="http://cdn.bootcss.com/highlight.js/9.7.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>