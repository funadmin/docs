## 强大的表单组件助您快速开发,curd 可以自动生成表单组件
  
  ```
    {:form_input('username','text',['verify'=>'required','tips'=>'Between 4 and 25 characters.'])}
    {:form_input('mobile','text',['verify'=>'phone'])}
    {:form_upload('avatar',$formData,['cropper'=>1])}
    {:form_input('email','text',['verify'=>'email'])}
    {:form_switch('name',$switchList,['verify'=>'required','label'=>'name','multiple'=>1],1)}
    {:form_checkbox('name',$checkboxList,['verify'=>'required','label'=>'name','multiple'=>1],1)}
    {:form_arrays('name',$arrList,['verify'=>'required','label'=>'name'])}
    {:form_textarea('name',['verify'=>'required','label'=>'name'])}
    {:form_select('name',$selectList,['verify'=>'required','label'=>'name','multiple'=>1] ,'id,name')}
    {:form_selectn('city_ids',[],['url'=>__u('member.member/getgroup'),'multiple'=>1,'verify'=>'required'],'id,title',$formData?$formData['city_ids']:'')}
    {:form_radio('sex',['Secrecy','Man','Female'],['filter'=>'sex'],1)}
    {:form_selectplus('sex',['Secrecy','Man','Female'],['filter'=>'sex'],1)}
    {:form_xselect('sex',['Secrecy','Man','Female'],['filter'=>'sex'],1)}
    {:form_date($name=null,$options = [],$value='')}
    {:form_city($name='cityPicker',$id='cityPicker',$options = [])}
    {:form_region($name='regionCheck',$id='regionCheck',$options = [])}
    {:form_tags($id='tags',$name='',$options = [],$value='')}
    {:form_color($id='iconPicker',$name=null,$options = [],$value='')}
   
    {:form_upload($name=null,$formdata=[],$options=[],$value='')}
    {:form_editor($name='container',$id='container',$type=1,$options=[],$value='')}
    {:form_submitbtn()}
    {:form_closebtn($reset = true, $options=[])}
  ```
 
 - 基本覆盖了业务所需的常用的组件，如有好的组件可以联系作者增加
 
### 基础属性
- $name 表单 input | textarea | radio | checkbox 或其他表单的名字
- $options 表单一些基础属性 ，
  - class  css  class类属性
  - label label 显示的值
  - verify验证 常见的可参考layui表单
  - tips 表单下面的提示
  - placeholder 表单显示的文字
  - filter 可见于layui 表单
  - search 是否可搜索 用于select
  - readonly | disabled 表单是否可读或禁止
- $value  表单值
- $select  下拉框的选项
- $attr  下拉框所需属性 比如 `id,title` 表示值为id 显示的文本为title
## form_input输入框

~~~
form_input($name='',$type='text',$options=[],$value=null)
~~~

- ` type` 可选类型 `text`  `hidden`,`password`, 

## form_xmselect 下拉选项
~~~
form_xmselect($name, $select, $options, $attr, $value)
~~~
- name 表单名

- select  下拉选项，

- attr  要显示的属性 比如要显示 id 和 title

- value  默认值

