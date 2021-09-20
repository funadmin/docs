## 系统架构
~~~
FunAdmin项目目录
├── addons                     //插件存放目录
├── app                        //应用目录
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
│   │   ├── view             //api视图目录
│   ├── common                //通用应用模块
│   ├── BaseController.php    //控制器基础类
│   ├── common.php            //应用公共文件
│   ├── event.php             //事件定义文件
│   ├── ExceptionHandle.php   //应用异常处理类
│   ├── middleware.php        //全局中间件定义文件
│   ├── provider.php          //容器Provider定义文件
│   ├── Request.php           //应用请求对象类
├── config                     //配置项目录
├── extend                        //其他扩展目录  
├── public
│   ├── install           //安装静态资源目录  
│   │   ├──css           //后台静态资源
│   ├── static
│   │   ├── backend           //后台静态资源
│   │   │    ├── css        //后台自义定CSS
│   │   │    ├── fonts      //后台自义定字体
│   │   │    ├── images     //后台相关图片资源
│   │   │    ├── js         //后台js, 与后台控制器是一一对应的
│   │   ├── common           //公共资源
│   │   ├── plugins            //插件资源
│   └── storage               //上传文件目录
│   ├── index.php             //应用入口主文件
│   ├── install.php             //应用安装文件
│   └── router.php
├── route                      //路由目录  
├── runtime                    //缓存目录    
├── vendor                     //Compposer资源包位置
├── view
│   │   ├── index    //前台视图页面
├── LICENSE
├── README.md
├── build.php                    
├── composer.json              //Composer包配置
└── think
~~~


[filename](powered.md ':include')
