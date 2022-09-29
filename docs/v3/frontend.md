## 前端JS

 > 一个控制器对应一个 js  js 名为控制器名的全小写， 每个js 的方法对应控制器里的方法， 函数名和控制器方法名一致并小写
- js 默认是生产模式 如果需要开启开发模式 ；可以在后台系统/配置中设置 app_debug 为 1 
- 生产模式系統后台的js默认加载的是` require-backend.min.js ` 前台的是` require-frontend.min.js ` ,   `（require-table.js， fun.js， require-form.js ，require-fu.js， require-upload.js ）`这些js 已经压缩到min.js 中了，从而减少系统压力
- 开发模式后台默认加载的是 `require-backend.js` 其中这个js会自动加载 譬如 `require-table.js ,fun.js ,require-form.js ,require-fu.js, require-upload.js` 等
- 打包js 进入static 目录 并使用 `node r.js -o backend-build.js `命令打包后端js 加快浏览速度
- node r.js -o frontend-build.js 打包前台js

 -  
~~~
define(['jquery','table','form'], function ($,Table,Form) {
    let Controller = {
        index: function () {
            Table.init = {
                table_elem: 'list',
                tableId: 'list',
                searchName :'id' ,//搜索的名字 默认不写是ID  
                requests: {
                    modify_url: 'member/modify',  // 请求地址
                    index_url: 'member/index',
                    delete_url: 'member/delete',
                    // add_url: 'member/add',
                    // edit_url: 'member/edit',
                    //下面两个为自定义按钮样式
                    add_full:{
                        type: 'open',//打开弹窗
                        class: 'layui-btn-sm layui-btn-green',//样式，见layui
                        url: 'member.member/add' +location.search,  // 获取当前url?后面的数据 
                        icon: 'layui-icon layui-icon-add',//图标，见layuiicon
                        text: __('Add'),
                        title: __('Add'),//标题及按钮文字
                       // full: 1,
                        width:800,//窗口的大小
                        height:800,
                        extend:'',      // 弹窗按钮可以这样写 extend:"data-btn='false'",//默认不写是‘submit,close’,参数有：submit(只显示提交),close(只显示关闭),false(不显示按钮)

                    },
                    edit_full:{
                        type: 'open',
                        class: 'layui-btn-xs layui-btn-green',
                        url: 'member.member/edit',
                        icon: 'layui-icon layui-icon-edit',
                        text: __('Edit'),
                        title: __('Edit'),
                        // full: 1,
                        width:'1200',
                        height:'800',
                    },
                },
            };
            Table.render({
                elem: '#' + Table.init.table_elem,
                id: Table.init.tableId,
                url: Fun.url(Table.init.requests.index_url),
                init: Table.init,
                search:true,//是否开启搜索 //默认true
                searchFormTpl:'模板id',//是否开启模板表单搜索，默认false, 1.5.0新增
                searchShow:false,//默认不显示搜索表单,true 
                searchInput:true,//默认显示搜索框
                rowDouble:true,//双击事件
                totalRow: false,//汇总行,默认关闭，汇总字段加totalRow:true属性
                toolbar: ['refresh','add_full','delete'],  //toolbar 栏
                cols: [[
                    {checkbox: true,},
                    {field: 'id', title: 'ID', width: 80, sort: true},//field：字段，title：列表标题，sort：排序
                    {field: 'username', title: __('membername'), width: 120,},
                    {field: 'email', title: __('Email'), width: 120,},
                    {field: 'mobile', title: __('mobile'), width: 120,edit: 'text'},
                    {
                        field: 'sex',
                        title: __('Sex'),
                        filter: 'sex',
                        width: 120,
                        search: 'select',  //搜索栏里面为：下拉框组件，区间为：between
                        selectList: {0: __('Secret'), 1: __('Male'), 2: __('Female')},  //搜索栏下拉框里面的选项
                        templet: Table.templet.select,  //下拉框模板解析
                        tips: __('Female')+'|'+  __('Male'),  //表格的内容转换
                    },
                    {
                        field: 'memberLevel.name',
                        title: __('MemberLevel'),
                        width: 120,
                        templet: Table.templet.resolution,  //解析关联模型字段
                    },
                    {field: 'avatar', title: __('Avatar'), width: 120, templet: Table.templet.image},
                    {
                        field: 'status',
                        title: __('Status'),
                        width: 120,
                        search: 'select',
                        selectList: {0: __('Disabled'), 1: __('Enabled')},
                        url:'url地址',//2.2新增 当selectList 为空时可设置url 获取后端url数据
                        tips:__('Enabled')+'|'+__('Disabled'),//开关字段自定义显示文字
                        filter: 'status',
                        templet: Table.templet.switch
                    },
                    {field: 'create_time', title: __('Registertime'), width: 180,search:'range'},//创建时间，时间范围搜索框
                    {field: 'last_login', title: __('Lastlogintime'), width: 180,search:'timerange', templet: Table.templet.time},
                    {
                        minwidth: 250,
                        align: 'center',
                        title: __('Operat'),
                        init: Table.init,
                        templet: Table.templet.operat,        //操作方法模板解析
                        operat: ['edit_full', 'delete'],      //操作按钮
                    }
                ]],
                limits: [10, 15, 20, 25, 50, 100],
                limit: 15,  //默认行数
                page: true, //开启多页
            });
            Table.api.bindEvent(Table.init);
        },
        add:function () {
            Controller.api.bindevent()
        },
        edit:function () {
            Controller.api.bindevent()
        },
        api: {
            bindevent: function () {
                Form.api.bindEvent($('form'))  //监听表单事件
            }
        }

    };
    return Controller;
});
~~~

