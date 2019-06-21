
---

title: OAuth2.0与QQ 第三方登录

date: 2016-06-04 13:47:01 +0800

tags: [PHP,Oauth,QQ第三方登录]

categories: PHP

---


<a name="80feaa8c"></a>
# 1 什么是OAuth

OAuth is short for open Autnorization.

OAUTH协议为用户资源的授权提供了一个安全的、开放而又简易的标准。与以往的授权方式不同之处是OAUTH的授权不会使第三方触及到用户的帐号信息（如用户名与密码），即第三方无需使用用户的用户名与密码就可以申请获得该用户资源的授权，因此OAUTH是安全的。

**简单说，OAuth 就是一种授权机制。数据的所有者告诉系统，同意授权第三方应用进入系统，获取这些数据。系统从而产生一个短期的进入令牌（token），用来代替密码，供第三方应用使用。**

<a name="7478751c"></a>
# 2 工作原理

<a name="97f4196c"></a>
## 2.1 快递员问题

考虑一种生活的常见场景:我住在一个大型的居民小区。小区有门禁系统.进入的时候需要输入密码。我经常网购和外卖，每天都有快递员来送货。我必须找到一个办法，让快递员通过门禁系统，进入小区。如果我把自己的密码，告诉快递员，他就拥有了与我同样的权限，这样好像不太合适。万一我想取消他进入小区的权力，也很麻烦，我自己的密码也得跟着改了，还得通知其他的快递员。

有没有一种办法，让快递员能够自由进入小区，又不必知道小区居民的密码，而且他的唯一权限就是送货，其他需要密码的场合，他都没有权限？

<a name="d92a4781"></a>
## 2.2 授权机制的设计

于是，我设计了一套授权机制:

第一步，门禁系统的密码输入器下面，增加一个按钮，叫做"获取授权"。快递员需要首先按这个按钮，去申请授权。

第二步，他按下按钮以后，屋主（也就是我）的手机就会跳出对话框：有人正在要求授权。系统还会显示该快递员的姓名、工号和所属的快递公司。

我确认请求属实，就点击按钮，告诉门禁系统，我同意给予他进入小区的授权。

第三步，门禁系统得到我的确认以后，向快递员显示一个进入小区的令牌（access token）。令牌就是类似密码的一串数字，只在短期内（比如七天）有效。

第四步，快递员向门禁系统输入令牌，进入小区。

有人可能会问，为什么不是远程为快递员开门，而要为他单独生成一个令牌？这是因为快递员可能每天都会来送货，第二天他还可以复用这个令牌。另外，有的小区有多重门禁，快递员可以使用同一个令牌通过它们。

<a name="c48ee988"></a>
## 2.3 互联网场景

我们把上面的例子搬到互联网，就是 OAuth 的设计了。

首先，居民小区就是储存用户数据的网络服务。比如，微信储存了我的好友信息，获取这些信息，就必须经过微信的"门禁系统"。

其次，快递员（或者说快递公司）就是第三方应用，想要穿过门禁系统，进入小区。

最后，我就是用户本人，同意授权第三方应用进入小区，获取我的数据。

<a name="dbe15baa"></a>
## 2.4 令牌与密码

令牌（token）与密码（password）的作用是一样的，都可以进入系统，但是有三点差异。

（1）令牌是短期的，到期会自动失效，用户自己无法修改。密码一般长期有效，用户不修改，就不会发生变化。

（2）令牌可以被数据所有者撤销，会立即失效。以上例而言，屋主可以随时取消快递员的令牌。密码一般不允许被他人撤销。

（3）令牌有权限范围（scope），比如只能进小区的二号门。对于网络服务来说，只读令牌就比读写令牌更安全。密码一般是完整权限。

上面这些设计，保证了令牌既可以让第三方应用获得权限，同时又随时可控，不会危及系统安全。这就是 OAuth 2.0 的优点。

注意，只要知道了令牌，就能进入系统。系统一般不会再次确认身份，所以令牌必须保密，泄漏令牌与泄漏密码的后果是一样的。 这也是为什么令牌的有效期，一般都设置得很短的原因。

