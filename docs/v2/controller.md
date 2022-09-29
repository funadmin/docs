## 基类控制器
~~~
fun/auth/Api.php //API接口基类控制器
app/common/controller/Backend.php //后台基类控制器
app/common/controller/Frontend.php //前台基类控制器
app/common/controller/AddonsFrontend .php //插件前台基类控制器
app/common/controller/AddonsBackend.php //插件后台基类控制器
~~~
## Curd类 
> 这个类 里有增删改查方法  index/add/edit/delete/destroy/recycle  等 
> 
> 控制器沒有的方法，会使用这个类里的方法，控制器也可以重写这个类里的方法，控制器Controller优先级比这里高

~~~
app\common\traits\Curd  //Curd 基类类控制器
~~~


## 控制器
- 默认前台控制器 统一继承 Frontend .php
-  默认后台控制器 统一继承 Backend.php
-  插件前台控制器 统一继承 AddonsFrontend .php
- 插件后台控制器 统一继承 AddonsBackend.php

- 例如后台控制器
~~~
    <?php
    /**
    FunAdmin 会员管理
    * ============================================================================
    * 版权所有 2017-2028 FunAdmin，并保留所有权利。
    * 网站地址: http://www.FunAdmin.com
    * ----------------------------------------------------------------------------
    * 采用最新Thinkphp6实现
    * ============================================================================
    * Author: yuege
    * Date: 2020/8/2
    */

    namespace app\backend\controller\member;

    use app\common\controller\Backend;
    use think\facade\Request;
    use think\facade\View;
    use app\backend\model\Member as MemberModel;
    use think\App;

    class Member extends Backend
    {

        /**
        * 关联搜索
        * @var bool 
        */
        protected $relationSearch = true;

        public function __construct(App $app)
        {
            parent::__construct($app);
            $this->modelClass = new MemberModel();
        }

        /**
        * 默认的控制器所继承的父类中有index/add/edit/delete/destroy 等方法
        * 因此在当前控制器中可不用编写增删改查的代码,如果需要自己在这里增加或者修改这里的逻辑
        */

        
    }
~~~

## 属性和方法
- 当我们的控制器继承自以上基类控制器以后，我们就可以使用以下常用属性
~~~
    /**
   * 主键 id
   * @var string
   */
  protected $primaryKey = 'id';
  /**
  * @var
   * 模型
   */
  protected $modelClass;
  /**
   * @var
   * 页面大小
   */
  protected $pageSize;
  /**
   * @var
   * 页数
   */
  protected $page;
  /**
   * 模板布局,
   * @var string|bool
   */
  protected $layout = 'layout/main';
  /**
   * 快速搜索时执行查找的字段
   */
  protected $searchFields = 'id';
  /**
   * 下拉选项条件
   * @var string
   */

  protected $selectMap =[];

  protected $allowModifyFields = [
      'status',
      'sort',
      'title',
      'auth_verify',
  ];
  /**
   * 是否是关联查询
   */
  protected $relationSearch = false;

  /**
   * 关联join搜索
   * @var array
   */
  protected $joinSearch = [];
  
  /**
  * $selectpageFields
  */
  protected $$selectpageFields = ['*'];


## 关联查询

~~~
 
 在控制器设置 $relationSearch 即可
 protected $relationSearch = true;

~~~

~~~
/**
 * 关联join搜索
 * @var array
 */
  protected $joinSearch = [];

我们需要修改控制器的`index`方法，代码如下：


    public function index()
    {
        if ($this->request->isAjax()) {
            list($this->page, $this->pageSize, $sort, $where) = $this->buildParames('',true);
            $count = $this->modelClass
                ->withJoin(['memberGroup','memberLevel'])
                ->where($where)
                ->count();
            $list = $this->modelClass
                ->withJoin(['memberGroup','memberLevel'])
                ->where($where)
                ->order($sort)
                ->page($this->page, $this->pageSize)
                ->select();
            $result = ['code' => 0, 'msg' => lang('Delete Data Success'), 'data' => $list, 'count' => $count];
            return json($result);
        }
        return view();
    }

~~~




## 业务流程

> 增加一个完整示例需要添加以下信息
- 需要添加一个控制器
- 需要添加一个模型( 有時候也可以省略 )
- 添加一个视图页面
- 在后台对应静态文件目录添加一个 `控制器名.js`  （注意js文件名必须小写）修改里面的地址即可


[filename](powered.md ':include')
