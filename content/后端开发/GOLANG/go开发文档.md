```
{
  "date": "2022.08.09 18:00",
  "tags": ["go"],
  "description":"看了一下go的开发代码，梳理一下整体的开发流程"
}
```

### 开发流程

分析接口，确定入参、出参，确定sql

```json
1.注册路由（是否使用中间件，注册中间件）
2.入参结构体，验证器结构体    
3.控制层   获取入参(断言转换)，调用业务层逻辑，返回数据和状态码
4.业务层   处理入参，sql的go语言映射，返回数据的封装
5.模型层  （返回参数 ，分页参数）
```

#### 断言语法

**示例**

- 在学习golang过程中遇到

```go
1._data := data.(*VerifyCodePhoneRequest)
```

语法，感觉很迷惑，不清楚具体意思,通过查询资料得到解释，记录下，加深记忆

**解释**

- 类型动态转换/查询（只有对接口对象才能执行类型动态转换/查询）[这个可能不太准确]
- 实际上是golang中的类型断言
- 还有另外一种写法：

```go
1._data,ok := data.(*VerifyCodePhoneRequest)
```

表示对data进行断言，如果断言成功，将接口返回给_data,并且ok为真，否则ok为假



### Go的基础语法

我们还可以通过使用`new`关键字对结构体进行实例化，得到的是结构体的地址。 格式如下：

```go
var p2 = new(person)
fmt.Printf("%T\n", p2)     //*main.person
fmt.Printf("p2=%#v\n", p2) //p2=&main.person{name:"", city:"", age:0}
```

从打印的结果中我们可以看出`p2`是一个结构体指针。

需要注意的是在Go语言中支持对结构体指针直接使用`.`来访问结构体的成员。

```go
var p2 = new(person)
p2.name = "小王子"
p2.age = 28
p2.city = "上海"
fmt.Printf("p2=%#v\n", p2) //p2=&main.person{name:"小王子", city:"上海", age:28}
```

**取结构体的地址实例化**

使用`&`对结构体进行取地址操作相当于对该结构体类型进行了一次`new`实例化操作。

```go
p3 := &person{}
fmt.Printf("%T\n", p3)     //*main.person
fmt.Printf("p3=%#v\n", p3) //p3=&main.person{name:"", city:"", age:0}
p3.name = "七米"
p3.age = 30
p3.city = "成都"
fmt.Printf("p3=%#v\n", p3) //p3=&main.person{name:"七米", city:"成都", age:30}
```

p3.name = "七米"其实在底层是(*p3).name = "七米"，这是Go语言帮我们实现的语法糖



```
任意精度的数字计算
加(bcadd),(减bcsub),乘(bcmul),除(bcdiv)
```



```
SQLSTATE[42S02]: Base table or view not found: 1146 Table 'admin02.iwala_google_auth_type' doesn't exist
```