<a name="cdf88018"></a>
# 3 OAth的应用场景

第三方登录，如qq 微博登录

获取权限后，在符合权限的规则下访问各种api

<a name="960f2f2e"></a>
# 4 授权流程详解

<a name="3e805a26"></a>
## 4.1 三个重要步骤

以使用qq登录为例；

![](https://cdn.nlark.com/yuque/__mermaid_v3/20052b87e6b9dbeaf570a2e172ae5fa7.svg#lake_card_v2=eyJjb2RlIjoiZ3JhcGggTFJcbkFb55So5oi3XS0tPnwyLui-k-WFpXFx6LSm5Y-35ZKM5a-G56CBfEJb6IW-6K6vIHFxIE9hdXRoXVxuQi0tPnwzLui_lOWbnueZu-W9lee7k-aenHxDW-esrOS4ieaWuee9keermV1cbkMtLT58MS7or7fmsYJPYXV0aOeZu-W9lemhtXxCIiwidXJsIjoiaHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlL19fbWVybWFpZF92My8yMDA1MmI4N2U2YjlkYmVhZjU3MGEyZTE3MmFlNWZhNy5zdmciLCJ0eXBlIjoibWVybWFpZCIsImlkIjoiOExWblciLCJjYXJkIjoiZGlhZ3JhbSJ9)
<a name="4a1a8471"></a>
### 1.请求Oauth登录

请求地址:**Request Token Url(未授权的令牌请求服务地址)**，也就是第三方网站请求QQ登录页面事使用的**带有特定参数的URL**。比如:

```
https://graph.qq.com/oauth/show?which=Login&display=pc&client_id=100490398&response_type=code&scope=get_user_info&redirect_uri=http%3A%2F%2Fpassport.mukewang.com%2Fuser%2Ftpcallback%3Freferer%3Dhttp%3A%2F%2Fwww.imooc.com%26tp%3Dqq%26bind%3D0
```


其中，`client_id`就是向腾讯申请的`app_id`，`redirect_uri`是回调地址，这个地址用来处理腾讯发过来的一些消息。

<a name="8dfeffe1"></a>
### 2.输入qq账号和密码登录并授权。

当用户登录成功后，`redirect_uri`在跳转过程中，会带一个加密后的参数code，然后使用php的`$_GET['code']`来获取。由code可以基本确认用户输入的用户名和密码是匹配的。

<a name="a9e74184"></a>
### 3.返回登录结果

为了确保code没有被劫持，需要第三方网站再次请求一个url，即**User Authorization URL：用户授权的令牌请求服务地址**，具体来说就是用户登录qq授权后需要请求的一个带有**特定参数的URL**。地址包含参数： `client_id`, `client_secret` ,`code` 参数(之前qq返回的code)并且code 只能使用一次且有效时间很短的字符串。这部请求之后，会得到一个反馈， 可能是json 或 xml ，包含 昵称、头像 、AccessToken(权限范围)等基本信息

<a name="f8631288"></a>
## 4.2 AccessToken和RefreshToken数据传输原理

用AccessToken参数使用post请求来调用QQ的API。qq验证AccessToken返回消息。

<a name="8d43d727"></a>
## 4.3 AccessToken和RefreshToken生命周期

- Access Token-具有较长的生命周期（10天半个月甚至更长，由个个平台来定）

Access Token过期后，有两种处理方式。一种是重新登录；另一种是在请求**User Authorization URL**(步骤3)的时候带上一个布尔型的参数`need_refersh_token=true`指明在返回结果中携带**Refresh Token-刷新令牌**。在Access Token快过期时，用之重新请求Access Token。一般用户有后台定时任务中，比如每天在qq空间发说说。

- Refresh Token-刷新令牌，起到刷新Access Token的作用(半年或一年甚至更长)

<a name="56ca3b27"></a>
# 5.简单回顾

![](https://cdn.nlark.com/yuque/0/2019/jpeg/352947/1559627314588-ea299c16-c372-440f-ae85-822ac9c4b21d.jpeg#align=left&display=inline&height=284&originHeight=284&originWidth=500&size=0&status=done&width=500)

<a name="d30a6765"></a>
# 6.接入的前置条件，获得appid和appkey等。

获得appid和appkey的方法，可以在qq互联网站进行，这里不再详述。此处使用一个已经获取到的数据来做学习测试:

```php
 <?php
    $this->inc->appid       = '101568914';
		$this->inc->appkey      = 'f19678cceef4ab7929ab51f887927454';
		$this->inc->callback    = 'http://xxxx/QqLogin/login';
		$this->inc->scope       = 'get_user_info';
		$this->inc->errorReport = true;
		$this->inc->storageType = 'file';
```

回调地址是用tp的pathinfo模式，那么我们也来构造一个：

1. 首先是改hosts，让www.laoshixxx.com指向127.0.0.1
1. 模拟tp的pathinfo路由，新建文件如下

```php
<?php
//控制器基类
class Controller
{
    // Path_Info路由需要以下的四个成员来初始化Index首页模板
    private $controller = 'index';
    //默认控制器
    private $method = 'index';
    //默认方法
    private $url_split = '/';
    //路由分隔符
    private $url_suffix = '.html';
    //URL后缀名
    // 获取并自动加载对应的控制器、方法
    public function Curl()
    {
        //解析URL
        $this->Analysis();
        //如果参数C存在则获得控制器名,不存在则加载默认控制器
        $Controller = !empty($_GET['c']) ? $_GET['c'] : $this->controller;
        //获得当前控制器名称
        $Controller .= 'Controller';
        //加上控制器后缀名
        //同上
        $Method = !empty($_GET['m']) ? $_GET['m'] : $this->method;
        //获得当前方法名称
        //自动加载控制器
        $instance = new $Controller();
        //访问对应的操作方法
        $instance->{$Method}();
    }
    //需要用这个方法来解析URL，并对C和M重新赋值
    public function Analysis()
    {
        // 分析PATHINFO信息
        // 注意！！！当隐藏index.php这个入口文件后，直接获取$_SERVER['PATH_INFO']是获取不到的，
        //这时候可以通过$_SERVER['REDIRECT_PATH_INFO']得到path_info信息
        // 摘自tp3的\ThinkPHP\Library\Think\Dispatcher.class.php文件
        if(!isset($_SERVER['PATH_INFO'])) {
            $urlPathInfoFetch ='ORIG_PATH_INFO,REDIRECT_PATH_INFO,REDIRECT_URL';// 用于兼容判断PATH_INFO 参数的SERVER替代变量列表
            $types   =  explode(',',$urlPathInfoFetch);
            foreach ($types as $type){
                if(0===strpos($type,':')) {// 支持函数判断
                    $_SERVER['PATH_INFO'] =   call_user_func(substr($type,1));
                    break;
                }elseif(!empty($_SERVER[$type])) {
                    $_SERVER['PATH_INFO'] = (0 === strpos($_SERVER[$type],$_SERVER['SCRIPT_NAME']))?
                        substr($_SERVER[$type], strlen($_SERVER['SCRIPT_NAME']))   :  $_SERVER[$type];
                    break;
                }
            }
        }

        if (isset($_SERVER['PATH_INFO'])) {
            //$_SERVER['PATH_INFO']URL地址中文件名后的路径信息, 不好理解, 来看看例子
            //比如你现在的URL是 http://www.im158.com/index.php 那么你的$_SERVER['PATH_INFO']就是空的
            //但是如果URL是 http://www.im58.com/index.php/abc/123
            //现在的$_SERVER['PATH_INFO']的值将会是 index.php文件名称后的内容 /abc/123/
            $path = trim($_SERVER['PATH_INFO'], $this->url_split);// 移除两侧的url_split
            //删除最末尾的分隔符
            $paths = explode($this->url_split, $path);
            //将URL分割成数组
            //如果参数C存在则获得控制器名,不存在则加载默认控制器
            $Controller = str_replace('/', '', $paths[0]);
            //获得C参数，并将左侧的/符号删除
            $Method = str_replace($this->url_suffix, '', $paths[1]);
            //获得M参数，并将右侧的伪后缀删除
            //这里对控制器重新赋值
            $_GET['c'] = $Controller;
            //同上
            $_GET['m'] = $Method;
        }
    }
}
//测试控制器-Index
class IndexController
{
    public function Index()
    {
        echo '这是IndexController控制器下的Index方法';
    }
    public function Showlist()
    {
        echo '这是IndexController控制器下的Showlist方法';
    }
}
//测试控制器-Ceshi
class CeshiController
{
    public function Index()
    {
        echo '这是CeshiController控制器下的Index方法';
    }
    public function Showlist()
    {
        echo '这是CeshiController控制器下的Showlist方法';
    }
}
class QqLoginController
{
    public function login()
    {
        echo '这是QqLoginController控制器下的login方法';
    }
}
//实例化控制器
$res = new Controller();
//加载路由监控
$res->curl();
```

3. 新建.htaccess文件，用来开启重定向，隐藏index.php的入口

```
<IfModule mod_rewrite.c>
  Options +FollowSymlinks
  RewriteEngine On

  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteCond %{REQUEST_FILENAME} !-f
#  RewriteRule ^(.*)$ index.php?/$1 [QSA,PT,L]
  RewriteRule ^(.*)$ index.php [L,E=PATH_INFO:$1]
</IfModule>
```

这里要特别注意，当隐藏index.php这个入口文件后，**直接获取$_SERVER['PATH_INFO']是获取不到的，这时候可以通过$_SERVER['REDIRECT_PATH_INFO']得到path_info信息，以下是摘自tp3的\ThinkPHP\Library\Think\Dispatcher.class.php文件**

```php
<?php
if(!isset($_SERVER['PATH_INFO'])) {
            $urlPathInfoFetch ='ORIG_PATH_INFO,REDIRECT_PATH_INFO,REDIRECT_URL';// 用于兼容判断PATH_INFO 参数的SERVER替代变量列表
            $types   =  explode(',',$urlPathInfoFetch);
            foreach ($types as $type){
                if(0===strpos($type,':')) {// 支持函数判断
                    $_SERVER['PATH_INFO'] =   call_user_func(substr($type,1));
                    break;
                }elseif(!empty($_SERVER[$type])) {
                    $_SERVER['PATH_INFO'] = (0 === strpos($_SERVER[$type],$_SERVER['SCRIPT_NAME']))?
                        substr($_SERVER[$type], strlen($_SERVER['SCRIPT_NAME']))   :  $_SERVER[$type];
                    break;
                }
            }
        }
```

<a name="5d83f9f2"></a>
# 7. 下载并使用官方sdk文件

下载地址:[http://wiki.connect.qq.com/sdk下载](http://wiki.connect.qq.com/sdk%E4%B8%8B%E8%BD%BD)

访问sdk目录，和一般网站傻瓜式安装类似，填入appid、appkey、callback、勾选授权列表(一般只勾选get_user_info)，选择开户调试，进行“配置”。对这部分处理的代码如下:

```php
<?php
//检查是不是已配置过
if(file_exists("setted.inc")){
    echo '<meta charset="UTF-8">';
    die("请先删除intall目录下setted.inc文件再进行配置<br /><span style='color:red'>如果已配置成功并发布到外网，请只保留API目录下文件，删除intall目录下和其他文件</span>");
}
if(!function_exists("curl_init")){
    echo "<h1>请先开启curl支持</h1>";
    echo "
        开启php curl函数库的步骤(for windows)<br />
        1).去掉windows/php.ini 文件里;extension=php_curl.dll前面的; /*用 echo phpinfo();查看php.ini的路径*/<br />
        2).把php5/libeay32.dll，ssleay32.dll复制到系统目录windows/下<br />
        3).重启apache<br />
        ";
    exit();
}
if($_POST){

    foreach($_POST as $k => $val){
        if(empty($val)){
            die("请填写$k");
        }
    }
    $_POST['storageType'] = "file";
    $_POST['host'] = "localhost";
    $_POST['user'] = "root";
    $_POST['password'] = "root";
    $_POST['database'] = "test";
    $_POST['scope'] = implode(",",$_POST['scope']);
    $_POST['errorReport'] = (boolean) $_POST['errorReport'];
    $setting = "<?php die('forbidden'); ?>\n";
    $setting .= json_encode($_POST);
    $setting = str_replace("\/", "/",$setting);
    // w+ 读写方式打开，将文件指针指向文件头并将文件大小截为零。如果文件不存在则尝试创建之。
    $incFile = fopen("../API/comm/inc.php","w+") or die("请设置API\comm\inc.php的权限为777");
    if(fwrite($incFile, $setting)){
        echo "<meta charset='utf-8' />";
        echo "配置成功,<a href='../example/'>查看example</a><br /><span style='color:red'>如果已配置成功并发布到外网，请只保留API目录下文件，删除intall目录下和其他文件</span>";

        fclose($incFile);
        fclose(fopen("setted.inc", "w"));
    }else{
        echo "Error";
    }
}else{
    require_once("install.html");
}
```

会将配置信息写入`/API/comm/inc.php`,结果形如:

```php
<?php die('forbidden'); ?>
{"appid":"101568914","appkey":"f19678cceef4ab7929ab51f887927454","callback":"http://www.xxxx.com/QqLogin/login","scope":"get_user_info","errorReport":true,"storageType":"file","host":"localhost","user":"root","password":"root","database":"test"}
```

接着我们就可以利用demo下的文件进行学习测试

<a name="ec53b907"></a>
# 8. sdk文件解读

登录授权三个主要类(api/class/*.class.php)

- Recorder.class.php [配置读写与SESSION存取]
- URL.class.php [基于CURL库的get与post请求]
- Oauth.class.php [Oauth相关URL动态拼接与token操作]

主要方法介绍:

1. Recorder.class.php

```php
<?php
.  __construct() 方法
        $incFileContents = file(ROOT."comm/inc.php");//读取配置文件json串
        $incFileContents = $incFileContents[1];
        $this->inc = json_decode($incFileContents);//解析成php对象
  .  api/comm/inc.php文件内容如下
    {   
        "appid" : 1****156 ,
        "appkey" :  "e1*****f24cc551b6e80bff",
        "callback" : "http://*****.php",
        "scope" : "get_user_info",
        "errorReport" : true,
        ......
    }
. readInc($name) 方法
    return $this->inc->$name;
    //->readInc('appid')既读取配置文件的appid
```

2. URL.class.php

```php
<?php
. combineURL($baseURL, $keysArr) 
        $combined = $baseURL."?"; //拼接？
        $valueArr = array();
        foreach($keysArr as $key => $val){
            $valueArr[] = "$key=$val"; //拼接参数
        }
        $keyStr = implode("&",$valueArr);//使用&拼接参数键值对
        //生成形如http://xxx.com?a=b&c=d......的链接
. get($url, $keysArr) //发送get请求
. post($url, $keysArr, $flag = 0) //发送post请求
```

3. Oauth.class.php

```php
<?php
public function qq_login(){
        $appid = $this->recorder->readInc("appid");
        $callback = $this->recorder->readInc("callback");
        $scope = $this->recorder->readInc("scope");

        //-------生成唯一随机串防CSRF攻击
        $state = md5(uniqid(rand(), TRUE));// 原样返回参数
        $this->recorder->write('state',$state);// state 写入session

        //-------构造请求参数列表
        $keysArr = array(
            "response_type" => "code",
            "client_id" => $appid,
            "redirect_uri" => $callback,
            "state" => $state,
            "scope" => $scope
        );

        $login_url =  $this->urlUtils->combineURL(self::GET_AUTH_CODE_URL, $keysArr);

        header("Location:$login_url");
    }
    
        public function qq_callback(){
        $state = $this->recorder->read("state");

        //--------验证state防止CSRF攻击
        if(!$state || $_GET['state'] != $state){
            $this->error->showError("30001");
        }

        //-------请求参数列表
        $keysArr = array(
            "grant_type" => "authorization_code",
            "client_id" => $this->recorder->readInc("appid"),
            "redirect_uri" => urlencode($this->recorder->readInc("callback")),
            "client_secret" => $this->recorder->readInc("appkey"),
            "code" => $_GET['code']
        );

        //------构造请求access_token的url
        $token_url = $this->urlUtils->combineURL(self::GET_ACCESS_TOKEN_URL, $keysArr);
        $response = $this->urlUtils->get_contents($token_url);

        if(strpos($response, "callback") !== false){

            $lpos = strpos($response, "(");
            $rpos = strrpos($response, ")");
            $response  = substr($response, $lpos + 1, $rpos - $lpos -1);
            $msg = json_decode($response);

            if(isset($msg->error)){
                $this->error->showError($msg->error, $msg->error_description);
            }
        }

        $params = array();
        parse_str($response, $params);

        $this->recorder->write("access_token", $params["access_token"]);
        return $params["access_token"];

    }
```

<a name="3e1860ba"></a>
# 9. sdk优化

为了更好的集成到web项目中，需要对sdk做优化，包含两个方面

1. 调整目录结构

- 删除sdk中api之外的文件(夹)
- 将api/qqConnect.php 和api/comm/config.php整合成一个。

config.php

```php
<?php
define("ROOT",dirname(dirname(__FILE__))."/");
define("CLASS_PATH",ROOT."class/");
```

qqConnect.php

```php
<?php
  session_start();
/* PHP SDK
 * @version 2.0.0
 * @author connect@qq.com
 * @copyright © 2013, Tencent Corporation. All rights reserved.
 */

require_once(dirname(__FILE__)."/comm/config.php");
require_once(CLASS_PATH."QC.class.php");
```

整合如下:

```php
<?php
session_start();
/* PHP SDK
 * @version 2.0.0
 * @author connect@qq.com
 * @copyright © 2013, Tencent Corporation. All rights reserved.
 */

define("ROOT",dirname(__FILE__)."/");
define("CLASS_PATH",QQ_CONNECT_SDK_ROOT."class/");
require_once(CLASS_PATH."QC.class.php");
```

- 删除api/comm/utils.php
- 修改\API\class\Recorder.class.php的构造方法

```php
<?php
public function __construct(){
        $this->error = new ErrorCase();

        //-------读取配置文件
//        $incFileContents = file(ROOT."comm/inc.php");
//        $incFileContents = $incFileContents[1];
//        $this->inc = json_decode($incFileContents); // json转为对象
        // 修改如下 -s
        $this->inc->appid       = '101568914';
        $this->inc->appkey      = 'f19678cceef4ab7929ab51f887927454';
        $this->inc->callback    = 'http://xxxx/QqLogin/login';
        $this->inc->scope       = 'get_user_info';
        $this->inc->errorReport = true;
        $this->inc->storageType = 'file';
        // 修改如下 -e
        if(empty($this->inc)){
            $this->error->showError("20001");
        }

        if(empty($_SESSION['QC_userData'])){
            self::$data = array();
        }else{
            self::$data = $_SESSION['QC_userData'];
        }
    }
```

删除API\comm\inc.php

2. 全文搜索替换,修改常量，避免和项目中的常量冲突。<br />
如下:

```php
<?php
define("QQ_CONNECT_SDK_ROOT",dirname(__FILE__)."/");
define("QQ_CONNECT_SDK_CLASS_PATH",QQ_CONNECT_SDK_ROOT."class/");
require_once(QQ_CONNECT_SDK_CLASS_PATH."QC.class.php");
```

'ROOT'改为'QQ_CONNECT_SDK_ROOT';'CLASS_PATH'改为'QQ_CONNECT_SDK_CLASS_PATH'

具体代码可以参考git仓库(QQLoginDemo)

最后，再总结一下登录的原理:

1、获取用户授权，取得code

2、将code发送到授权服务器获取Access Token

3、通过Access Token调取API接口获取用户信息

> 根据阮一峰博客修改:[http://www.ruanyifeng.com/blog/2019/04/oauth_design.html](http://www.ruanyifeng.com/blog/2019/04/oauth_design.html)
> [https://www.imooc.com/learn/557](https://www.imooc.com/learn/557)  PHP第三方登录—OAuth2.0协议