> index 方法

 requests 参数为 请求参数，
`index_url add_url  edit_url modiry_url，export_url ` 为默认参数只包含url地址
其他url 为自定义
自定义按钮全部参数如下
~~~
        type: 'open',  //事件   open  request  delete  destroy 等
        class: 'layui-btn-sm layui-btn-green',  //layui类
        url: 'member.member/add', //地址
        icon: 'layui-icon layui-icon-add' ,  //图标
        text: __('Add'),  // 文字信息
        title: __('Add'), //标题
       // full: 1, //是否全屏打开 默认没有
        width:800,//宽
        height:800// 高
        node:true, 是否验证节点。默认为true
        extend:    扩展参数 一般为 字符串 或者json 
~~~

## cols参数
* cols字段属性列表
- class: class 类属性
- field：对应返回的数据列
- filter filter属性
- url 当需要远程获取的数据时 用于模板  select tags  selects 等
- saveurl 当需要保存到后端时的url  selects  switch 等
- title：表格标题
- align：对齐方式
- sort：是否排序字段，默认值不显示排序按钮
- width:表格列宽度
- minWidth：列最小宽度，设置width后不生效
- selectList：搜索表单里面的下拉选项
- tips：开关字段显示的文本，格式：tips:__('Enabled')+'|'+__('Disabled')
- edit：编辑字段，修改需要再后台接收此字段更新 
- totalRowText：开启汇总属性后的汇总行文本
- totalRow：是否开启该列的自动合计功能，默认：false
- fixed：固定列，可选值有：*left*、*right*，该列必须设置在最左（left）、最右(right)
- search：搜索表单字段的格式：`between：区间搜索、not between：不在区间内、timerage： 时间范围、select：下拉框,xmSelect 、range：普通时间范围、time：日期时间，不显示在搜索表单直接设置 **search:false,**`
- templet：模板解析，见JS 模板 - 模板解析
- operat：操作选项，模板解析为：templet: Table.templet.operat 时生效
- searchOp 设置搜索条件  默认`%*%`   
- searchTip   搜索placeholder
- searchValue 默认搜索值
- timepickerformat    timepicker 搜索表单日期范围格式  默认 `YYYY-MM-DD HH:mm:ss`
- searchdateformat  搜索表单日期格式   默认 `yyyy-MM-dd HH:mm:ss`
- dateformat 日期值格式化   默认 `yyyy-MM-dd HH:mm:ss`
- extend 扩展属性


-    默认  比如 ：

~~~
  {field: 'username', title: __('membername'), width: 120,},
~~~

- 开关

~~~
{
    field: 'status',
    title: __('Status'),
    width: 120,
    search: 'select', //搜索类型
    selectList: {0: __('Disabled'), 1: __('Enabled')}, //搜索表单下拉选项
    tips:"是|否",   //开关显示文本 ，默认设为selectList 
    filter: 'status', //fiter
    templet: Table.templet.switch  //模板解析，其它解析见下方
},
~~~

