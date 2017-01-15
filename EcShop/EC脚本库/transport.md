#transport类 — 用于支持AJAX的传输类

[TOC]

##类属性
###filename — 存储本对象所在的文件名
默认为`transport.js`文件
###debugging — 存储调试信息
存储是否进入调试模式的开关，打印调试消息的方式，换行符，调试用的容器的ID。
```js
var debugging = {
  isDebugging : 0, //调试模式开关，1：打开，0：关闭
  debuggingMode : 0, //调试信息显示模式，1：innerHTML，2：alert
  linefeed : "", //换行符
  containerId : 0 //显示错误的容器ID
}
```

##类方法
###debug() — 设置调试信息

**语法：**`debug(isDebugging, debuggingMode)`
**参数：**
@param   {int}   是否打开调试模式      0：关闭，1：打开
@param   {int}   打印调试消息的方式    0：alert，1：innerHTML
**返回：**
无

###onComplete() — 传输完毕后自动调用的方法

**语法：**`onComplete()`
**说明：**
该方法将在`run()`方法的参数`callback`回调函数执行之前执行
**默认动作`Ajax.onComplete = hideLoader;`隐藏载入信息**
###onRunning() — 传输过程中自动调用的方法

**语法：**`onRunning()`
**说明：**
分两种情况：一是异步，在`open()`方法之前执行，必须参数`quiet`为false才会执行；二是同步，同步的情况下，会跟异步相同条件的执行一次，然后再`send()`方法之前还会执行一次。
**默认动作`Ajax.onRunning  = showLoader;`显示载入信息**

###run() — 调用此方法发送HTTP请求

**语法：**`run(url, params, callback, transferMode, responseType, asyn, quiet)`
**参数：**
@param {string}   url          请求的URL地址
@param {mix}      params       发送参数
@param {Function} callback     回调函数
@param {string}   ransferMode  请求的方式，有"GET"和"POST"两种
@param {string}   responseType 响应类型，有"JSON"、"XML"和"TEXT"三种
@param {boolean}  asyn         是否异步请求的方式
@param {boolean}  quiet        是否安静模式请求
**返回：**
无
**说明：**
看代码：
```js
function run(url, params, callback, transferMode, responseType, asyn, quiet)
{
    params = this.parseParams(params); //解析参数
    transferMode = typeof(transferMode) === "string"
    && transferMode.toUpperCase() === "GET"
    ? "GET"
    : "POST"; //请求方式，只有POST与GET两种
    if (transferMode === "GET") //如果是GET请求，将请求url与params进行拼接，返回新的url
    {
      var d = new Date();

      // 设置get请求url，将url与params拼接
      url += params ? (url.indexOf("?") === - 1 ? "?" : "&") + params : "";
      url = encodeURI(url) + (url.indexOf("?") === - 1 ? "?" : "&") + d.getTime() + d.getMilliseconds();
      params = null;
    }
    // 返回类型，有"JSON"、"XML"和"TEXT"三种
    responseType = typeof(responseType) === "string" && ((responseType = responseType.toUpperCase()) === "JSON" || responseType === "XML") ? responseType : "TEXT";
    // 异步或者同步，异步为true，同步为false
    asyn = asyn === false ? false : true;
    // 创建XMLHttpRequest对象
    var xhr = this.createXMLHttpRequest();
    try
    {
      var self = this; //将当前对象赋值给self
      // 传输过程中自动调用方法
      if (typeof(self.onRunning) === "function" && !quiet)
      {
        self.onRunning();
      }
      // 规定请求的类型、URL 以及是否异步处理请求
      xhr.open(transferMode, url, asyn);
      // POST请求头信息设置
      if (transferMode === "POST")
      {
        xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
      }
      if (asyn) // 异步
      {
        xhr.onreadystatechange = function ()
        {
          if (xhr.readyState == 4)
          {
            switch ( xhr.status )
            {
              case 0:
              case 200: // OK!
                /*
                 * If the request was to create a new resource
                 * (such as post an item to the database)
                 * You could instead return a status code of '201 Created'
                 */
                // 请求完成后自动调用的方法
                if (typeof(self.onComplete) === "function")
                {
                  self.onComplete();
                }
                //执行回调函数
                if (typeof(callback) === "function")
                {
                  //这里会报错呢。。真是666  原因是xhr.responseText不是对象格式的字符串,担心有其他功能,这里先搁置
                  callback.call(self, self.parseResult(responseType, xhr), xhr.responseText);
                }
              break;
              case 304: // Not Modified
                /*
                 * This would be used when your Ajax widget is
                 * checking for updated content,
                 * such as the Twitter interface.
                 */
              break;
              case 400: // Bad Request
                /*
                 * A bit like a safety net for requests by your JS interface
                 * that aren't supported on the server.
                 * "Your browser made a request that the server cannot understand"
                 */
                 alert("XmlHttpRequest status: [400] Bad Request");
              break;
              case 404: // Not Found
                alert("XmlHttpRequest status: [404] \nThe requested URL "+url+" was not found on this server.");
              break;
              case 409: // Conflict
                /*
                 * Perhaps your JavaScript request attempted to
                 * update a Database record
                 * but failed due to a conflict
                 * (eg: a field that must be unique)
                 */
              break;
              case 503: // Service Unavailable
                /*
                 * A resource that this request relies upon
                 * is currently unavailable
                 * (eg: a file is locked by another process)
                 */
                 alert("XmlHttpRequest status: [503] Service Unavailable");
              break;
              default:
                alert("XmlHttpRequest status: [" + xhr.status + "] Unknow status.");
            }
            xhr = null;
          }
        }
        // 发送请求
        if (xhr != null) xhr.send(params);
      }
      else // 同步
      {
        // 运行中自动执行的方法
        if (typeof(self.onRunning) === "function")
        {
          self.onRunning();
        }
        // 发送请求
        xhr.send(params);
        var result = self.parseResult(responseType, xhr);
        //xhr = null;
        if (typeof(self.onComplete) === "function")
        {
          self.onComplete();
        }
        if (typeof(callback) === "function")
        {
          callback.call(self, result, xhr.responseText);
        }
        return result;
      }
    }
    catch (ex)
    {
      if (typeof(self.onComplete) === "function")
      {
        self.onComplete();
      }
      alert(this.filename + "/run() error:" + ex.description);
    }
}
```


