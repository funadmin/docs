## 访问速度太慢

1、关闭开发模式 ；可以在后台配置中设置 app_debug 为0

2、打包js 进入static 目录  需要安装node
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

[filename](powered.md ':include')
