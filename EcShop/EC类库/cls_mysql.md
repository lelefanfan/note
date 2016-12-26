#cls_mysql类

[TOC]

##简介
用于mysql数据库的api。代表PHP与MYSQL之间的一个连接。

##cls_mysql — 构造函数
##connect — 连接数据库
##select_database — 选择数据库
##set_mysql_charset — 设置数据库编码
##fetch_array — 从结果集中取得一行作为关联数组，或数字数组，或二者兼有
##query — 执行sql语句
##affected_rows — 取得前一次 MySQL 操作所影响的记录行数
##error — 获取上一个 MySQL 操作产生的文本错误信息
##errno — 获取上一个 MySQL 操作中的错误信息的数字编码 
##result — 取得结果数据
##num_rows — 取得结果集中行的数目 
##num_fields — 取得结果集中字段的数目
##free_result — 释放结果内存
##insert_id — 取得上一步INSERT操作产生的 ID
##fetchRow — 从结果集中取得一行作为关联数组
##fetch_fields — 从结果集中取得列信息并作为对象返回
##version — 获取MySQL版本信息
##ping — 一个服务器连接，如果没有连接则重新连接 
##escape_string — 转义SQL语句中使用的字符串中的特殊字符，并考虑到连接的当前字符集
##close — 关闭 MySQL 连接
##ErrorMsg — 输出错误信息
##selectLimit — 为sql语句拼接 LIMIT参数
##getOne — 从结果集中取得一行作为枚举数组
##getOneCached — 返回带缓存的一条数据库数据
##getAll — 执行sql语句，并返回全部结果集
##getAllCached — ？？？
##getRow — 从结果集中取得一行作为关联数组
##getRowCached — ？？？
##getCol — 获取结果集的第一个字段值
##getColCached — ？？？
##autoExecute — 自动执行INSERT或UPDATE
##autoReplace — 自动添加更新数据
##setMaxCacheTime — ？？？
##setSqlCacheData — ？？？
##table_lastupdate — 获取SQL语句中最后更新的表的时间，有多个表的情况下，返回最新的表的时间
##get_table_name — ？？？
##set_disable_cache_tables — 设置不允许进行缓存的表












<style>
    h1,h2,h3,h4,p,strong { font-family: "Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif }
    .markdown-body h3 { padding-left:20px; }
    p { font-size: 16px; }
    code { color: #c7254e; background-color:#f9f2f4 !important; }
    .toc ul { list-style-type: none; margin-bottom: 15px; font-size:18px; font-family:"Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif;  }
    .toc li { padding-bottom: 8px;  }
</style>
<link href="http://cdn.bootcss.com/highlight.js/9.7.0/styles/vs.min.css" rel="stylesheet">
<script src="http://cdn.bootcss.com/highlight.js/9.7.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>