#Auth权限认证类使用教程
通过对Auth权限认证类的源码进行分析，对Auth权限认证有了进一步的认识。为加深印象，便于复习，特整理使用教程如下：

[TOC]

##验证原理
通常我们使用 Auth 权限认证类进行权限验证用法如下：

```php
$Auth = new \Think\Auth();
/*
 * @param string|array name 
 * @param int uid  
 * @param int type 
 * @param string mode 
 */
if(!$Auth->check($name,$uid,$type,$mode)){
    // 验证失败
    return false;
}else{
    // 验证通过
    return true;
}
```

通过以上代码，感觉 Auth 权限认证类的使用非常简单，但是我们要把这个类用好，必须知道其原理，也就是运行流程，才能知其所以然。

通过对源码分析，该类在使用 $Auth->check()方法时，大致走了如下流程：

- 获取当前用户所在用户组的全部权限规则，以数组方式返回，此处有两项重要验证
1. 根据用户id，规则id，权限type，状态status取得当前用户的所有权限
2. 在第一步的基础上，对于存在condition条件的，进行再次验证
- 根据 $mode 模式与url参数进行权限验证

$Auth->check()方法大致的验证就是上面的几步，当然其中还有很多细节，就需要分析源码去学习了。

##使用教程
###数据添加
对用户组数据表名、用户-用户组关系表、权限规则表、用户信息表按照关联关系添加基础数据
###后台建设
根据四个表建立后台，主要是增删改查
###权限验证
这里我只说大概流程，具体还请查阅onethink代码，或其他成熟框架代码

- 建立一个后台验证类，在此处引入Auth类，进行权限验证
- 所有控制器都继承后台验证类

###使用心得

- 权限表中的 condition 条件表达式的字段必须是用户表中的字段，且只能验证一个字段。
- Auth类是对规则进行验证，而不是对节点进行验证，但是可以把节点当作规则来用，进行权限验证。
- 使用前可以在配置信息中对 AUTH_CONFIG 以数组的方式进行配置，来确定四个表的名字，但是在此配置中的配置必须包含表前缀。





<style>
    h1,h2,h3,p,strong { font-family: "Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif }
    p { font-size: 16px; }
    .toc ul { list-style-type: none; margin-bottom: 15px; font-size:18px; font-family:"Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif;  }
</style>
<link href="http://cdn.bootcss.com/highlight.js/9.7.0/styles/vs.min.css" rel="stylesheet">
<script src="http://cdn.bootcss.com/highlight.js/9.7.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>