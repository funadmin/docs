## form_input  输入框

~~~
form_input($name='',$type='text',$options=[],$value=null)
~~~

- ` type` 可选类型 `text`  `hidden`,`password`, 

## form_xmselect 支持tree,
~~~
form_xmselect ()
~~~
## form_select  下拉组件
~~~
form_select($name = null,$select=[], $options = [],$attr='',$value=null)
~~~
﻿
- `name ` 表单名
- `select` 表单列表
- `attr`   表单属性 例如，‘id,title’
- `value`  默认选择的value
  ﻿
  默认选中value为 'text'的实例：{:form_select('type', $msgType, ['label' => 'Type', 'verify' => 'required'],'', 'text')}
## form_textarea 文本域
~~~
form_textarea($name=‘’, $option=[], $value=‘’)
~~~

## form_upload  上传组件
~~~
form_upload($name=null,$formdata=[],$options=[])
~~~

- options  属性
    - `label` label 标签
    - `type`  上传类型  radio 单选文件  checkbox 多选文件
    - `mime` 文件类型  默认 `image`    可选 ‘*’ 全部  ,‘file’ 等 或者 `video,audio,image,zip,office`等
    - `num` 文件数量  默认 1
    - `path`  上传路径
    - `cropper` 开启裁剪功能
        - `width` ,`height`裁剪宽高
        - `mark` 是否有面罩
        - `area` 裁剪区域大小
    - `exts` 文件后缀
    - `size` 最大文件大小
    - `accept` 可接受的文件类型
    - `multiple` 批量选择
    - `select` false 则不开启选择按钮  不填或为true 则默认开启选择

## form_editor  富文本组件
~~~
form_editor($name='container',$id='container',$type=1,$options=[])
~~~

- `name `富文本名
- `id `富文本id
- `type  `  1 =>layeditor  ,  2 => 其他，比如百度，quill  wangEditor jodit ,codemirror等编辑器
- options  基础属性 label  tips   placeholder 等     其中 mode 属性用于代码编辑器
-  mode  javascript  text/html  htmlmixed 等

## form_radio 富文本组件
~~~
form_radio($name=null, $radiolist = null, $options = [],$value='')
~~~

- `name ` 表单名
- `radiolist` 表单列表

## form_switch 开关组件
~~~
form_radio($name=null, $radiolist = null, $options = [],$value='')
~~~

- `name ` 表单名
- `radiolist` 表单列表
- 
## form_checkbox 多选组件
~~~
form_checkbox($name,$list, $option, $value)
~~~

## form_arrays 数组增加删除本组件
~~~
function form_arrays($name, $option, $list=[])
~~~
- 主要用于配置中的属性增加减少


## form_icon 图标组件
~~~
form_icon($name=null,$options = [],$value=null)
~~~


## form_date 图标组件
~~~
form_date ($name=null,$options = [],$value=null)
~~~
- options
    - type 类型 详细请参考layui
    - format 格式 详细请参考layui
    - range 是否范围详细请参考layui

## form_date 图标组件
~~~
form_date ($name=null,$options = [],$value=null)
~~~
- options
    -   type   类型 详细请参考layui
    -  format 格式 详细请参考layui
    -  range 是否范围详细请参考layui


## form_city城市选择组件
~~~
form_city($name='cityPicker',$id='cityPicker',$options = [])
~~~


## form_region区域选择组件
~~~
form_region($name='regionCheck',$id='regionCheck',$options = [])
~~~


## form_tags 标签组件
~~~
form_tags($id='tags',$name='',$options = [],$value='')
~~~


## form_color 颜色选择组件
~~~
form_color($id='iconPicker',$name=null,$options = [],$value='')
~~~

## form_submitbtn 提交按钮组件
~~~
form_submitbtn($reset = true, $options=[])
~~~
- resert 是否有重置按钮
- options
    - show 是否显示


## form_closebtn  关闭按钮组件
~~~
form_closebtn($reset = true, $options=[])
~~~
[filename](powered.md ':include')
