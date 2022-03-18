## 前端js模板
- 增强属性适用于 v2.3及以上
~~~
define(['jquery','table','form','tableFilter'], function ($,Table,Form,tableFilter) {
    let Controller = {
        /**
         * 会员等级
         *
         */
        index:function () {
            // 初始化表格参数配置
            Table.init = {
                table_elem: 'list',
                tableId: 'list',
                requests:{
                    modify_url:'member.memberLevel/modify',
                    index_url: 'member.memberLevel/index',
                    add_url: 'member.memberLevel/add',
                    edit_url: 'member.memberLevel/edit',
                    destroy_url: 'member.memberLevel/destroy',
                    delete_url: 'member.memberLevel/delete',
                    recycle_url: 'member.member/recycle',
                    export_url: 'member.member/export',
                }
            };
            //表格过滤搜索示例 
            var tableFilterInit = layui.tableFilter.render({
                elem: '#' + Table.init.table_elem,
                'mode' : 'api',
                'filters' : [
                    {field: 'name', type:'checkbox'},
                    {field: 'amount', type:'input'},
                    {field: 'discount', type:'input'},
                ],
                'done': function(filters){

                }
            });
            Table.render({
                elem: '#' + Table.init.table_elem,
                id: Table.init.tableId,
                url: Fun.url(Table.init.requests.index_url),
                init: Table.init,
                rowDouble:false,
                toolbar: ['refresh','add','destroy','export','recycle'],
                size:'lg',
                cols: [[
                    {checkbox: true, },
                    {field: 'id', title: __('Id'), width: 80, sort: true},
                    //xmSelect 搜索示例
                    {field: 'name', title: __('Levelname'), width: 120, sort: true,filter:'xmSelect',extend:' data-url="member.memberLevel/index" data-tree="false" data-autorow="false" data-prop="name,name"'},
                    {field: 'thumb', title: __('thumb'), width: 120, sort: true, templet: Table.templet.image},
                    {field: 'amount', title: __('Levelmoney'), width: 150, sort: true},
                    {field: 'discount', title: __('Leveldiscount'), width: 180, sort: true},
                    {field: 'description', title: __('Leveldesc'), width: 150, sort: true},
                    {
                        field: 'status', title: __('Status'), width: 180, search: 'select',
                        selectList: {0: __('Disabled'), 1: __('Enabled')},
                        filter: 'status',
                        templet: Table.templet.switch
                    },
                    {field: 'create_time', title: __('Createtime'), width: 180,search: 'range'},
                    {field: 'update_time', title: __('Updatetime'), width: 180,search: false},
                    {
                        minwidth: 250,
                        align: 'center',
                        title: '操作',
                        init: Table.init,
                        templet: Table.templet.operat,
                        operat: ['edit', 'destroy',]
                    }
                ]],
                done: function(res, curr, count){
                    tableFilterInit.reload()
                },
                limits: [10, 15, 20, 25, 50, 100],
                limit: 15,
                page: true
            });
            let table = $("#"+ Table.init.table_elem);
            Table.api.bindEvent(table);
        },
        add:function () {
            Controller.api.bindevent();
        },
        edit:function () {
            Controller.api.bindevent();
        },
        recycle:function () {
            // 初始化表格参数配置
            Table.init = {
                table_elem: 'list',
                tableId: 'list',
                requests: {
                    recycle_url: 'member.member/recycle',
                    restore_url: 'member.member/restore',
                    delete_url: 'member.member/delete',
                },
            };
            Table.render({
                elem: '#' + Table.init.table_elem,
                id: Table.init.tableId,
                url: Fun.url(Table.init.requests.index_url),
                init: Table.init,
                toolbar: ['refresh','delete','restore'],
                cols: [[
                    {checkbox: true, },
                    {field: 'id', title: __('Id'), width: 80, sort: true},
                    {field: 'name', title: __('Levelname'), width: 120, sort: true},
                    {field: 'amount', title: __('Levelmoney'), width: 150, sort: true},
                    {field: 'discount', title: __('Leveldiscount'), width: 180, sort: true},
                    {field: 'description', title: __('Leveldesc'), width: 150, sort: true},
                    {
                        field: 'status', title: __('Status'), width: 180, search: 'select',
                        selectList: {0: __('Disabled'), 1: __('Enabled')},
                        filter: 'status',
                        templet: Table.templet.switch
                    },
                    {field: 'create_time', title: __('Createtime'), width: 180,search: false},
                    {field: 'update_time', title: __('Updatetime'), width: 180,search: false},
                    {
                        minwidth: 250,
                        align: 'center',
                        title: '操作',
                        init: Table.init,
                        templet: Table.templet.operat,
                        operat: ['restore', 'delete']
                    }
                ]],
                limits: [10, 15, 20, 25, 50, 100],
                limit: 15,
                page: true
            });
            let table = $("#"+ Table.init.table_elem);
            Table.api.bindEvent(table);
        },

        api: {
            bindevent: function () {
                Form.api.bindEvent()
            }
        }
    };
    return Controller;
});
~~~

## cols参数
* cols字段属性列表
- class: class 类属性
- field：对应返回的数据列
- filter filter属性
- url 当需要远程获取的数据时 用于模板  select tags  selects 等
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
- search：搜索表单字段的格式：`between：区间搜索、not between：不在区间内、timerage： 时间范围、select：下拉框、range：普通时间范围、time：日期时间，不显示在搜索表单直接设置 **search:false,**`
- templet：模板解析，见JS 模板 - 模板解析
- operat：操作选项，模板解析为：templet: Table.templet.operat 时生效
- searchOp 设置搜索条件  默认`%*%`
- searchTip   搜索placeholder
- searchValue 默认搜索值
- timepickerformat    timepicker 搜索表单日期范围格式  默认 `YYYY-MM-DD HH:mm:ss`
- searchdateformat  搜索表单日期格式   默认 `yyyy-MM-dd HH:mm:ss`
- dateformat 日期值格式化   默认 `yyyy-MM-dd HH:mm:ss`
- extend 扩展属性

[filename](powered.md ':include')