- options
  - 除基础属性外还有下列配置项
  
    ### 配置项
  
    | 参数             | 说明                               | 类型                                                         | 可选值                                                       | 默认值   |
    | :--------------- | :--------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :------- |
    | language         | 语言选择                           | string                                                       | zn / en                                                      | zn       |
    | data             | 显示的数据                         | array                                                        | -                                                            | [ ]      |
    | content          | 自定义下拉框html                   | string                                                       | -                                                            | -        |
    | initValue        | 初始化选中的数据, 需要在data中存在 | array                                                        | -                                                            | null     |
    | tips             | 默认提示, 类似于placeholder        | string                                                       | -                                                            | 请选择   |
    | empty            | 空数据提示                         | string                                                       | -                                                            | 暂无数据 |
    | filterable       | 是否开启搜索                       | boolean                                                      | true / false                                                 | false    |
    | searchTips       | 搜索提示                           | string                                                       | -                                                            | 请选择   |
    | delay            | 搜索延迟 ms                        | int                                                          | -                                                            | 500      |
    | filterMethod     | 搜索回调函数                       | function(val, item, index, prop) val: 当前搜索值, item: 每个option选项, index: 位置数据中的下标, prop: 定义key | -                                                            | -        |
    | filterDone       | 搜索完成函数                       | function(val, list) val: 当前搜索值, list: 过滤后的数据      | -                                                            | -        |
    | remoteSearch     | 是否开启自定义搜索 (远程搜索)      | boolean                                                      | true / false                                                 | false    |
    | remoteMethod     | 自定义搜索回调函数                 | function(val, cb, show, pageIndex) val: 当前搜索值, cb(arr, totalPage): 回调函数, 需要回调一个数组, 结构同data, 远程分页需要第二个参数: 总页码, show: 下拉框显示状态, pageIndex: 分页下当前页码 | -                                                            | -        |
    | direction        | 下拉方向                           | string                                                       | auto / up / down                                             | auto     |
    | style            | 自定义样式                         | object                                                       | -                                                            | { }      |
    | height           | 默认最大高度                       | string                                                       | -                                                            | 200px    |
    | paging           | 是否开启自定义分页                 | boolean                                                      | true / false                                                 | false    |
    | pageSize         | 分页条数                           | int                                                          | -                                                            | 10       |
    | pageEmptyShow    | 分页无数据是否显示                 | boolean                                                      | true / false                                                 | true     |
    | pageRemote       | 是否开启远程分页                   | boolean                                                      | true / false                                                 | true     |
    | radio            | 是否开启单选模式                   | boolean                                                      | true / false                                                 | false    |
    | repeat           | 是否开启重复性模式                 | boolean                                                      | true / false                                                 | false    |
    | clickClose       | 是否点击选项后自动关闭下拉框       | boolean                                                      | true / false                                                 | false    |
    | prop             | 自定义属性名称, 具体看下表         | object                                                       | -                                                            |          |
    | theme            | 主题配置, 具体看下表               | object                                                       | -                                                            |          |
    | model            | 模型, 多选的展示方式, 具体见下表   | object                                                       | -                                                            |          |
    | iconfont         | 自定义选中图标                     | object                                                       | -                                                            |          |
    | show             | 展开下拉的回调                     | function                                                     | -                                                            | -        |
    | hide             | 隐藏下拉的回调                     | function                                                     | -                                                            | -        |
    | template         | 自定义渲染选项                     | function({ item, sels, name, value })                        | -                                                            | -        |
    | on               | 监听选中变化                       | function({ arr, change, isAdd })                             | -                                                            | -        |
    | max              | 设置多选选中上限                   | int                                                          | -                                                            | 0        |
    | maxMethod        | 达到选中上限的回到                 | function(sels, item), sels: 已选中数据, item: 当前选中的值   | -                                                            | -        |
    | name             | 表单提交时的name                   | string                                                       | -                                                            | select   |
    | layVerify        | 表单验证, 同layui的lay-verify      | string                                                       | -                                                            | ''       |
    | layVerType       | 表单验证, 同layui的lay-verType     | string                                                       | -                                                            | ''       |
    | layReqText       | 表单验证, 同layui的lay-reqText     | string                                                       | -                                                            | ''       |
    | toolbar          | 工具条, 具体看下表                 | object                                                       | -                                                            | -        |
    | showCount        | 展示在下拉框中的最多选项数量       | int                                                          | -                                                            | 0        |
    | enableKeyboard   | 是否启用键盘操作选项               | boolean                                                      | true / false                                                 | true     |
    | enableHoverFirst | 是否默认选中第一项                 | boolean                                                      | true / false                                                 | true     |
    | selectedKeyCode  | 选中的键盘KeyCode                  | int                                                          | 全部KeyCode, 也可xmSelect.KeyCode.Enter,xmSelect.KeyCode.Space | 13       |
    | autoRow          | 是否开启自动换行(选项过多时)       | boolean                                                      | true / false                                                 | false    |
    | size             | 尺寸                               | string                                                       | large / medium / small / mini                                | medium   |
    | disabled         | 是否禁用多选                       | boolean                                                      | true / false                                                 | false    |
    | create           | 创建条目                           | function(val, data), val: 搜索的数据, data: 当前下拉数据     | -                                                            | null     |
    | tree             | 树形结构, 具体看下表               | object                                                       | -                                                            | -        |
    | cascader         | 级联结构, 具体看下表               | object                                                       | -                                                            | -        |
    | submitConversion | 配置表单提交数据                   | function(sels, prop), sels: 已选中数据, prop: 自定义的prop   | -                                                            | -        |
    | done             | 渲染完成回调                       | function                                                     | -                                                            | -        |
  
    ### prop
  
    | 参数     | 说明                 | 类型   | 可选值 | 默认值   |
    | :------- | :------------------- | :----- | :----- | :------- |
    | name     | 显示名称             | string | -      | name     |
    | value    | 选中值, 当前多选唯一 | string | -      | value    |
    | selected | 是否选中             | string | -      | selected |
    | disabled | 是否禁用             | string | -      | disabled |
    | children | 分组children         | string | -      | children |
    | optgroup | 分组optgroup         | string | -      | optgroup |
  
    ### 分组说明
  
    如果children属性为数组的时候开启分组模式
  
    ```
    {name: '销售员', children: [
    	{name: '李四', value: 4, selected: true},
    	{name: '王五', value: 5},
    ]},
    
    //可在分组上定义click属性, 来定义点击事件
    {name: '选中', children: [...], click: 'SELECT'},
    {name: '清空', children: [...], click: 'CLEAR'},
    {name: '自动', children: [...], click: 'AUTO'},
    {name: '自定义', children: [...], click: function(item){
    	alert('自定义的, 想干嘛干嘛');
    }},
    ```
  
    ### theme
  
    | 参数     | 说明                 | 类型   | 可选值 | 默认值  |
    | :------- | :------------------- | :----- | :----- | :------ |
    | color    | 主题颜色             | string | -      | #009688 |
    | maxColor | 选中上限闪烁边框颜色 | string | -      | #e54d42 |
    | hover    | 键盘操作的背景色     | string | -      | #f2f2f2 |
  
    ### model
  
    目前仅配置label即可
  
    ```
    model: {
    	//是否展示复选框或者单选框图标 show, hidden:变换背景色
    	icon: 'show',
    	label: {
    		//使用方式
    		type: 'block',
    		//使用字符串拼接的方式
    		text: {
    			//左边拼接的字符
    			left: '',
    			//右边拼接的字符
    			right: '',
    			//中间的分隔符
    			separator: ', ',
    		},
    		//使用方块显示
    		block: {
    			//最大显示数量, 0:不限制
    			showCount: 0,
    			//是否显示删除图标
    			showIcon: true,
    			//自定义渲染label, 默认渲染name, 回调参数(item, sels)
    			template: null,
    		},
    		//自定义文字
    		count: {
    			//函数处理
    			template(data, sels){
    				//data: 所有的数据
    				//sels: 选中的数据
    				return `已选中 ${sels.length} 项, 共 ${data.length} 项`
    			}
    		},
    	},
    	//展示类型, 下拉框形式: absolute, 直接显示模式: relative, 浮动布局: fixed
    	type: 'absolute', 
    },
    ```
  
    ### iconfont
  
    | 参数     | 说明                           | 类型   | 可选值 | 默认值 |
    | :------- | :----------------------------- | :----- | :----- | :----- |
    | select   | 选中图标                       | string | -      | -      |
    | unselect | 非选中图标                     | string | -      | -      |
    | half     | 半选图标                       | string | -      | -      |
    | parent   | 父节点图标, 值为hidden时, 隐藏 | string | -      | -      |
  
    ### toolbar
  
    | 参数     | 说明                                                         | 类型    | 可选值              | 默认值             |
    | :------- | :----------------------------------------------------------- | :------ | :------------------ | :----------------- |
    | show     | 是否展示工具条                                               | boolean | true / false        | false              |
    | showIcon | 是否显示工具图标                                             | boolean | true / false        | true               |
    | list     | 工具条数组 (默认有 全选/清空, 可以自定义), 还有 REVERSE:反选 | array   | ALL, CLEAR, REVERSE | [ "ALL", "CLEAR" ] |
  
    > 自定义方式
  
    ```
    list: [ "ALL", "CLEAR", 
    	{
    		//显示图标, 可以是layui内置的图标, 也可以是自己引入的图标
    		//传入的icon会转化为 <i class="layui-icon layui-icon-face-smile"></i>
    		icon: 'layui-icon layui-icon-face-smile',
    		//显示名称 
    		name: 'xxx',
    		//点击时触发的回调
    		method: function(data){
    			//data 当前页面的数据
    			
    		}
    	} 
    ]
    ```
  
    ### tree
  
    | 参数           | 说明                                              | 类型            | 可选值                                         | 默认值      |
    | :------------- | :------------------------------------------------ | :-------------- | :--------------------------------------------- | :---------- |
    | show           | 是否展示为树状结构                                | boolean         | true / false                                   | false       |
    | showFolderIcon | 是否显示节点前的三角图标                          | boolean         | true / false                                   | true        |
    | showLine       | 是否显示虚线                                      | boolean         | true / false                                   | true        |
    | indent         | 间距                                              | int             | -                                              | 20          |
    | expandedKeys   | 默认展开的节点数组, 为true时展开所有节点          | array / boolean | -                                              | [ ]         |
    | strict         | 是否遵循严格父子结构                              | boolean         | true / false                                   | true        |
    | simple         | 是否开启极简模式                                  | boolean         | true / false                                   | false       |
    | nodeType       | 标注节点类型的key                                 | string          | leaf: 叶子节点, parent: 父节点, half: 半选节点 | __node_type |
    | clickExpand    | 点击节点是否展开, false时点击三角箭头进行展开操作 | boolean         | true / false                                   | true        |
    | clickCheck     | 点击节点是否选中, false时点击复选框进行选中操作   | boolean         | true / false                                   | true        |
  
    ### cascader
  
    | 参数   | 说明                 | 类型    | 可选值       | 默认值 |
    | :----- | :------------------- | :------ | :----------- | :----- |
    | show   | 是否展示为级联结构   | boolean | true / false | false  |
    | indent | 每一级的宽度         | int     | -            | 100    |
    | strict | 是否遵循严格父子结构 | boolean | true / false | true   |
  
    ### 全局方法
  
    | 事件名   | 说明                     | 参数                                                         | 返回值             |
    | :------- | :----------------------- | :----------------------------------------------------------- | :----------------- |
    | render   | 渲染多选                 | (options: 配置项)                                            | 实例对象           |
    | get      | 获取页面中已经渲染的多选 | (filter: 过滤`el`, single: 是否返回单实例)                   | 符合条件的实例数组 |
    | batch    | 批量操作已渲染的多选     | (filter: 过滤`el`, method: 方法, ...方法参数)                | 符合条件的实例数组 |
    | arr2tree | 把列表数据转化为树状结构 | (arr: 数据, pid: 父节点ID的key, id: 对应key, children: 对应key, topParentId: 顶级节点的ID) | 符合条件的数组     |
  
    ```
    //render 使用方式
    xmSelect.render(OPTIONS);
    
    //get 使用方式
    xmSelect.get('#demo1');	 //指定某一个获取
    xmSelect.get(/.*demo1.*/);  //正则获取
    //自定义方法获取
    xmSelect.get(function(el){
    	return el == '#demo1' || el == '#demo2';
    });  
    //单实例
    xmSelect.get('#demo2', true);
    
    //batch 使用方式
    //批量执行禁用
    xmSelect.batch(/.*demo/, 'update', {
    	disabled: true,
    });   
    //批量执行warning
    xmSelect.batch(/.*demo/, 'warning', '#F00', true);   
    ```
  
    ### 实例方法
  
    xmSelect.render()后会返回一个xmSelect对象, 可以进行方法调用
  
    | 事件名             | 说明                                     | 参数                                                         |
    | :----------------- | :--------------------------------------- | :----------------------------------------------------------- |
    | getValue           | 获取当前选中的数据                       | (type: 类型), 可选值: name, nameStr, value, valueStr         |
    | setValue           | 动态设置数据                             | (array: 选中的数据, show: 是否展开下拉,不传默认当前显示状态,取值: true/false, listenOn: 是否触发on的监听, 默认false) |
    | append             | 追加赋值                                 | (array: 追加的数据)                                          |
    | delete             | 删除赋值                                 | (array: 删除的数据)                                          |
    | opened             | 主动展开下拉                             | -                                                            |
    | closed             | 主动关闭下拉                             | -                                                            |
    | reset              | 重置为上一次的render状态                 | -                                                            |
    | update             | 更新多选选中, reset不保留                | (options: 见配置项)                                          |
    | warning            | 警告                                     | (color: 默认同theme.maxColor, sustain: 是否持续显示)         |
    | getTreeValue       | 树节点模式下获取数据, v1.2.0 新增        | (leafOnly: 是否只是叶子节点，默认值为 false, includeHalfChecked: 是否包含半选节点，默认值为 false) |
    | changeExpandedKeys | 树模式下更新节点展开状态, v1.2.0 新增    | (keys: true-全部展开, false-全部关闭, 数组-展开的节点值)     |
    | enable             | 启用选项, disabled=false, v1.2.0 新增    | (array: 想要启用的选项数组)                                  |
    | disable            | 禁用用选项, disabled=true, v1.2.0 新增   | (array: 想要禁用的选项数组)                                  |
    | calcPosition       | fixed布局模式下重新计算位置, v1.2.2 新增 | -                                                            |
  
  
