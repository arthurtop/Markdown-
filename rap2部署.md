## rap2使用

#### 服务

**rap2-delos:** 后端数据API服务器，基于Koa + MySQL

**rap2-dolores:** 前端静态资源，基于React

---

#### 部署

##### 1. rap2-delos

参考README.md文档

https://github.com/thx/rap2-delos

##### 环境要求
- Node.js 8.9.4+
- MySQL 5.7+
- Redis 4.0+

备注：windowns下安装nodejs建议放入系统盘,可以避免在`npm install [package]`发生权限不足的错误

##### 需要配置的文件说明

> src/config/config.dev.ts

```ts
let config: IConfigOptions = {
  serve: {
    port: 2333,// 服务端口号
  },
  db: {
    dialect: 'mysql',
    host: 'localhost',
    port: 3306,
    username: 'root',// 略
    password: '123456',// 略
    database: 'RAP2_DELOS_DEV',// 数据库名
  },
  email: {
    user: '', // 用于发送邮件验证码的账号
    pass: '' // 邮箱第三方授权码
  },
}
```


##### 2. rap2-dolores

###### 需要配置的文件说明

> src/config/config.dev.ts

```ts
module.exports = {
  serve: 'http://127.0.0.1:2333',// 接入后台服务
}

```