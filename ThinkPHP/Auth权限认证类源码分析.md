#Auth权限认证类源码分析
[TOC]

##属性

###配置属性[ $_config ]
用于设置**Auth权限认证类**的认证开关、认证方式及所关联的用户组数据表名、用户-用户组关系表、权限规则表、用户信息表。

源码如下：
```php
//默认配置
protected $_config = array(
    'AUTH_ON'           => true,                // 认证开关
    'AUTH_TYPE'         => 1,                   // 认证方式，1为实时认证；2为登录认证。
    'AUTH_GROUP'        => 'auth_group',        // 用户组数据表名
    'AUTH_GROUP_ACCESS' => 'auth_group_access', // 用户-用户组关系表
    'AUTH_RULE'         => 'auth_rule',         // 权限规则表
    'AUTH_USER'         => 'member'             // 用户信息表
);
```

##方法
###构造方法[ __construct() ]
用于设置表名称，分三步走：

- 获取表前缀；
- 为默认表加表前缀；
- 配置文件存在`AUTH_CONFIG`配置就覆盖类中的配置表名称。

源码如下：
```php
public function __construct() {
    //获取表前缀
    $prefix = C('DB_PREFIX');
    //连接表前缀
    $this->_config['AUTH_GROUP'] = $prefix.$this->_config['AUTH_GROUP'];
    $this->_config['AUTH_RULE'] = $prefix.$this->_config['AUTH_RULE'];
    $this->_config['AUTH_USER'] = $prefix.$this->_config['AUTH_USER'];
    $this->_config['AUTH_GROUP_ACCESS'] = $prefix.$this->_config['AUTH_GROUP_ACCESS'];
    //检测AUTH_CONFIG，存在就覆盖表名称
    //PS：AUTH_CONFIG中配置的表名必须包含表前缀
    if (C('AUTH_CONFIG')) {
        //可设置配置项 AUTH_CONFIG, 此配置项为数组。
        $this->_config = array_merge($this->_config, C('AUTH_CONFIG'));
    }
}
```

###检查权限[ check() ]
用于检查权限

源码如下：
```php
/**
  * 检查权限
  * @param name string|array  需要验证的规则列表,支持逗号分隔的权限规则或索引数组
  * @param uid  int           认证用户的id
  * @param string mode        执行check的模式
  * @param relation string    如果为 'or' 表示满足任一条规则即通过验证;如果为 'and'则表示需满足所有规则才能通过验证
  * @return boolean           通过验证返回true;失败返回false
 */
public function check($name, $uid, $type=1, $mode='url', $relation='or') {
    // 如果关闭验证，验证通过并返回true
    if (!$this->_config['AUTH_ON'])
        return true;

    //获取当前用户权限列表
    $authList = $this->getAuthList($uid,$type); 
    // 将验证规则转为数组格式
    if (is_string($name)) {
        $name = strtolower($name);
        if (strpos($name, ',') !== false) {
            $name = explode(',', $name);
        } else {
            $name = array($name);
        }
    }

    $list = array(); //保存验证通过的规则名
    // 如果 check模式为url 则获取url参数
    if ($mode=='url') {
        $REQUEST = unserialize( strtolower(serialize($_REQUEST)) );
    }
    
    // 循环当前用户权限列表
    foreach ( $authList as $auth ) {
        // $query 如果不存在url参数则保存规则，如果存在url参数则保存url参数
        // $auth 保存的规则是从权限表中取出来的，没有进行过数据加工
        // $query 与 $auth 的数据都来自数据库，前者有加工，后者没有
        $query = preg_replace('/^.+\?/U','',$auth);

        // 此处主要是对check模式为url，且存在url参数的规则进行验证
        if ($mode=='url' && $query!=$auth ) {
            // 将$query解析为数组，得到$param
            parse_str($query,$param); 
            // 获取 $REQUEST与$param 的交集
            $intersect = array_intersect_assoc($REQUEST,$param);
            // 去除 $auth 中的参数
            $auth = preg_replace('/\?.*$/U','',$auth);
            // 如果需要验证的规则存在于 $auth 中，并且url参数与数据库中相符，验证通过
            if ( in_array($auth,$name) && $intersect==$param ) {  //如果节点相符且url参数满足
                $list[] = $auth ;
            }
        }else if (in_array($auth , $name)){
            $list[] = $auth ;
        }
    }
    // 如果 $relation 为 ‘or’，只要求一条规则通过
    if ($relation == 'or' and !empty($list)) {
        return true;
    }
    // 如果 $relation 为 ‘and’，只要求一条规则通过
    $diff = array_diff($name, $list);
    if ($relation == 'and' and empty($diff)) {
        return true;
    }
    return false;
}
```
###获取用户组[ getGroups() ]
根据用户id获取用户组所有权限id