## form_select  下拉组件
~~~
form_select($name = null,$select=[], $options = [],$attr='',$value=null)
~~~
- `name ` 表单名
- `select` 表单列表
- `attr`   表单属性 例如，‘id,title’
- `value`  默认选择的value
-   默认选中value为 'text'的实例：{:form_select('name', $selectList, ['label' => 'Type', 'verify' => 'required'],'')}

## form_selectplus  下拉加强版组件
~~~
form_selectplus($name = null,$select=[], $options = [],$attr='',$value=null)
~~~
- `name ` 表单名
- `select` 表单列表
- `attr`   表单属性 例如，‘id,title’
- `value`  默认选择的value
- `options`  url获取数据url,delimiter 分隔符，multiple 是否多选
-   默认选中value为 'text'的实例：{:form_selectplus($name = null,$select=[], $options = [],$attr='',$value='')}


## form_selectn  级联选择器
~~~
form_selectn($name = null,$select=[], $options = [],$attr='',$value=null)
~~~
- `name ` 表单名
- `select` 表单列表
- `attr`   表单属性 例如，‘id,title’
- `value`  默认选择的value
- `options`  url获取数据url,num 下拉框数量默认3,delimiter 分隔符,search 是否开启搜索
-   默认选中value为 'text'的实例：{:form_selectn($name = null,$select=[], $options = [],$attr='',$value='')}


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
- `type  `  2 =>layeditor  ,  1 => 其他，比如百度，quill  wangEditor jodit ,codemirror等编辑器
- options  基础属性 
  - label label 显示的值
  - verify验证 常见的可参考layui表单
  - tips 表单下面的提示
  - placeholder 表单显示的文字
  - filter 可见于layui 表单
  - search 是否可搜索 用于select
  - readonly | disabled 表单是否可读或禁止
  - 其中 mode 属性用于代码编辑器
  - mode  javascript  text/html  htmlmixed 等

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
- `radiolist` 表单列表 例如 $radiolist = [1=>'开启',2=>'关闭']
- options  基础属性
  - label label 显示的值
  - verify验证 常见的可参考layui表单
  - tips 表单下面的提示
  - placeholder 表单显示的文字
  - filter 可见于layui 表单
  - search 是否可搜索 用于select
  - readonly | disabled 表单是否可读或禁止
