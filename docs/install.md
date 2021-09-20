## 环境要求
* PHP >= 7.2.0  建议7.4或8.0
* Mysql >= 5.5.0 (需支持innodb引擎) 建议5.7及以上
* Apache 或 Nginx
* PDO PHP Extension
* MBstring PHP Extension
* CURL PHP Extension
* Fileinfo PHP Extension

## 安装
*   使用git克隆资源下来
    *  `git clone https://gitee.com/funadmin/funadmin`
    *  `git clone https://github.com/funadmin/funadmin`
    *  github下载慢话,请使用 `https://github.com.cnpmjs.org/funadmin/funadmin.git` 加速下载
    *  进入目录，执行composer install 安装扩展包
    *  将网站入口部署至`public`目录下面（即`funadmin/public`目录下）
    *  修改伪静态配置, 请参考下方伪静态设置。
    *  访问[http://www.yoursite.com/install.php](http://www.yoursite.com/install.php)进行安装
    *  根据图形界面直接安装即可
    *  安装完成后会自动生成安装锁`public/install.lock`, 如需重新安装, 删掉该文件即可。

## 伪静态配置
* Apache
    * 把下面的内容保存为`.htaccess`文件放到应用入口`public`文件的同级目录下
    ~~~
    <IfModule mod_rewrite.c>
    Options +FollowSymlinks -Multiviews
    RewriteEngine On
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^(.*)$ index.php?/$1 [QSA,PT,L]
    </IfModule>
    ~~~

* Nginx
    * 修改nginx.conf 配置文件 加入下面的语句
    ~~~
  location / {
	if (!-e $request_filename){
		rewrite  ^(.*)$  /index.php?s=$1  last;   break;
	}
    }
    ~~~
## 常见问题
*  如果提示`当前权限不足，无法写入配置文件config/database.php`，请检查`database.php`是否可读，还有可能是当前安装程序无法访问父目录，请检查PHP的`open_basedir`配置
*   如果`composer install`失败，请尝试在命令行进行切换配置到国内源，命令如下`composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/`
*  如果使用的宝塔面板，请在软件配置中PHP的禁用函数中，移除`putenv`函数

遇到问题到[社区](https://bbs.funadmin.com/)或QQ群：[775616363](https://jq.qq.com/?_wv=1027&k=RAvbwgRY)反馈

[filename](powered.md ':include')
