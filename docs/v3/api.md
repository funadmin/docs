# FunAdmin API 接口文档

## 接口（一）
- 默认接口
- `config/api.php`  配置 `type`设置为 `simple`
- 以下参数均不生效
- 'driver'        =>'redis',//缓存或数据驱动;//redis//mysql
- 'redisTokenKey'  =>'AccessToken:',//缓存键名
- 'redisRefreshTokenKey'        =>'RefreshAccessToken:',//缓存键名
- 'sign'        =>false,//是否需要签名 //加强安全性

### 一、请求获取token

   -  地址 api/v1.token/build


| 参数      | 说明           | 默认       |
| --------- | -------------- | ---------- |
| username  | 用户名或手机号 | -          |
| password  | 密码           | -          |
| timestamp | 时间戳         | 当前时间戳 |

### 二、请求接口

   - 地址api/v1.member/index


| 参数          | 说明                                                      | 默认            |
| ------------- | --------------------------------------------------------- | --------------- |
| Authorization | 配置中authentication头部参数 Authorization 放到header里面 | 上面获取的token |
| 其他          | 其他post或者get参数                                       | -               |

 -  获取上面的 `access_token` 然后把token放到请求头部,头部参数可以在 `config/api.php`定义

到此接口请求完成

### 三、刷新token

   -  请求地址为 ` api/v1.token/refresh` `参数` `refresh_token`


| 参数          | 说明          | 默认                   |
| ------------- | ------------- | ---------------------- |
| refresh_token | refresh_token | 上面获取的access_token |

## 接口（二）

- 设置type 为 ''
- 以下参数均有效,可自定义
  - 'driver'        =>'redis',//缓存或数据驱动;//redis//mysql
  - 'redisTokenKey'  =>'AccessToken:',//缓存键名
  - 'redisRefreshTokenKey'        =>'RefreshAccessToken:',//缓存键名
  - 'sign'        =>false, //是否需要签名 //加强安全性

### 一、多应用API数据配置

  - 表名: fun_oatuh2_client

 -  1、每个记录对应一个api应用，关键字段appid、appsecret对应应用ID，应用密钥，两者用于后面签名加密生成Authorization使用。

 -  2、目前api的设置暂未有入口，可自行在后台编写配置操作的界面。

### 二 、获取token

- 接口地址 : api/v1.token/build
- 请求方式 Post
- 接口参数

| 参数名    | 参数值        | 注释                    | 是否必须                                |
| --------- |------------|-----------------------| --------------------------------------- |
| username  | admin      | 用户名或邮箱手机号             | 是                                      |
| password  | 123456     | 密码                    | 是                                      |
| appid     |            | auth_client 表appid    | 是                                      |
| appsecret |            | auth_client 表appsecret | 是                                      |
| timestamp | 1663148274 | 当前时间戳                 | 是                                      |
| nonce     | abcds      | 随机数                   | 否，当config.php 配置sign为true 时 必须 |
| sign      |            | 签名                    | 否，当config.php 配置sign为true 时 必须 |


 - sign生成算法:
   - 对以上除sign外的 按key首字母进行排序
   - 对新数组进行http_build_query转url参数形式的字符串  
   - 后进行urldecode编码，最后再转md5小写即生成sign签名

```
$params= [
   'username'=>'username',
   'password'=>'password',
    "appid"=>"appid",
    “appsecret”=>'appsecret',
    “timestamp”=>'timestamp',
    "nonce"=>"随机字符串",
];
ksort($params);
$sign = strtolower(md5(urldecode(http_build_query($params))));
```

- 后台代码如下

```
<?php
  /**
     * 生成签名
     * 字符开头的变量不参与签名
     */
    protected  function buildSign ($data = [])
    {
        unset($data['version']);
        unset($data['sign']);
        ksort($data);
        $data['key'] = $this->app_secret;
        return strtolower(md5(urldecode(http_build_query($data))));
    }
```

 - 请求成功后，将获取的access-token和refresh_token

   - 需要注意的是，在vendor\funadmin\fun-addons\src\auth\Token.php的build中默认查询member数据库，
   - 如果需要自定义查询用户登陆，比如管理员表登陆或者其他表的匹配登陆，可以直接修改源码或者在api的控制器Api.php 修改protect $tableName 

### 三、Api请求

   - 在进行api请求时，header部分提交Authorization Value的值上面获取到的:`access_token`


   - 不需要鉴权的则在  控制器内 noAuth属性 加入不需要鉴权的方法即可 注意 不需要鉴权的 不需要加header

   ```
   $noAuth = ["user"]
   ```

[filename](powered.md ":include")