-    时间选择  search  可选

`timerage`  时间范围timepicker    `range` 普通时间范围   `time ` 日期时间
~~~
 {
    field: 'last_login',
    title: __('Lastlogintime'), 
    width: 180,
    search:'timerange', 
    templet: Table.templet.time},
~~~

-  关联查询时用到字段解析 字段直接写 关联模型字段`memberLevel.name`
模板选择 `Table.templet.resolution`
~~~
{
        field: 'memberLevel.name',
        title: __('MemberLevel'),
        width: 120,
        templet: Table.templet.resolution
},
~~~

## 模板解析
- `Table.templet.resolution`  //解析关联模型字段
- `Table.templet.image`     //图片/多图片
- `Table.templet.content`  内容
- `Table.templet.text`  text
- `Table.templet.number`  number
- `Table.templet.icon`  图标
- `Table.templet.url`  url地址
- `Table.templet.switch` 开关
- `Table.templet.operat`  操作方法
- `Table.templet.time`  操作方法
- `Table.templet.select`  select 显示一个
- `Table.templet.selects`  select 下拉框
- `Table.templet.tags`  tag
- `Table.templet.dropdown`  dropdown 
- `Table.templet.operat`  operat


格式样板：
~~~
{ field: 'id', title: __('ID'), },
{
field: 'status',
search: 'select',
title: __('Status'),
filter: 'status',
tips: __('enabled') + '|' + __('disabled'),
selectList: {0: __('Disabled'), 1: __('Enabled')},
sort: true,
templet: Table.templet.switch,
width: 100
},
{field:'create_time', title: __('CreateTime'),align: 'center',sort:'sort',width: 170,search: 'timerage',},
{
fixed:right,
width: 180,
align: "center",
title: __("Operat"),
init: Table.init,
templet: Table.templet.operat,
operat: ["edit","destroy","delete"]
},
~~~

## 其他
~~~
Form.api.bindEvent($('form'))  //监听表单事件
监听表单事件，可以不用此公共函数,自己二次开发
~~~  


## 前端权限验证

- 比如按钮需要设置权限 

~~~
<button class="layui-btn layui-btn-sm layui-btn-sm layui-btn-green  {if !auth('member.member/add')}layui-hide{/if}"
data-width="800" data-height="600" data-full="0" data-resize="0"
lay-event="open" data-url="member.member/add"
title="添加"><i class="layui-icon layui-icon-add"></i>添加</button >
~~~

或者
~~~
{if auth('member.member/add')}
<button class="layui-btn layui-btn-sm layui-btn-sm layui-btn-green"
data-width="800" data-height="600" data-full="0" data-resize="0"
lay-event="open" data-url="member.member/add"
title="添加"><i class="layui-icon layui-icon-add"></i>添加</button >
{/if}
~~~


## table事件
默认的事件有
- open  打开弹窗
- request  请求comfirm
- import 导入事件
- export 导出事件
- delete 销毁
- destroy 删除
- refresh  刷新
- tabswitch 选项卡切换事件
- iframe   v1.2.3 新增  打开新的iframe
- dropdown   v2.6 新增  dropdown
> 示例
~~~
add_full:{
    type: 'iframe   ',
    class: 'layui-btn-sm layui-btn-green',
    url: 'member.member/add',
    icon: 'layui-icon layui-icon-add',
    text: __('Add'),
    title: __('Add'),
    // full: 1,
    width:'800',
    height:'600',
extend:'',
},
~~~
也可以自定义事件
~~~
edit_full:{
    type: 'demo', //类型不能和上面冲突
    class: 'layui-btn-xs layui-btn-green',
    url: 'member.member/edit',
    icon: 'layui-icon layui-icon-edit',
    text: __('Edit'),
    title: __('Edit'),
    // full: 1,
    width:'800',
    height:'600',
    extend:'data-callback="demo(可以填写参数)"'
},
~~~
这里自定义的函数要在js 里自己写，会自动调用的
~~~
demo = function(可以填写参数){
    console.log(可以填写参数)
};
~~~

> 注意 extend 里面可以写对象，也可以是字符串  你可以在里面自定义样式或者其他属性


[filename](powered.md ':include')
