# 目录结构
```
├── mocms //插件名字  
│   ├── backend                //后台管理应用模块
│   │   ├── config           //后台配置项目录
│   │   ├── controller       //后台控制器目录
│   │   ├── middleware       //后台中间件目录
│   │   ├── model            //后台模型目录
│   │   ├── service          //后台服务类目录
│   │   ├── traits           //后台trait目录
│   │   ├── view             //后台视图目录
│   ├── frontend                //前台管理应用模块
│   │   ├── config           //前台配置项目录
│   │   ├── controller       //前台控制器目录
│   │   ├── middleware       //前台中间件目录
│   │   ├── model            //前台模型目录
│   │   ├── service          //前台服务类目录
│   │   ├── traits           //前台trait目录
│   │   ├── view             //前台视图目录
│   ├── common                //common管理应用模块
│   │   ├── config           //common配置项目录
│   │   ├── controller       //common控制器目录
│   │   ├── middleware       //common中间件目录
│   │   ├── model            //common模型目录
│   │   ├── service          //common服务类目录
│   │   ├── traits           //common trait目录
│   ├── view   视图目录
│   │   ├── frontend
│   │   │   ├── default  //默认前台视图目录
│   │   ├── backend
│   │   │   ├── index/index.html //前台视图目录
│   ├── config.php  配置文件
│   ├── plugin.php  插件文件
│   ├── plugin.ini  插件信息文件
│   ├── common.php  公共函数文件
│   ├── middleware..php 中间件文件
│   ├── plugin.js. 插件全局js
│   ├── install.sql
│   ├── uninstall.sql
│   ├── 其他
```

# 内置标签

- 标签公共参数 
- data 自定义返回数据名
- where 自定义搜索条件

## template 
  - 模板标签，加载模板 
  - 参数 module  插件模块 file 文件名 
## nav 
  - 导航标签 获取导航全部数据
  - 参数 where,order,cache,data,field
    ```
    {nav order="sort asc"}
      {volist name="data" id="vo"}
       {$vo.url}
       {$vo.catename}
       {$vo.cateflag}
       {$vo.thumb}
       {if $vo.children}
         {volist name="$vo.children" id="v"}
           {$v.url}
           {$v.catename}
         {/volist}
       {/if}
      {/volist}
    {/nav}
    ```
## navlist
  - 导航标签  获取导航列表数据，只有一级 pid 默认为0;
  - where,order,pid,field,cache,data
   ```
    {navlist order="sort asc"}
       {$vo.url}
       {$vo.catename}
       {$vo.cateflag}
       {$vo.thumb}
           {navlist order="sort asc" pid="$vo.id"}
           {$v.url}
           {$v.catename}
           {/navlist}
      {/volist}
    {/navlist}
   ```
## adv
  - 广告标签：用于调用广告管理模块中的各种广告
  - 参数 where,order,pid,id,limit,cache,data
  ```
  {adv pid="1" id="1" data="data"}
  {$vo.title}{$vo.url}
  {/adv}
  ```
## fun
  - 获取各种模型文章数据
  -参数 where,page,limit,topicids,cateid,id,sql,cache,order,page,field,data
   ```
   {fun cateid="2" limit="8" page='1' order="id desc" data="news"}
   {$vo.title}
   {:getBySymbol($vo.thumb)}
   {$vo.description}
   {$vo.url}
   {$vo.title}{$vo.url}
  {/fun}
  ```
## query
  - 万能标签
  - 参数 where,table,sql,field,limit,page,order,cache,data

  ``` 
  {php }$where='FIND_IN_SET('.$siteId.',site_ids)';{/php}                                   
  {query table="addons_mocms_topic" where="$where" order="hits desc" limit='2' data="topicdata"}
  {volist name="topicdata" id="vo"}
  
  {/volist}
  {/query}
  ```
## category
  - 分类标签 获取分类数据
  - 参数 where,field,cateid,pid,order,limit,cache,data
  ```
  {category pid="18" data='solution'}
  {$vo.url}
  {:getBySymbol($vo.thumb)}
  {$vo.cateflag}
  {$vo.title}
  {$vo.description}
  ```
## tags
 - 获取标签
 - 参数 where,order,limit,cache,data
## links
  - 友情链接
  - where,order,limit,cache,data
  ```
  {links id='vo'}
     <a href="{$vo.url}" target="_blank">{$vo.name}</a>
  {/links}
  ``` 
## debris
  - 碎片
  - where,tid,id,order,field,cache,data
  ```html
  {debris id='1'}{$vo.content}{/debris}
  ```
## after
  - 下一篇
  - where,cateid,id,cache,order,data
  ```html
  {after cateid='1' id="2"}{$vo.url}{$vo.title}{/after}
  ```
## front
  - 上一篇
  - where,cateid,id,cache,order,data
  ```html
  {front cateid='1' id="2"}{$vo.url}{$vo.title}{/front}
  ```
# 常用函数
  - 函数列表
##   getSeo
  - 获取seo
  ```
    getSeo($cateid = '',$forumid='')
  ```
## getMember 
  - 获取会员
     ```
    getMember($id,$field='',$cache=true)
    ```
##  getAttach
  - 获取附件 
    ```
    getAttach($ids)
    ```
## getHtmlImages
  - 获取内容图片
    ```
    getHtmlImages($html, $num = 1, $order = 'asc')
    ```
## getBySymbol
  - 获取数据通过分隔符
    ```
    getBySymbol($data,$symbol=',')
    ```
## getHotTags
  - 获取热门标签
    ```
    getHotTags($limit=6,$cache=true,$order='nums desc')
    ```
## getTopic
  - 获取专题信息
    ```
    getTopic($id, $field = '', $newCache = true)
    ```
## getCategory
  - 获取分类
    ```
     getCategory($cateid, $field = '', $newCache = true)
    ```
## getCategorys
  - 获取分类列表
    ```
    getCategorys($cateids, $field = '-', $newCache = true)
    ```
## getChildCategory
  - 获取子分类
    ```
    getChildCategory($cateid, $field = '', $newCache = true)
    ```
## cateStep  
  - 分类导航  
    ``` 
    cateStep($cateid, $symbol = ' > ')
    ```
## getFront
  - 获取上一篇
    ``` 
    getFront($id,$cateid,$where=[],$order = 'id desc',$cache=true)
    ```
## getAfter
  - 获取下一篇
    ```
    getAfter($id, $cateid,$where=[],$order = 'id desc',$cache=true)
    ```
## getLang 
  - 获取语言数据 
    ``` 
    getLang($modelName,$field,$cache=true)
    ```
## getSiteById
    -获取当前站点
    ``` 
     getSiteById($siteId='')
    ```
## getForum
  - 获取文章
    ```  
     getForum($cateid='',$where=[], $limit=6,$order="id desc",$cache=true)
    ```
## buildUrl 
  - 构建url 
    ```
     buildUrl($param,$url);
    ```


