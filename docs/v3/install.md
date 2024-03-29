## 支持 
   - star地址 [https://gitee.com/funadmin/funadmin](https://gitee.com/funadmin/funadmin) 
   - star地址 [https://github.com/funadmin/funadmin](https://github.com/funadmin/funadmin) 

![1667014617054](https://user-images.githubusercontent.com/65004113/198809752-907adc57-dd66-4706-b67a-0b19d0ea6f00.jpg)

## 环境要求
* PHP >= 7.4.0  建议7.4或8.0  注意8.1暂不推荐使用 
* Mysql >= 5.7  建议8.0及以上
* Nginx  或 Apache 建议Nginx
* PDO PHP Extension
* MBstring PHP Extension
* CURL PHP Extension
* Fileinfo PHP Extension
* 伪静态配置 
* 设置目录权限 755
* 启用函数 `putenv` `proc_open` 安装composer 扩展时用到 
* 如果是宝塔安装注意权限的问题，否则会提示权限不足
  

## 官网下载
  * 通过官网下载完整包，进行安装
    * [https://www.funadmin.com/frontend/version/index.html](https://www.funadmin.com/frontend/version/index.html)
    *  将网站入口部署至`public`目录下面（即`funadmin/public`目录下）
    *  修改伪静态配置, 请参考下方伪静态设置
	*  访问[http://www.yoursite.com/install.php](http://www.yoursite.com/install.php)进行安装 www.yousite.com 为你配置的域名
	*  根据图形界面直接安装即可
	*  安装完成后会自动生成安装锁`public/install.lock`, 如需重新安装, 删掉该文件即可。



## 命令行安装
  * 通过 Composer 创建项目建议
	* ```composer create-project --prefer-dist funadmin/funadmin funadmin```
	* ``` cd funadmin &&  composer install  ```
	*  将网站入口部署至`public`目录下面（即`funadmin/public`目录下）
	*  修改伪静态配置, 请参考下方伪静态设置
	* 执行命令  ```php think install``` 安装数据库 



## composer安装
* 通过 Composer 创建项目建议
	* ```composer create-project --prefer-dist funadmin/funadmin funadmin```
	* ```cd funadmin && composer install  ```
	*  将网站入口部署至`public`目录下面（即`funadmin/public`目录下）
	*  修改伪静态配置, 请参考下方伪静态设置
	*  访问[http://www.yoursite.com/install.php](http://www.yoursite.com/install.php)进行安装 www.yousite.com 为你配置的域名
	*  根据图形界面直接安装即可
	*  安装完成后会自动生成安装锁`public/install.lock`, 如需重新安装, 删掉该文件即可。

## git安装
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



## 宝塔安装
*   购买服务器，安装宝塔，部署LNMP环境
	*   宝塔安装方法 https://www.bt.cn/bbs/thread-19376-1-1.html
![image](https://user-images.githubusercontent.com/65004113/148901865-a1b206db-e812-474b-807d-cd9ea85fea3a.png)

![image](https://user-images.githubusercontent.com/65004113/148900062-cd7e95d0-26c4-44a4-ba8e-33820a9642e5.png)

![image](https://user-images.githubusercontent.com/65004113/148901084-a6d5db64-2c37-4dd7-9d08-72253182cdb1.png)

![image](https://user-images.githubusercontent.com/65004113/148901160-92070765-b745-475a-b03e-b5de82526fc0.png)

![image](https://user-images.githubusercontent.com/65004113/148901171-4f19eced-f8c2-4a95-98a5-80c771800721.png)

![image](https://user-images.githubusercontent.com/65004113/148901407-4dea4d07-7394-4cc7-9131-f75ed238445a.png)
	



## 伪静态配置
* Nginx
    * 修改nginx.conf 配置文件 加入下面的语句
    ~~~
  location / {
	if (!-e $request_filename){
		rewrite  ^(.*)$  /index.php?s=$1  last;   break;
	}
    }
    ~~~

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
    
    确保已经启用Apache的伪静态，确保目录已经配置好权限,修改配置

    ```
    <VirtualHost *:80>
	    DocumentRoot "/Users/document/myproject/funadmin/public"
	    ServerName funadmin.com 
	    ServerAlias funadmin.com  *.funadmin.com
	    <Directory "/Users/document/myproject/funadmin">
		AllowOverride All
		Options Indexes FollowSymLinks
		Require all granted
	    </Directory>
    </VirtualHost>
	```
    
<VirtualHost *:80>
    DocumentRoot "/Users/Karson/Project/fastadmin/public"
    ServerName fa.com 
    ServerAlias fa.com *.fa.com
    <Directory "/Users/Karson/Project/fastadmin">
        AllowOverride All
        Options Indexes FollowSymLinks
        Require all granted
    </Directory>
</VirtualHost>

## 常见问题
*  如果提示`当前权限不足，无法写入配置文件config/database.php`，请检查`database.php`是否可读，还有可能是当前安装程序无法访问父目录，请检查PHP的`open_basedir`配置
*  如果`composer install`失败，请尝试在命令行进行切换配置到国内源，命令如下`composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/`
*  如果使用的宝塔面板，请在软件配置中PHP的禁用函数中，移除`putenv`函数

遇到问题到[社区](https://bbs.funadmin.com/)或QQ群：[775616363](https://jq.qq.com/?_wv=1027&k=RAvbwgRY)反馈

[filename](powered.md ':include')