源码如下：
```php
/**
 * @param  uid int     用户id
 * @return array       用户所属的用户组权限id
 */
public function getGroups($uid) {
    // 用于保存当前用户权限id静态变量 $groups
    static $groups = array();
    // 如果存在于静态变量 $groups 中就直接返回
    if (isset($groups[$uid]))
        return $groups[$uid];

    // 数据库中获取当前用户所属用户组权限id，可以属于多个用户组
    $user_groups = M()
        ->table($this->_config['AUTH_GROUP_ACCESS'] . ' a')
        ->where("a.uid='$uid' and g.status='1'")
        ->join($this->_config['AUTH_GROUP']." g on a.group_id=g.id")
        ->field('rules')->select();
    $groups[$uid]=$user_groups?:array();
    // 返回
    return $groups[$uid];
}
```

###获取权限列表[ getAuthList() ]
获取用户权限列表，分三步走：

- 根据 用户id，类型获取当前用户的规则列表 
- 可以定义condition条件，返回符合条件的规则列表
- 如果为登录认证，则将规则列表返回的同时保存到session中

源码如下：
```php
/**
 * 获得权限列表
 * @param integer $uid  用户id
 * @param integer $type 权限类型，URL（1）与主菜单（2）
 * 说明：
 * 1.根据用户id，权限类型获取当前用户的规则列表
 * 2.如果存在condition条件，根据condition条件获取当前用户的规则列表
 * 3.如果为登录认证，则将规则列表返回的同时保存到session中
 */
protected function getAuthList($uid,$type) {
    // 用于保存权限列表静态变量 $_authList
    static $_authList = array();
    // 用于保存权限类型 
    $t = implode(',',(array)$type); //in,1,2

    // 检测 $_authList 中是否存在当前用户的权限列表，如果存在就返回
    if (isset($_authList[$uid.$t])) {
        return $_authList[$uid.$t];
    }

    // 如果登录方式为登录认证，并且在session中存在当前用户的权限列表就返回
    // AUTH_TYPE：1表示实时认证，2表示登录认证
    if( $this->_config['AUTH_TYPE']==2 && isset($_SESSION['_AUTH_LIST_'.$uid.$t])){
        return $_SESSION['_AUTH_LIST_'.$uid.$t];
    }

    //获取用户组所有权限列表
    $groups = $this->getGroups($uid);
    //用于保存当前用户全部用户组所有权限id,用数组方式进行存储
    $ids = array();
    foreach ($groups as $g) {
        $ids = array_merge($ids, explode(',', trim($g['rules'], ',')));
    }
    $ids = array_unique($ids);

    // 如果不存在权限列表，返回空数组
    if (empty($ids)) {
        $_authList[$uid.$t] = array();
        return array();
    }

    //设置 auth_rule 表查询条件
    $map=array(
        'id'=>array('in',$ids),
        'type'=>$type,
        'status'=>1,
    );

    //获取当前用户已有权限的规则 name与condition字段，用于再次验证
    $rules = M()->table($this->_config['AUTH_RULE'])->where($map)->field('condition,name')->select();

    $authList = array();
    // 循环权限列表验证 condition 字段的条件
    foreach ($rules as $rule) {
        //如果 condition 不为空，就继续验证
        if (!empty($rule['condition'])) { 
            //获取用户信息,一维数组
            $user = $this->getUserInfo($uid);
            //条件判断
            $command = preg_replace('/\{(\w*?)\}/', '$user[\'\\1\']', $rule['condition']);
            @(eval('$condition=(' . $command . ');'));//满足条件返回真
            if ($condition) {
                $authList[] = strtolower($rule['name']);
            }
        } else {
            // condition中不存在条件，直接存储
            $authList[] = strtolower($rule['name']);
        }
    }
    // 保存规则列表
    $_authList[$uid.$t] = $authList;
    // 如果认证方式为登录认证，就将规则列表保存到session中
    if($this->_config['AUTH_TYPE']==2){
        //规则列表结果保存到session
        $_SESSION['_AUTH_LIST_'.$uid.$t]=$authList;
    }
    // 去重复后返回
    return array_unique($authList);
}
```

###获取用户资料[ getUserInfo() ]
根据用户的 UID 获取用户资料。

源码如下：
```php
protected function getUserInfo($uid) {
    // 用于保存用户信息静态变量
    static $userinfo=array();
    // 如果 $userinfo 中不存在，就根据 $uid 从数据库中获取
    if(!isset($userinfo[$uid])){
         $userinfo[$uid]=M()->where(array('uid'=>$uid))->table($this->_config['AUTH_USER'])->find();
    }
    // 返回用户信息
    return $userinfo[$uid];
}
```






<style>
    h1,h2,h3,p,strong { font-family: "Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif }
    p { font-size: 16px; }
    .toc ul { list-style-type: none; margin-bottom: 15px; font-size:18px; font-family:"Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif;  }
</style>
<link href="http://cdn.bootcss.com/highlight.js/9.7.0/styles/vs.min.css" rel="stylesheet">
<script src="http://cdn.bootcss.com/highlight.js/9.7.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>