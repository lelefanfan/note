#cls_template模板类

[TOC]

##属性
##方法
###is_cached - 判断是否缓存
**说明：**
`boolean is_cached(string $filename, string $cache_id = '')`
is_cached() 判断文件名为 filename 的文件是否存在，如果 cache_id 不为空，则判断该缓存id下文件是否存在。
**参数：**
`string $filename` 文件名
`string $cache_id` 缓存id
**返回值：**
存在缓存文件返回true，否则返回false。
**说明：**
如果存在缓存文件。获取缓存文件数组 $para ，如果 $para 存在并且缓存时间 $para['expires'] 有效，为模板对象 $this->_expires 赋 $para['expires'] 值，为模板对象 $this->template_out 赋 缓存文件中静态代码，同时还检测 $para['template'] 所有库文件的缓存时间，任何一个过期，就返回 false。

如果不存在缓存文件，返回false。

###select - 处理模板标签
**说明：**
` select(string $tag)`
select() 处理 tag 标签，将它编译为编译文件即PHP代码。
**参数：**
`string $tag` 标签名
**返回值（实际参数中是没有{}标签的，这里为了便于理解，加上了{}标签）：**
{}：'{}'
{ * 注释 *}：' '
{$变量}：`'<?php echo ' . $this->get_val(substr($变量, 1)) . '; ?>'` 
{/if}：`<?php endif; ?>`
{/foreach}：???
{/literal}: ' '



###get_val - 处理变量标签
**说明：**
` get_val($val)`
select() 处理变量标签。
**参数：**
`string $val` 标签名，如果一个标签是 {$变量 }
**返回值（实际参数中是没有{}标签的，这里为了便于理解，加上了{}标签）：**


<style>
    h1,h2,h3,h4,p,strong { font-family: "Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif }
    p { font-size: 16px; }
    code { color: #c7254e; background-color:#f9f2f4 !important; }
    .toc ul { list-style-type: none; margin-bottom: 15px; font-size:18px; font-family:"Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif;  }
</style>
<link href="http://cdn.bootcss.com/highlight.js/9.7.0/styles/vs.min.css" rel="stylesheet">
<script src="http://cdn.bootcss.com/highlight.js/9.7.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>