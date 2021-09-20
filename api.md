## FunAdmin API 接口文档
## 一、多应用API数据配置
-    表名: <表前缀>_oatuh2_client
     ![](images/image-20210419120801324.png)

> 1、每个记录对应一个api应用，关键字段appid、appsecret对应应用ID，应用密钥，两者用于后面签名加密生成authentication使用。

> 2、目前api的设置暂未有入口，可自行在后台编写配置操作的界面。

## 二 、access-token 获取
>  1、生成authentication前需要获取access-token，获取access-token方法在Token控制器父类fun\auth\Token中的accessToken方法

[comment]: <> (![]&#40;images/screenshot_1621329748530.png&#41;)

     -在api的路由配置中已经写好了token获取的路由,请无视原注释，访问路径  xxx.com/api/v1/token

```php
//生成access_token，post访问Token类下的token方法
Route::post(':version/token','api/:version.token/accessToken');
Route::post(':version/token/refresh','api/:version.token/refresh');
```
>  2、access-token的获取,对/api/v1/token进行post请求，需要提交的body为json对象，json参数如下:
```
  ·username:用户名

  ·password:原始密码

  ·nonce:随机字符串

  ·timestamp:请求时间戳,与服务器收到请求的时间戳相差超过10秒视为无效时间戳，该时间在 vendor\funadmin\fun-addons\src\auth\Send.php中的$timeDif    定义，相关的过期时间都在这里定义了

  ·appid:对应的appid，如FunAdmin

  ·appsecret:对应appid的appsecret如123456

  ·sign:签名
  
  ```
**`sign生成算法:对以上除sign外的所有属性+ key=appsecret 
按key首字母进行升序排序后，
对新数组进行http_build_query转url参数形式的字符串 
后进行urldecode编码，最后再转md5小写即生成sign签名，PHP代码如下`**
即

```
$params= [
    "appid"=>"XXX"
    “appsecret”=>'xxxxxx'
    "key"=>"xxx"  //等于appsecret
    "nonce"=>"随机字符串"
    "timestamp"=>'时间戳'  
];
sign = strtolower(md5(urldecode(http_build_query($params))));
```
> 后台代码如下
```
<?php
/**
     * 生成签名
     * _字符开头的变量不参与签名
     */
    public static function makeSign ($data = [],$app_secret = '')
    {   
        unset($data['version']);
        unset($data['sign']);
        return self::buildSign($data,$app_secret);
    }

    /**
     * 计算ORDER的MD5签名
     */
    private static function buildSign($params = [] , $app_secret = '') {
        ksort($params);
        $params['key'] = $app_secret;
        return strtolower(md5(urldecode(http_build_query($params))));
    }
```
>  3 .取请求成功后，将获取的access-token和refresh_token,refresh_token用于刷新access-token，参数内包含用户个人信息；

> 需要注意的是，在vendor\funadmin\fun-addons\src\auth\Token.php的accessToken中默认查询member数据库，如果需要自定义查询用户登陆，比如管理员表登陆或者其他表的匹配登陆，可以直接修改源码或者在api的控制器Token.php中，重写父类的getMember自定义查询，推荐后者，前者容易在更新依赖被覆盖‘’**



## 三、authentication的生成

> 1、在进行api请求时，需要先生成authentication用于api请求，authentication鉴权的关键字可以自定义，在api应用下的config文件夹内定义authentication即可   

```php
<?php
return [
    'authentication'=>"authenticationValue"
];
```
     在进行api请求时，header部分提交authenticationValue的值为:uid 鉴权加密字符串，即可，注意中间是空格，uid为登陆用户id。

> 2 、生成authentication

将获取的access-token  ，使用以下格式 

`appid:access-token:uid`

进行base64 生成密文，组成:`uid 密文`，用户api请求 ;注意中间有个空格，uid 登陆用户的id 

通过上面的操作 即可以使用接口获取你想要的数据了，

>  3、不需要鉴权的则在  控制器内 noAuth属性 加入不需要鉴权的方法即可 //例如
 ~~~
$noAuth = [‘user’] 
~~~



## 四、Api请求

对以上生成的鉴权密文，在头部header设置authentication关键字的值为 `uid base64密文` 即可进行api请求，如没有设置关键字，默认为authentication

![](images/image-20210419140002052.png)