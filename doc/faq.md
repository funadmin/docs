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

