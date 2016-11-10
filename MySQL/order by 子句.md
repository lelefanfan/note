#order by 子句

[TOC]

## 语法
`order by 字段1 【asc|desc】，字段2 【asc|desc】，......`

## 定义
`ordey by`子句用于将前面“取得”的数据以设定的标准（字段）来进行排序以输出结果。

- 对前面的结果数据以指定的一个或多个字段排序；
- 排序可以谁定正序（asc，默认值）或倒序（desc）；
- 多个字段的排序，都是在前一个字段排序基础上，如果还有“相等值”，才继续以后续字段排序。















<style>
    h1,h2,h3,h4,p,strong { font-family: "Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif }
    p { font-size: 16px; }
    code { color: #c7254e; background-color:#f9f2f4 !important; }
    .toc ul { list-style-type: none; margin-bottom: 15px; font-size:18px; font-family:"Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif;  }
</style>
<link href="http://cdn.bootcss.com/highlight.js/9.7.0/styles/vs.min.css" rel="stylesheet">
<script src="http://cdn.bootcss.com/highlight.js/9.7.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>