- 
## form_checkbox 多选组件
~~~
form_checkbox($name,$list, $option, $value)
~~~
- `name ` 表单名
- `$list` 表单列表 例如 $list = [1=>'开启',2=>'关闭']
- options  基础属性
  - label label 显示的值
  - verify验证 常见的可参考layui表单
  - tips 表单下面的提示
  - placeholder 表单显示的文字
  - filter 可见于layui 表单
  - search 是否可搜索 用于select
  - readonly | disabled 表单是否可读或禁止
  -
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
- `name ` 表单名
- options
    - type 类型 详细请参考layui
    - format 格式 详细请参考layui
    - range 是否范围详细请参考layui
- $value input值

## form_icon 图标组件
~~~
form_icon($name=null,$options = [],$value=null)
~~~
- `name ` 表单名
- $options
  - id  表单id 必须且唯一
  - verify 验证
- $value input值

## form_city城市选择组件
~~~
form_city($name='cityPicker',$id='cityPicker',$options = [])
~~~
- `name ` 表单名  默认cityPicker
- `id ` 表单名  默认cityPicker
- `options `
  - provinceId 省市区id
  - cityId
  - districtId

## form_region区域选择组件
~~~
form_region($name='regionCheck',$id='regionCheck',$options = [])
~~~
- options 同基础属性

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
