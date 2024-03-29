## 插件结构
~~~
demo  //插件标识
├── app //此文件夹为插件前后台控制器目录 非必须
├── ├──demo //此文件夹为插件控制器目录，安装后就会迁移到app目录下面
├── ├── ├──controller //此文件夹为插件控制器目录，安装后就会迁移到app目录下面
├── ├── ├──model //此文件夹为插件模型目录，安装后就会迁移到app目录下面
├── ├── ├──view //此文件夹为插件视图目录，安装后就会迁移到app目录下面
├── ├── ├──lang //此文件夹为插件语言目录，安装后就会迁移到app目录下面
├── ├── ├──config //此文件夹为配置目录，安装后就会迁移到app目录下面
├── ├── ├──... /其他，安装后就会迁移到app目录下面 和app 应用一致
├── controller //此文件夹为插件控制器目录
├── public        //此文件夹中所有文件会覆盖到根目录的/public文件夹
├── view            //此文件夹为插件视图目录
├── Plugin.php        //此文件为插件核心安装卸载控制器,必需存在
├── LICENSE        //版权文件 
├── config.php    //插件配置文件 必需存在
├── menu.php    //菜单配置文件
├── plugin.js    //此文件为插件JS文件 可选 可以编写全局js
├── plugin.ini        //插件信息文件,用于保存插件基本信息，插件开启状态等,必需存在
└── install.sql    //插件数据库安装文件,此文件仅在插件安装时会进行导入 可选
└── uninstall.sql    //插件数据库卸载文件,此文件仅在插件安装时会进行导入 可选
~~~
## 命名规范
- 小写字母 ，不能有特殊字符 ，且在插件市场上唯一


> 插件内 app  目录即为插件的一个模块 和主目录（app ）下的应用模块完全一样 会把app 目录下面对应的 插件名字的目录移动到app 目录下
- 可以在里面建立模型，验证，等一系列你想做的事
- 例如  app/demo/controller/Index.php 文件  内 index 方法
- 可以直接使用链接访问  域名+/addons/bbs/frontend/index/index   也可以配置路由进行访问



## 插件文件
>  Plugin.php
~~~
<?php
namespace addons\alisms;
// 注意命名空间规范
use fun\Addons;
class Plugin extends Addons    // 需继承fun\Addon类
{
    /**
     * 初始化
     * @return bool
     */
    public function init()
    {
    
    }

    /**
     * /**
     * 插件安装方法
     * @return bool
     */
    public function install()
    {
        return true;
    }
    /**
     * 插件卸载方法
     * @return bool
     */
    public function uninstall()
    {
        return true;
    }

    /**
     * 插件使用方法
     * @return bool
     */
    public function enabled()
    {

        return true;
    }
    /**
     * 插件禁用方法
     * @return bool
     */
    public function disabled()
    {
        return true;
    }
    /**
     * 钩子函数 AddonsInit 默认会执行
     */
    public function AddonsInit($params)
    {
        
    }

    /**
     * hook 函数 在框架中任意位置可以使用
     */
    public function demohook(array $params)
    {
       
    }
}
~~~

## 插件钩子

    -  默认的事件有 `AddonsInit` 加载插件时会默认加载此函数钩子
    -  除了 install uninstall disabled enabled方法  和上面的默认钩子，其他的均为钩子函数
    -  钩子函数可以在任何地方使用 hook('demo',$params = []);

