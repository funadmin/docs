## 数据库
- 默认使用fun_ 开头， 也可以在安装的时候替换为你需要的 数据库表建议默认设置 delete_time =0  软删除字段  

// 软删除
User::destroy(1);
// 真实删除
User::destroy(1,true);

$user = User::find(1);
// 软删除
$user->delete();
// 真实删除
$user->force()->delete();


默认情况下查询的数据不包含软删除数据，如果需要包含软删除的数据，可以使用下面的方式查询：

User::withTrashed()->find();
User::withTrashed()->select();

如果仅仅需要查询软删除的数据，可以使用：

User::onlyTrashed()->find();
User::onlyTrashed()->select();

恢复被软删除的数据

$user = User::onlyTrashed()->find(1);
$user->restore();
软删除的删除操作仅对模型的删除方法有效，如果直接使用数据库的删除方法则无效，例如下面的方式无效。

$user = new User;
$user->where('id',1)->delete();


[filename](powered.md ':include')
