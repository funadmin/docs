## 插件市场
- 目前FunAdmin官方已经上线插件市场，开发者可以在插件市场下载插件进行离线安装，
- 地址：[https://www.funadmin.com/frontend/plugins.html](https://www.funadmin.com/frontend/plugins.html)
- 如果你开发了一款插件需要上架到FunAdmin的插件市场，请先注册账号，然后进行认证，
- 如果您不同意认证，那么则无法发布插件，认证后如果需要退款可以加群
  [https://jq.qq.com/?_wv=1027&k=3v3nl4HI](https://jq.qq.com/?_wv=1027&k=3v3nl4HI) 联系群主退款

## 插件安装 
- 先下载插件放到addons 目录下，后台刷新缓存，插件就会出现，直接点击安装即可
- 后台管理可以直接卸载和禁用
- 在linux 上请设置插件目录 权限为755    执行命令 chmod -R 755  目录路径


##  插件开发

  - 插件分为一般插件 和应用插件
  - 一般插件可以不用app目录
  - 应用插件 ，包含app 目录 且目录结构和app下的应用结构一样
  - 需要注意的一点，如果包含后台管理文件，控制器需要设置一下layout路径     `protected $layout = '../../backend/view/layout/main';`
  - 前台模板可以设置  `protected $layout = false` 或者  `protected $layout = '../../frontend/view/layout/main';`
  - 

## 插件目录
~~~
├── addonsname                     //插件名字    
│   ├── app  
│   │   ├── addonsname           //插件名字 目录结构和app 下面的应用一样
│   │   ├──├── config           //配置项目录
│   │   ├──├── controller       //控制器目录
│   │   ├──├──├── v1       //v1目录
│   │   ├──├──├── v2       //v2目录
│   │   ├──├──├── backend       //v2目录
│   │   ├──├──├── api       //v2目录
│   │   ├──├──├── ...       
│   │   ├──├── middleware       //中间件目录
│   │   ├──├── model            //模型目录
│   │   ├──├── service          //服务类目录
│   │   ├──├── view             //视图目录
│   ├── controller   插件控制器目录
│   ├── view   插件视图目录
│   ├── config.php  配置文件
│   ├── Plugin.php  插件文件
│   ├── plugin.ini  插件信息文件
│   ├── menu.php    菜单
│   ├── plugin.js. 插件全局js 
│   ├── install.sql
│   ├── uninstall.sql
│   ├── service.ini  插件服务文件
~~~


[filename](powered.md ':include')
