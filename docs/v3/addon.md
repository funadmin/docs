## 插件市场1
- 目前FunAdmin官方已经上线插件市场，开发者可以在插件市场下载插件进行离线安装，
- 地址：[https://www.funadmin.com/frontend/plugins.html](https://www.funadmin.com/frontend/plugins.html)
- 如果你开发了一款插件需要上架到FunAdmin的插件市场，请先注册账号，然后进行认证，
- 如果您不同意认证，那么则无法发布插件，认证后如果需要退款可以加群
  [https://jq.qq.com/?_wv=1027&k=3v3nl4HI](https://jq.qq.com/?_wv=1027&k=3v3nl4HI) 联系群主退款

## 插件安装 
- 先下载插件放到addons 目录下，后台刷新缓存，插件就会出现，直接点击安装即可
- 后台管理可以直接卸载和禁用
- 在linux 上请设置插件目录 权限为755    执行命令 chmod -R 755  目录路径

## 插件目录
~~~
├── addonsname                     //插件名字    
│   ├── backend                //后台管理应用模块
│   │   ├── config           //后台配置项目录
│   │   ├── controller       //后台控制器目录
│   │   ├── middleware       //后台中间件目录
│   │   ├── model            //后台模型目录
│   │   ├── service          //后台服务类目录
│   │   ├── traits           //后台trait目录
│   │   ├── view             //后台视图目录
│   ├── frontend                //前台管理应用模块
│   │   ├── config           //前台配置项目录
│   │   ├── controller       //前台控制器目录
│   │   ├── middleware       //前台中间件目录
│   │   ├── model            //前台模型目录
│   │   ├── service          //前台服务类目录
│   │   ├── traits           //前台trait目录
│   │   ├── view             //前台视图目录
│   ├── api                //api管理应用模块
│   │   ├── config           //api配置项目录
│   │   ├── controller       //api控制器目录
│   │   ├── middleware       //api中间件目录
│   │   ├── model            //api模型目录
│   │   ├── service          //api服务类目录
│   │   ├── traits           //apitrait目录
│   ├── view   视图目录
│   ├── config.php  配置文件
│   ├── plugin.php  插件文件
│   ├── plugin.ini  插件信息文件
│   ├── common.php  公共函数文件
│   ├── middleware..php 中间件文件
│   ├── plugin.js. 插件全局js 
│   ├── install.sql
│   ├── uninstall.sql
│   ├── 其他
~~~


[filename](powered.md ':include')
