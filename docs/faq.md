##  如何在页面引入JS CSS
    - 当你需要使用第三方css  js 的時候，你可以在当前页面使用script 和link引入  js ,css
  
    ~~~
        <link href="xxx.css" />
        <script src="xxx.js"></script>
    ~~~

## 插件安裝失败

- 采用离线安装 
    - 插件管理 ，离线导入压缩包安装 
- 采用手动导入
    - 把压缩文件解压到addons 目录  
    - 导入install.sql （导入前修改__PREFIX__为表前缀）沒有则无需导入 
    - Plugin.php 查看是否有除了 `install uninstall disabled enabled addonsInit ` 外的函数 如果有则需把钩子函数加入到 config/addons.php下  示例如下
    ~~~
    return array (
        'autoload' => true,
        'hooks' => 
        array (
            'bbs' => 
            array (
                0 => 'bbshook',//这里是hooks钩子
            ),
        ),
        'route' => 
            array (
                0 => 
                array (
                'addons' => 'bbs',
                'domain' => 'demobbs',
                'rule' => 
                array (
                    'bbs' => 'bbs/frontend/index/index',
                    'bbs/i/[:id]/[:type]/[:page]' => 'bbs/frontend/bbs/index',
                    'bbs/d/[:id]' => 'bbs/frontend/bbs/detail',
                ),
            ),
            'service' =>array (),
        );
    ~~~

    - Plugin.php 查看是否有$menu 如果有 那么需要将 菜单加入到数据库内 可以在任何地方执行下面代码 安装菜单 执行后清空缓存
    ~~~
        $addonService = app\backend\service\AddonService::instance();
        $name = '插件名';
        $class = get_addons_instance($name);
        // 安装菜单
        $menu = $class->menu;
        if(!empty($menu_config)){
            if(isset($menu_config['is_nav']) && $menu_config['is_nav']==1){
                $pid = 0;
            }else{
                $pid = $addonService->addAddonManager()->id;
            }
            $menu[] = $menu_config['menu'];
            $addonService->addAddonMenu($menu,$pid);
        }
    ~~~

    - Plugin.ini 修改install = 1
    - plugin.js  有这个文件则把文件内容拷贝到require-addons.js 内部
     
    ~~~ 
    define([], function () {  plugin.js内容复制到这里面 }) 
    ~~~
    - 在 `fun_addon` 表内插入一行 插件数据即可  示例如下
    
    ~~~
     INSERT INTO `fun_addon` 

     (`id`, `title`, `name`, `images`, `group`, `description`, `author`, `version`, `require`, `website`, `is_hook`, `status`, `create_time`, `update_time`, `delete_time`) 
     VALUES 
     (NULL, '社区管理系统', 'bbs', '', '', 'bbs社区管理插件', 'yuege', '1', '1', '', '0', '1', '1616400849', '1650286568', '0')
    ~~~
  
 
## 插件访问404 
 - 检查伪静态是否配置 必须配置否则访问不了

## 访问速度太慢

 - 关闭开发模式 ；可以在后台配置中设置 app_debug 为0

 - 打包js 进入static 目录  需要安装node
并使用
```
node r.js -o backend-build.js
```
命令打包压缩后端js 加快浏览速度
```
node r.js -o frontend-build.js
```
打包压缩前台js 

## 如何开启调试模式
*    修改.env  app_debug =true

## 如何开启伪静态
*    nginx
~~~
location / {
            index  index.html index.htm index.php;
            if (!-e $request_filename) {
                rewrite  ^(.*)$  /index.php?s=/$1  last;
                break;
            }
            #autoindex  on;
        }
~~~
## 目录没有权限的问题
* 进入linux控制台 命令 chmod -R 755 '目录文件夹'

## 插件安装没有权限的问题
* 进入linux控制台 命令 chmod -R 755 '目录文件夹'


## 如何关闭弹出窗口的按钮 
* 设置extend:"data-btn=''" 即可
```

add_full:{
                type: 'open',
                class: 'layui-btn-sm layui-btn-green',
                url: 'member.member/add',
                icon: 'layui-icon layui-icon-add',
                text: __('Add'),
                title: __('Add'),
                node:false,//不使用节点权限
                // full: 1,
                width:'800',
                height:'600',
                extend:'data-btn=""'
            },
```

##  composer 安装错误

 * composer依赖包安装中出现这个错误：
 ```
  
            H:\phpstudy_pro\www\funadminv23>composer update

            Warning: Module "openssl" is already loaded in Unknown on line 0
            Loading composer repositories with package information
            Updating dependencies
            Your requirements could not be resolved to an installable set of packages.

              Problem 1
                - Root composer.json requires funadmin/fun-addons ^v4.0, found funadmin/fun-addons[dev-master, v1.0, ..., v1.60, v2.0, ..., v2.8.3, v3.0, ..., v3.5.0]              but it does not match the constraint.

                        

    解决：
    先查看包来源地址，查询命令： composer config -l -g
    
    执行命令： composer config -g repo.packagist composer https://packagist.org
    
    而后composer install完美成功。
    
    也可以尝试使用阿里云的源，并对composer进行升级
    
    composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
    
    composer selfupdate



[filename](powered.md ':include')
