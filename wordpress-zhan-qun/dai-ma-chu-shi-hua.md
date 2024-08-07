---
description: 徐林
---

# 1️ 代码初始化



{% embed url="https://www.bilibili.com/video/BV1fT421v76q/" %}

## 代码实现

### 1.后端环境

项目框架使用 go-zore [https://go-zero.dev/docs/tasks](https://go-zero.dev/docs/tasks)

集成了各种工程实践的 web 和 rpc 框架。含极简的 API 定义和生成工具 goctl，可以根据定义的 api 文件一键生成 Go。可以很大程度上提高开发效率，统一开发结构。

#### 1.1 goctl 安装

```
go install github.com/zeromicro/go-zero/tools/goctl@latest
```

#### 1.2 protoc 安装

通过 `goctl` 可以一键安装 `protoc`，`protoc-gen-go`，`protoc-gen-go-grpc` 相关组件，你可以执行如下命令：

```
goctl env check --install --verbose --force
```

#### 1.3 goswagger 安装

文档 [https://goswagger.io/go-swagger/](https://goswagger.io/go-swagger/)

```
go install github.com/go-swagger/go-swagger/cmd/swagger@latest
```

#### 1.4 初始化station工作区

```
mkdir station && cd  station
go work init # 创建station 工作区
go get -u github.com/zeromicro/go-zero@latest #安装go-zore
```

#### 1.5 初始化 api、rpc、job和pkg项目(在station工作区中)

```
cd station
mkdir api,rpc,job,pkg
cd api && go mod init api && cd ..
cd rpc && go mod init rpc && cd ..
cd job && go mod init job && cd ..
cd pkg && go mod init pkg && cd ..
go work use api rpc job pkg
```

### 2.代码生成

#### api代码生成

进入api目录,创建 station.api文件

```
//基础请求体
type BaseResponse {
    Code    int    `json:"code"`
    Message string `json:"message"`
    Data    string `json:"data"`
}
​
@server(
    group: base
)
service station-api {
    @handler hello
    get /station/api/hello  returns (BaseResponse)
}
```

进入到 api 目录生成 station api 项目

```
goctl api go -api station.api -dir .
​
go mod tidy 
```

#### rpc代码生成

进入rpc，创建station.proto 文件

```
// 声明 proto 语法版本，固定值
syntax = "proto3";
// proto 包名
package station;
// 生成 golang 代码后的包名
option go_package = "example/proto/greet";
// 定义请求体
message SayHelloReq {}
// 定义响应体
message SayHelloResp {}
// 定义 Greet 服务
service Greet {
  // 定义一个 SayHello 一元 rpc 方法，请求体和响应体必填。
  rpc SayHello(SayHelloReq) returns (SayHelloResp);
}
```

生成代码

```
goctl rpc protoc station.proto --go_out=. --go-grpc_out=. --zrpc_out=. -m
​
go mod tidy 
```

#### 生成数据库代码

进入 rpc项目目录,创建 model目录

准备sql，创建station.sql文件

```
CREATE TABLE `station_users` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT COMMENT '主键',
  `name` varchar(64) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '姓名 页面显示',
  `email` varchar(64) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '邮箱',
  `slug` varchar(64) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '用户标识符',
  `username` varchar(64) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '登录名称',
  `password` varchar(64) COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '登录密码',
  `create_time` datetime(3) DEFAULT CURRENT_TIMESTAMP(3) COMMENT '创建时间',
  `update_time` datetime(3) DEFAULT CURRENT_TIMESTAMP(3) ON UPDATE CURRENT_TIMESTAMP(3) COMMENT '修改时间',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uk_slug` (`slug`) USING BTREE,
  UNIQUE KEY `uk_username` (`username`)
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='站点用户表';
```

加上 cache --cache 增加缓存加快查询

```
goctl model mysql ddl --src station.sql --dir . cache --cache
​
go mod tidy 
```

使用goctl 生成的代码逻辑基本都在 logic中

### 3.后端代码联调

#### api 调用 rpc

```
# 在Config.go中增加rpc配置
RpcConf zrpc.RpcClientConf
```

在 station.yaml增加配置

```
RpcConf:
  Target: dns:///127.0.0.1:8080
  Timeout: 10000 #rpc 超时时间
```

在 servicecontext.go 上下文配置

```
# ServiceContext 增加
GreetRpc greet.Greet
# NewServiceContext 方法中增加
GreetRpc: greet.NewGreet(zrpc.MustNewClient(c.RpcConf)),
```

#### rpc配置model ,调用数据库

进入rpc目录: new model 目录

在配置文件中增加数据库配置

```
DB:
 DataSource: root:GHZJsi7tzS@tcp(10.0.0.238:3306)/station?charset=utf8mb4&parseTime=True&loc=Local
```

在 servicecontext.go配置

```
# ServiceContext 增加
StationUsersModel model.StationUsersModel
# NewServiceContext 方法中增加
cnn := sqlx.NewMysql(c.DB.DataSource)
​
StationUsersModel: model.NewStationUsersModel(cnn),
```

#### 生成swagger文档

```
goctl api plugin -plugin goctl-swagger="swagger -filename station.json -host 127.0.0.1:8888" -api station.api -dir .
```

运行swagger

```
 swagger serve --no-open -F=swagger --port 36666 station.json
```

### 编写业务代码

业务代码基本都在logic中编写

### 4.前端代码准备

首先准备node环境，最好使用nvm进行node版本管理

获取 vue-element-plus-admin 源码

```
git clone https://github.com/kailong321200875/vue-element-plus-admin.git
```



这次运行的源码

[https://github.com/AndsGo/station](https://github.com/AndsGo/station)