## 插件配置
> config.php`需要返回一个多维数组，例如：
~~~
<?php
/**
 * funadmin
 * ============================================================================
 * 版权所有 2018-2027 funadmin，并保留所有权利。
 * 网站地址: https://www.funadmin.com
 * ----------------------------------------------------------------------------
 * 采用最新Thinkphp6实现
 * ============================================================================
 * Author: yuege
 * Date: 2019/11/7
 */
return [
    'status' => [
        'title' => '启用前台:',
        'type' => 'radio',
        'rule' => 'required',
        'content' => [
            '1' => 'open',
            '0' => 'close'
        ],
        'value' => 1,
        'msg' => '',
        'tips' => '',
        'ok' => '',
    ],
    'config' => [
        'title' => '配置:',
        'type' => 'array',
        'rule' => 'required',
        'content' => ['accessKeyId','accessKeySecret'],
        'value' => [
            'accessKeyId'=>'',
            'accessKeySecret'=>'',
        ],
        'msg' => '必须',
        'tips' => '',
        'ok' => '成功',
    ],
];
~~~


## 插件信息
~~~
name = alisms //标记 和目录名一致
title = 阿里云短信插件  //标题
description = 阿里云短信插件-FunAdmin插件 //简介
status = 1  //状态
install = 0  //是否安装
author = yuege  //作者
requires = 3.0  //需要的框架版本
version = 1.0  //插件般般
website =   //插件演示地址
thumb =  //插件缩略图
url = // 前台地址
publish_time = 2021-03-18  // 发布时间
vendor = 1 //vendor自动加载
~~~

## 插件JS
    - 当需要使用额外的js時候，可以写 ` plugin.js `
   - 插件js 主要包含两个部分 
   - 第一部分为加载js css 文件 第二部分编辑你要的js代码
    ```
    // 第一部分为
    require.config({
        paths: {
            //其他组件
            'xxx': '插件名/plugins/xxx/xxx.min',//JS文件
        },
        shim: {
            'xxx': {
                    deps: [
                        'css!/static/插件名/plugins/ueditor/themes/default/css/ueditor.css',],//依赖Css文件
                },
            },
    });

 // 第二部分为
    require(['form'], function (Form) {
    Form.events.bindevent = function (form) {
        let Editor = {
            init: {
              
                },

            },
            events: {},
            api: {
                xxx: function () {
                    let editor = document.querySelectorAll('*[lay-filter="editor"]')
                    if (editor.length > 0) {
                        require(['xxx'], function (undefined) {
                                //写你的逻辑
                        })
                    }
                },
            },
        };
        return Editor.api.xxx() //调用代码
    }
})
    ```

    
##   内置函数

###   `addons_url`  插件路由
- 用于生成插件路由
- 调用方法
~~~
$url = addons_url('index'); 
~~~

或者在当前插件控制器下面 

~~~
addons_url('index/index');
~~~
### `get_addons_list`  获取插件列表
-  调用方法
~~~
$addonList = get_addons_list();
~~~

### `get_addons_info`  获取插件信息
-  调用方法
~~~
$addoninfo= get_addons_info ('demo'); //参数插件名
~~~
返回的值为Plugin.ini 内的全部参数


### `get_addons_config`  获取插件配置
-  调用方法
~~~
$config= get_addons_config('demo'); //参数插件名
~~~
返回的值为config.php 内的全部参数

### `set_addons_config`  修改配置信息
-  调用方法
~~~
$config= set_addons_config('demo',$arr); //参数插件名
~~~



## 表设计规范
> 插件数据库时最好统一设计规范，因为更好的设计规范能更好的让我们的用户更快速的掌握我们开发者的设计思想。


### 安装数据库 
> 可以直接在phpmyadmin 选择你要导出的表格，导出然后复制到install.sql   替换表前缀为`__PREFIX__`即可
~~~
CREATE TABLE `__PREFIX__addons_bbs_category` (
                                           `id` int(10) UNSIGNED NOT NULL,
                                           `title` varchar(20) DEFAULT NULL COMMENT '类别名称',
                                           `title_alias` varchar(20) DEFAULT NULL COMMENT '别名',
                                           `thumb` varchar(255) DEFAULT NULL COMMENT '缩略图',
                                           `pid` smallint(6) DEFAULT '0' COMMENT '上级ID',
                                           `is_menu` tinyint(1) DEFAULT '0' COMMENT '是否导航显示',
                                           `status` tinyint(1) DEFAULT '1' COMMENT '状态',
                                           `sort` smallint(6) DEFAULT '50' COMMENT '排序',
                                           `intro` varchar(255) DEFAULT NULL COMMENT '分类描述',
                                           `keywords` varchar(30) DEFAULT NULL COMMENT '搜索关键词',
                                           `create_time` int(11) NOT NULL,
                                           `update_time` int(11) DEFAULT '0',
                                           `delete_time` int(11) DEFAULT '0'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='论坛分类表';
~~~

### 卸载数据库
> 在unstall.sql文件里  输入你要删除的表格命令 即可
~~~
drop table if exists `__PREFIX__addons_bbs_category`;
drop table if exists `__PREFIX__addons_bbs_tags`;
~~~




##  全局JS
> plugin.js  默认安装后则启用
~~~
require.config({
// wang编辑器
    paths: {
        //其他组件
        'demo'      : 'demo/plugins/demo/demo.min',  //注意这个目录是public下的目录
    },
    shim: {

    },
});
require(['form'],function (Form){
    Form.events.bindevent = function (form){
        let demo= {
            //你的逻辑
            events: {},
            api: {
              
            },
        };
        return demo.api()
    }
})
~~~
> 全局js 在后台禁用插件后js 则失效


[filename](powered.md ':include')
