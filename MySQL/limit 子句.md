#limit 子句

[TOC]

## 语法
`limit  起始行号，要取出的行数；`

## 定义
`limit`子句用于将“前述取得的数据”，按指定的行取出来。从第几行开始取出多少行。

- 起始行号都是从0开始算起的；
- 起始行号跟数据中的任何一个字段（比如id）没有关系；
- 要取出的行数也是一个数字，自然应该是大于0的；
- 有一个简略形式：limit 行数；  表示直接从第0行开始取出指定的行数，它相当于limit 0,行数;















<style>
    h1,h2,h3,h4,p,strong { font-family: "Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif }
    p { font-size: 16px; }
    code { color: #c7254e; background-color:#f9f2f4 !important; }
    .toc ul { list-style-type: none; margin-bottom: 15px; font-size:18px; font-family:"Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif;  }
</style>
<link href="http://cdn.bootcss.com/highlight.js/9.7.0/styles/vs.min.css" rel="stylesheet">
<script src="http://cdn.bootcss.com/highlight.js/9.7.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>