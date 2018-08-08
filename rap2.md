## rap2

#### 为什么要选择 rap2？
##### 1. 轻松编辑和分享
可视化编辑，完善的版本控制，各种格式的导入导出。让前后端约定接口的工作变得十分简单。

##### 2. Mock服务
RAP会自动根据接口文档生成Mock接口，这些接口会自动生成模拟数据，并支持复杂的生成逻辑。

#### 介绍

阿里妈妈前端团队出品的开源接口管理工具RAP第二代


#### 能做什么

这是一个接口管理工具

> - 支持mock.js语法：RAP本身基于mcok.js
> - 支持接口管理：可管理url地址，不同模块分类。
> - 支持团队协作：拥有团队仓库
> - 支持历史修改操作查看：可查看接口修改情况，但不支持操作回溯。
> - 接口共享：不需要重复编写接口
> - 自动化测试：一键测试接口情况
> - JS插件
> - 可以一键导入postman

#### 如何使用

##### 进入主界面后创建新仓库

1. 新建：新建请求参数或响应内容
1. 导入：通过JSON导入参数设置
1. 预览：编辑内容发生改变时，Mock数据也会发生改变

![image](https://upload-images.jianshu.io/upload_images/6095375-5964d852f5023b39.png?imageMogr2/auto-orient/)

##### api的详细接口

![image](https://upload-images.jianshu.io/upload_images/6095375-e7ca01e0da897bcc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

![image](https://upload-images.jianshu.io/upload_images/6095375-ab4d84502815f8d3.png?imageMogr2/auto-orient/)

#### 权限问题

##### 查阅

个人仓库
- 只能有有本人或是该仓库的成员能查阅编辑

团队分有私有和公开
- 公开的类型里面所有的仓库都可以被所有人查阅
- 而设为私有类型，只能是团队成员查阅

##### 编辑

一个仓库加入其它成员后，仓库的所有成员都可以进行修改

---

## restful

#### 简单描述restful是什么

一种软件架构风格、设计风格，而不是标准，只是提供了一组设计原则和约束条件。它主要用于客户端和服务器交互类的软件。

1. 看Url就知道要什么
1. 看http method就知道干什么
1. 看http status code就知道结果如何


#### 使用

##### 版本

将版本号放在HTTP头信息中，但不如放入URL方便和直观。Github采用这种做法。

```
https://api.example.com/v1/
https://api.example.com/v2/
```

##### 路径

路径又称"终点"（endpoint），表示API的具体网址。

在RESTful架构中，每个网址代表一种资源（resource），所以网址中不能有动词，只能有名词，而且所用的名词往往与数据库的表格名对应。一般来说，数据库中的表都是同种记录的"集合"（collection），所以API中的名词也应该使用复数。

举例来说，有一个API提供动物园（zoo）的信息，还包括各种动物和雇员的信息，则它的路径应该设计成下面这样。


```
https://api.example.com/v1/zoos
https://api.example.com/v1/animals
https://api.example.com/v1/employees
```


##### HTTP动词

对于资源的具体操作类型

- GET（SELECT）：从服务器取出资源（一项或多项）。
- POST（CREATE）：在服务器新建一个资源。
- PUT（UPDATE）：在服务器更新资源（客户端提供改变后的完整资源）。
- PATCH（UPDATE）：在服务器更新资源（客户端提供改变的属性）。
- DELETE（DELETE）：从服务器删除资源。
- HEAD : 从服务器获取报头信息（不是资源）

###### 举个栗子

```url
GET /zoos：列出所有动物园
POST /zoos：新建一个动物园
GET /zoos/ID：获取某个指定动物园的信息
PUT /zoos/ID：更新某个指定动物园的信息（提供该动物园的全部信息）
PATCH /zoos/ID：更新某个指定动物园的信息（提供该动物园的部分信息）
DELETE /zoos/ID：删除某个动物园
GET /zoos/ID/animals：列出某个指定动物园的所有动物
DELETE /zoos/ID/animals/ID：删除某个指定动物园的指定动物
```


##### 状态码

服务器向用户返回的状态码和提示信息，常见的有以下一些（方括号中是该状态码对应的HTTP动词）。


状态码 |	响应类别|	原因短语
---|---|---
1xx |   信息性状态码（Informational）   |   服务器正在处理请求
2xx |   成功状态码（Success）           |   请求已正常处理完毕
3xx	|   重定向状态码（Redirection）     |	需要进行额外操作以完成请求
4xx	|   客户端错误状态码（Client Error）|	客户端原因导致服务器无法处理请求
5xx	|   服务器错误状态码（Server Error）|	服务器原因导致处理请求出错


```url
200 OK - [GET]：服务器成功返回用户请求的数据，该操作是幂等的（Idempotent）。
201 CREATED - [POST/PUT/PATCH]：用户新建或修改数据成功。
202 Accepted - [*]：表示一个请求已经进入后台排队（异步任务）
204 NO CONTENT - [DELETE]：用户删除数据成功。
301 Moved Permanently - 永久重定向，表示请求的资源已经永久的搬到了其他位置
302 Found - 临时重定向，表示请求的资源临时搬到了其他位置
400 INVALID REQUEST - [POST/PUT/PATCH]：用户发出的请求有错误，服务器没有进行新建或修改数据的操作，该操作是幂等的。
401 Unauthorized - [*]：表示用户没有权限（令牌、用户名、密码错误）。
403 Forbidden - [*] 表示用户得到授权（与401错误相对），但是访问是被禁止的。
404 NOT FOUND - [*]：用户发出的请求针对的是不存在的记录，服务器没有进行操作，该操作是幂等的。
406 Not Acceptable - [GET]：用户请求的格式不可得（比如用户请求JSON格式，但是只有XML格式）。
410 Gone -[GET]：用户请求的资源被永久删除，且不会再得到的。
422 Unprocesable entity - [POST/PUT/PATCH] 当创建一个对象时，发生一个验证错误。
500 INTERNAL SERVER ERROR - [*]：服务器发生错误，用户将无法判断发出的请求是否成功。
```


#### github api

###### 用户存在的返回值

```http
curl -i https://api.github.com/users/fylder

HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: GitHub.com
Status: 200 OK

{
  "login": "fylder",
  "type": "User",
  "name": "",
  ...
  "created_at": "2014-07-13T13:00:25Z",
  "updated_at": "2018-08-02T01:05:32Z"
}
```

###### 用户不存在的返回值

```http
curl -i https://api.github.com/users/fylder2

HTTP/1.1 404 Not Found
Content-Type: application/json; charset=utf-8
Server: GitHub.com
Status: 404 Not Found

{
  "message": "Not Found",
  "documentation_url": "https://developer.github.com/v3/users/#get-a-single-user"
}
```