###displayDebuggingInfo() — 显示错误信息

**语法：**`displayDebuggingInfo(info, type)`
**参数：**
 @param {string} info 调试信息
 @param {string} type 信息类型
**返回：**
无
**说明：**
如果属性 `this.debugging.debuggingMode` 为0，会以`alert()`的方式弹出错误信息；如果 `this.debugging.debuggingMode` 为1，会根据`this.debugging.containerId`获取或创建显示错误信息的容器，如果参数`type`为param，就将错误信息显示在错误容器里的第一个div，否则显示在错误容器的第二个div。

###createXMLHttpRequest() — 创建XMLHttpRequest对象的方法

**语法：**`createXMLHttpRequest()`
**返回：**
返回`XMLHTTPRequest`对象

###onXMLHttpRequestError() — 当传输过程发生错误时将调用此方法

**语法：**`onXMLHttpRequestError(xhr, url)`
**参数：**
@param   {Object}    xhr     XMLHttpRequest对象
@param   {String}    url     HTTP请求的地址
**说明：**
抛出一个错误到控制台。

###parseParams() — 对将要发送的参数进行格式化

**语法：**`parseParams(params)`
**参数：**
@params {mix} params 将要发送的参数
**返回：**
@return 返回合法的参数
**说明：**
如果参数格式为String类型，直接返回；如果参数格式为Object类型，按`"JSON=" + params.toJSONString();`返回；否则会提示无效参数返回false。
如果开启调试，会显示调试信息。

###preFilter() — 对返回的HTTP响应结果进行过滤

**语法：**`preFilter(result)`
**参数：**
@params {mix} result HTTP响应结果
**返回：**
@return 返回过滤后的结果
**说明：**
替换掉参数`result`的BOM头信息。

###parseResult() — 对返回的结果进行格式化

**语法：**`parseResult(responseType, xhr)`
**参数：**
@params {string} responseType 返回类型
@params {XMLHTTPRequest} xhr XMLHTTPRequest对象
**返回：**
@return 返回指定格式的响应内容
**说明：**
如果指定`responseType`为JSON，那么将返回JSON对象，如果为XML，那么将返回XML对象，如果为TEXT，那么将返回字符串。同时，根据调试设置判断是否显示调试信息。


##类别名
该类定义了两个别名：分别是 `var Ajax = Transport;` 和 `Ajax.call = Transport.run;`

##重写
该文件为包装对象添加了`toJSONString()`方法：
###array.toJSONString()
将数组对象转为字符串格式
###boolean.toJSONString()
将布尔对象转为字符串格式
###date.toJSONString()
将日期对象转为字符串格式，默认格式为`2017-01-10T21:32:49`
###object.toJSONString()
将对象转为JSON字符串格式，转换时，会自动过滤掉对象的方法。
###string.toJSONString()
将JSON对象转为JSON字符串？？？
###string.parseJSON
将JSON字符串转为JSON对象










<style>
    h1,h2,h3,h4,p,strong { font-family: "Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif }
    p { font-size: 16px; }
    code { color: #c7254e; background-color:#f9f2f4 !important; }
    .toc ul { list-style-type: none; margin-bottom: 15px; font-size:18px; font-family:"Helvetica Neue",Arial,"Hiragino Sans GB","STHeiti","Microsoft YaHei","WenQuanYi Micro Hei",SimSun,Song,sans-serif;  }
</style>
<link href="http://cdn.bootcss.com/highlight.js/9.7.0/styles/vs.min.css" rel="stylesheet">
<script src="http://cdn.bootcss.com/highlight.js/9.7.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>