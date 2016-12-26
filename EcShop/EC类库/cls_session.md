#cls_session类库

[TOC]

##简介
EcShop用于Session操作的API类。

##session过期时间
客户端cookie的过期时间是浏览器关闭即过期
服务器端的session过期时间默认是创建session后30分钟

##cls_session — 构造函数

**语法：** 
`cls_session(&$db, $session_table, $session_data_table, $session_name = 'ECS_ID', $session_id = '')`

**参数：**
@param & db：数据库对象引用
@param string session_table：session表
@param string session_data_table：session数据库表
@param string session_name：session_name值
@param string session_id：session_id值

**返回值**
无

**说明**
用于cls_session类初始化工作。
1. 为相关属性赋值
2. cookie中存在sessionid并合法，加载session
3. cookie中不存在sessionid，生成cookie
4. 清理过期的session

##gen_session_id — 初始化sessionid并插入数据库

**语法：** 
`gen_session_id()`

**返回值**
返回布尔值。成功：true；失败：false。

**说明**
初始化一个sessionid值，并将该sessionid值插入数据库`sessions`表，除存储sessionid的字段，其余字段均为初始值或空值。

##gen_session_key  — 获取sessionkey

**语法**
`gen_session_key($session_id)`

**参数**
@param string session_id：sessionid值

**返回值**
返回字符串，session key。

**说明**
根据 session_id 加密，得到 session key。

##insert_session  — 插入session

**语法**
`insert_session()`

**返回值**
返回布尔值。成功：true；失败：false。

**说明**
得到sessionid后，插入一条空数据到数据库 `sessions` 表，使用该方法前必须 `$this->session_id` 有值。

##loade_session  — 加载session

**语法**
`load_session()`

**返回值**
无

**说明**
根据 `$this->session_id` 获取session信息存储到全局变量 `$GLOBALS['_SESSION']`中。
1. 如果数据库中不存在session，根据 `$this->session_id` 初始化一条session信息。
2. 如果存在就将session信息存储到全局变量 `$GLOBALS['_SESSION']`中。

##update_session  — 更新session

**语法**
`update_session()`

**返回值**
返回布尔值。成功：true；失败：false。

**说明**
更新session。将全局变量 `$GLOBALS['_SESSION']`中的session信息更新到数据表中。

ps:`isset($data{255})`如果为真才会更新到数据库`sessions_data`表，这个值到底代表什么？

##close_session  — 关闭session

**语法**
`close_session()`

**返回值**
返回布尔值。成功：true；失败：false。

**说明**
1. 使用`$this->update_session()`更新session
2. 从数据库 `sessions`、`sessions_data`表中删除过期session

##delete_spec_admin_session  — 删除指定管理员session

**语法**
`delete_spec_admin_session($adminid)`

**参数**
@param int adminid：管理员id

**返回值**
返回布尔值。成功：true；失败：false。

**说明**
根据 `$adminid` 到数据库`sessions`表中删除session信息。


##destroy_session  — 销毁session

**语法**
`destroy_session()`

**返回值**
返回布尔值。成功：true；失败：false。

**说明**
1. 清空全局变量 `$GLOBALS['_SESSION'] = array()`
2. 清空cookie信息
3. 根据sessionid选择删除购物车信息
4. 根据sessionid从数据库表`sessions_data`表中删除session信息
5. 根据sessionid从数据库表`sessions`表中删除session信息

##get_session_id  — 获取session id

**语法**
`get_session_id()`

**返回值**
成功返回session id

##get_users_count  — 获取数据库sessions表sessions总条数

**语法**
`get_users_count()`

**返回值**
成功返回数据库sessions表sessions总条数




<style>
    h1,h2,h3,h4,p,strong { font-family: "Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif }
    p { font-size: 16px; }
    code { color: #c7254e; background-color:#f9f2f4 !important; }
    .toc ul { list-style-type: none; margin-bottom: 15px; font-size:18px; font-family:"Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif;  }
</style>
<link href="http://cdn.bootcss.com/highlight.js/9.7.0/styles/vs.min.css" rel="stylesheet">
<script src="http://cdn.bootcss.com/highlight.js/9.7.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>