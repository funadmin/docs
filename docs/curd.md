>FunAdmin`框架以内置快速生成CURD的命令, 包括插件快，普通控制器、视图、模型、JS文件,。使开发者效率得到进一步提升,节约时间回家陪家人。

> 命令行模式不需要加表前缀
## CURD普通模式
- 添加菜单栏  命行后面 加 `-u 1` 即可
-  多数据库切换生成表单 加上 ` --driver fundemo`   fundemo 是 database.php 中配置的驱动 和mySQL 驱动同级别 （此功能为2.3 版本新增）
- jump  `--jump 1`代表已经有的文件则跳过  , 默认为 1 跳过已经创建的文件，  `--jump 0` 则 不跳过直接覆盖已有的文件

~~~
# 生成fun_test表的CURD
php think curd -t test

# 生成fun_test表的CURD, 文件冲突时强制覆盖
php think curd -t test -f 1

# 生成fun_test表的前台模块CURD, 文件冲突时强制覆盖
php think curd -t test -b frontend 

# 强制删除fun_test表的CURD  
php think curd -t test -d 1  -f 1 

# 生成fun_test表的CURD, 控制器在目录demo下的Test.php文件
php think curd -t test  -c demo/test

# 生成fun_test表的CURD, 模型在目录demo下的Test.php文件
php think curd -t test  -m demo/Test

# 生成fun_test表的CURD, 并设置logo字段后缀为图片
php think curd -t test --imageSuffix=logo

# 生成fun_test表的CURD, 并设置忽略image字段
php think curd -t test -g image

# 生成fun_test表的CURD, 并关联fun_test_cate表, 并设置外键为cate_id cate_ids,
php think curd -t test -j test_cate -k cate_id,cate_ids -p id  

# 生成fun_test表的CURD, 并关联fun_test_cate表, 并设置下拉框显示字段
php think curd -t test -j test_cate -k cate_id,cate_ids -p id  --selectFields=name

# 生成fun_test表的CURD, 并设置logo字段后缀为图片
php think curd -t test --imageSuffix=logo
~~~
## CURD插件模式

> 插件模式  只需要在普通模式命令后加 `-a 插件目录名` 即可

## Menu命令
`FunAdmin`框架以内置快速生成Menu的命令, 包括菜单生成和删除

命令行解析
- a  插件模块名 不使用代表默认后台模块，加-a 代表插件后台
- c 控制器目录  如果是插件模式，不需要完整目录
- f  强制模式
- d 删除模式

```
php think menu demo/test 
```





## 表格规范

```
php think menu -c demo/test -a  demo   -f 1 -d 1 



### 系统字段
*   默认`开关`字段：
    *   status
*   默认`忽略`字段：
    *   update_time,creat_time,delete_time
### 以特殊字符结尾的规则
*   默认`编辑器`字段后缀：
    * `editor, content， detail, details, description` 

*   默认`多选`字段后缀：
    * `checkbox` 

*   默认`下拉选项`字段后缀：
    * `select,selects` 

*   默认`开关`字段后缀：
    * `data, state, status, radio` 

*   默认`日期时间字段`字段后缀：
    * `time, date, datetime` 
    
 *   默认`颜色`字段后缀：
     * `color`

*   默认`图片`字段后缀：
    * `image, images,photo,photos,picture,pictures, thumb, thumbs, avatar, avatars`

*   默认`文件`字段后缀：
    *  file, files, path, paths`
### 注释说明

类型和数据可以通过特殊字符进行定义, 例如：`爱好=[0:唱歌,1:跳舞]`, 代表的就是单选框, 数据集合为：`[0:唱歌,1:跳舞]`。

###示例
```
CREATE TABLE`fun_test` (

`id`int(10) UNSIGNED NOTNULL COMMENT 'ID',

`week` enum('monday','tuesday','wednesday') COLLATE utf8mb4_unicode_ci NOTNULLDEFAULT'monday' COMMENT '星期=[monday:星期一,tuesday:星期二,wedensday:星期三]',

`sexdata` enum('male','female','secret') COLLATE utf8mb4_unicode_ci NOTNULLDEFAULT'secret' COMMENT '性别=[male:男,female:女,secret:保密]',



`textarea` mediumtext COLLATE utf8mb4_unicode_ci NOTNULL COMMENT '内容',

`image`varchar(100) COLLATE utf8mb4_unicode_ci NOTNULLDEFAULT'' COMMENT '图片=1',

`images`varchar(255) COLLATE utf8mb4_unicode_ci NOTNULL COMMENT '图片集合=10',

`attach_file`varchar(100) COLLATE utf8mb4_unicode_ci NOTNULLDEFAULT'' COMMENT '附件=1',

`attach_files`int(11) NOTNULL COMMENT '附件=10',

`keywords`varchar(100) COLLATE utf8mb4_unicode_ci NOTNULLDEFAULT'' COMMENT '关键字',

`price`float(10,2) UNSIGNED NOTNULLDEFAULT'0.00' COMMENT '价格',

`startdate`dateDEFAULTNULL COMMENT '开始日期',

`activitytime`datetimeNOTNULL COMMENT '活动时间',

`timestaptime`timestampNOTNULL COMMENT '时间戳',

`year`year(4) NOTNULL COMMENT '年',

`times`timeNOTNULL COMMENT '时间',

`switch`tinyint(1) NOTNULLDEFAULT'1' COMMENT '上架状态=[0:下架,1:正常]',

`open_switch`tinyint(1) NOTNULLDEFAULT'0' COMMENT '开关=[0:OFF,1:ON]',

`teststate`set('1','2','3') COLLATE utf8mb4_unicode_ci NOTNULLDEFAULT'1' COMMENT '复选=[1:选项1,2:选项2,3:选项3]',

`test2state`set('0','1','2') COLLATE utf8mb4_unicode_ci DEFAULT'2' COMMENT '爱好=[0:唱歌,1:跳舞,2:游泳]',

`editor_content` mediumtext COLLATE utf8mb4_unicode_ci COMMENT '富文本',

`description`textCOLLATE utf8mb4_unicode_ci COMMENT '描述',

`test_color`varchar(30) COLLATE utf8mb4_unicode_ci DEFAULTNULL COMMENT '颜色',

`status`tinyint(1) NOTNULLDEFAULT'1' COMMENT '状态=[0:OFF,1:ON]',

`picture`varchar(255) COLLATE utf8mb4_unicode_ci DEFAULTNULL COMMENT '图片'

) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='测试表' ROW_FORMAT=COMPACT;

ALTERTABLE`fun_test`

ADDPRIMARYKEY (`id`) USING BTREE,

ALTERTABLE`fun_test`

MODIFY`id`int(10) UNSIGNED NOTNULL AUTO_INCREMENT COMMENT 'ID', AUTO_INCREMENT=46;

COMMIT;

```

[comment]: <> (![]&#40;images/screenshot_1620373722536.png&#41;)
```

[filename](powered.md ':include')
