```json
{
  "date": "2022.08.01 18:51",
  "tags": ["php"]
}
```

记录一下在php开发中遇到的Bug

1⃣️

```
# [0] InvalidArgumentException in Connection.php line 188

## 未定义数据库类型
```

解决方式

```
数据库加载的问题
protected function initialize(){
  if (ENV == 'dev') {
  	$this->connection = config('database.szb_main');
  }
}
    
```

2⃣️

```
未定义数组索引: electric_account
```

解决方式

```
'list' => $list->toArray()['data']

缺少后续['data'],我也不知道为啥
```

3⃣️

```
前端输入框输入参数，where条件中不显示
```

解决方式

```
原来是逻辑函数中params参数不一致
```

4⃣️

```
后台测试过程中发现能够得到记录，但是搜索条件无法搜索出记录
```

定位问题

```
定位到问题，就是拉下列表中的条件出错，导致无法进行有效搜索
```

解决方式

```
看一下之前的代码，解决好该问题。


未定义变量: allType
出现该错误,就是未定义变量，需要在controller中定义逻辑层的变量

$this->assign("allStatus", ContractOrderLogic::$allStatus);
$this->assign("allType", ContractOrderLogic::$allType);
```

5⃣️

```
控制器不存在:app\admin\controller\PoolMiningControllerController
```

解决方式

```
在html页面内绑定的url上去掉controller
```

6⃣️

```
测试：
1.联合挖矿搜索不出来   可以搜索出
2.渠道唯一标志符和渠道名称搜索不出来  通过打印搜索条件，可以发现type=-1,加入判断去掉该条件，即可查出
```