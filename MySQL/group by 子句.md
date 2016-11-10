#group by 字句

[TOC]

##语法
`group by 字段1 [desc|asc], 字段2 [desc|asc],...`

##分组定义
将多行数据以某种标准（就是指定的字段）来进行“分类”存放。

- 分组是对“前述”已经找出的数据（即where已经筛选过了）进行某种指定标准（依据）的分组；
- 分组结果，可以同时指定其“排序方式”：desc（倒序），asc（顺序）；
- 通常，分组就一个字段（依据），2个以上很少；
- 分组之后，数据就变成一个组，所以在select语句中的“输出（取出）”部分，只能出现组信息。形式：`select 组信息1，组信息2，..... from 数据源 group by 字段；`。

##分组后的数据
通过`group by`进行分组以后，通常只有如下几种可用的“组信息”（即可以出现在select中的信息）：

1. 分组依据本身的信息，其实就是该分组依据的字段名；
2. 每一组的“数量”信息：就是用count（*）获得；
3. 原来数据中的“数值类型字段的聚合信息”，包括如下几个：

- 最大值：  max(字段名)
- 最小值：  min(字段名)
- 平均值：  avg(字段名)
- 总和值：  sum(字段名)



















<style>
    h1,h2,h3,h4,p,strong { font-family: "Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif }
    p { font-size: 16px; }
    code { color: #c7254e; background-color:#f9f2f4 !important; }
    .toc ul { list-style-type: none; margin-bottom: 15px; font-size:18px; font-family:"Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif;  }
</style>
<link href="http://cdn.bootcss.com/highlight.js/9.7.0/styles/vs.min.css" rel="stylesheet">
<script src="http://cdn.bootcss.com/highlight.js/9.7.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>