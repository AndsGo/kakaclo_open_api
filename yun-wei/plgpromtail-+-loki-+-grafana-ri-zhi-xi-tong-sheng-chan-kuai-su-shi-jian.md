---
description: xulin
---

# 📈 PLG（Promtail + Loki + Grafana）日志系统生产快速实践

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

随着公司业务发展，支撑公司业务的各种系统越来越多，为了保证公司的业务正常发展，急需要对这些线上系统的运行进行监控，做到问题的及时发现和处理，最大程度减少对业务的影响。因此有必要引入一套日志监控系统。

ELK (Elasticsearch 、 Logstash和Kibana) 是功能丰富，允许复杂的操作。但是，这些方案往往规模复杂，**资源占用高**，操作苦难，有点杀鸡用牛刀了。

PLG (Promtail + Loki + Grafana) 轻量级的，**配置要求也不高**（最后有个简单的实验），功能简单，但是目的明确，就是日志采集。

如果是简单进行日志查询，硬件资源不充裕那 PLG 绝对是好选择。

### 1.简介

Promtail： 日志收集的代理，安装部署在需要收集和分析日志的服务器，promtail会将日志发给Loki服务。

Loki： 主服务器，负责存储日志和处理查询。

Grafana：提供web管理界面，数据展示功能。

https://grafana.com/docs/

PLG 官方文档很丰富，大家可以在网络上找到丰富的资料，这里就不多讲解了。

### 2.PLG 安装

Loki: https://grafana.com/docs/loki/latest/installation/

Grafana：https://grafana.com/docs/grafana/latest/setup-grafana/installation/

Promtail：https://grafana.com/docs/loki/latest/clients/promtail/installation/

安装都很简单 这里使用源码安装：

loki 和 promtail 可以到这里下载 https://github.com/grafana/loki/releases/

Grafana 下载地址：https://grafana.com/grafana/download?platform=linux

#### 2.1 loki 安装

下载：

```sh
wget https://github.com/grafana/loki/releases/download/v2.7.1/loki-linux-amd64.zip
```

下载配置：

```shell
wget https://raw.githubusercontent.com/grafana/loki/master/cmd/loki/loki-local-config.yaml
```

解压&启动：

```
unzip loki-linux-amd64.zip
./loki-linux-amd64 --config.file loki-local-config.yaml
```

#### 2.2 promtail 安装

下载：

```shell
wget https://github.com/grafana/loki/releases/download/v2.2.1/promtail-linux-amd64.zip
```

下载配置：

```sh
wget https://raw.githubusercontent.com/grafana/loki/main/clients/cmd/promtail/promtail-local-config.yaml
```

解压&启动：

```
unzip promtail-linux-amd64.zip
./promtail-linux-amd64 --config.file promtail-local-config.yaml
```

#### 2.3 Grafana 安装

下载：

```shell
wget https://dl.grafana.com/enterprise/release/grafana-enterprise-9.3.6.linux-amd64.tar.gz
```

解压&启动：

```shell
tar -zxvf grafana-enterprise-9.3.6.linux-amd64.tar.gz
./grafana-9.3.6/bin/grafana-server
```

经过上面的步骤后就算是安装成功了，接下来讲解下生产环境下我们是怎么使用的。

### 3.生产如何配置

#### 3.1 loki 配置

下面是一般生产上使用的配置，更多详细配置可以参考https://grafana.com/docs/loki/latest/configuration/

```yaml
auth_enabled: false

server:
  http_listen_port: 3100  # http 端口
  grpc_listen_port: 9096

common:
  path_prefix: /data/loki
  storage:
    filesystem:  # loki 存储位置
      chunks_directory: /data/loki/chunks
      rules_directory: /data/loki/rules
  replication_factor: 1
  ring:
    instance_addr: 127.0.0.1
    kvstore:
      store: inmemory

query_range:
  results_cache:
    cache:
      embedded_cache:
        enabled: true
        max_size_mb: 100
compactor:
  working_directory: /data/loki/compactor      # 压缩目录，一般也作为持久化目录
  compaction_interval: 10m                 # 压缩间隔
  retention_enabled: true                  # 持久化开启
  retention_delete_delay: 2h               # 过期后多久删除
  retention_delete_worker_count: 150       # 过期删除协程数目
schema_config:
  configs:
    - from: 2020-10-24
      store: boltdb-shipper
      object_store: filesystem
      schema: v11
      index:
        prefix: index_
        period: 24h  

ruler:
  alertmanager_url: http://localhost:9093
limits_config:
  reject_old_samples: true   # 是否拒绝旧样本
  reject_old_samples_max_age: 168h   # 168小时之前的样本被拒绝

chunk_store_config:
  max_look_back_period: 168h  # 为避免查询超过保留期的数据，必须小于或等于下方的时间值
table_manager:
  retention_deletes_enabled: true   # 保留删除开启
  retention_period: 168h  # 超过168h的块数据将被删除，必须为24h的倍数
```

#### 3.2 promtail 配置

下面以一个简单的例子:

```
LOG [INFO][2023-02-06 17:29:50 +0800] [][reactor-http-epoll-6]  K-Trace-Id:[63e0c88ed5de1c4cc5ace63b],method:POST,url:http://10.0.0.102/api/report/open/buried,body:{"eventTypeId":49,"ip":"10.0.2.55","userId":"10006429","referrer":"http://localhost:8081/","equipment":"pc"} 
```

```yaml
server:
  http_listen_port: 9080
  grpc_listen_port: 0

positions:
  filename: /tmp/positions.yaml

clients:
  - url: http://10.0.0.32:3100/loki/api/v1/push  # 推送到loki地址 
scrape_configs:
- job_name: logs  # 唯一
  static_configs:
  - targets:
      - localhost  # 读取本地文件
    labels: # labels 用户loki labels查询
      job: admin-service
      __path__: /data/logs/admin-service/*/*info.log  # 读取后缀为info.log的日志文件
  - targets:
      - localhost  
    labels: 
      job: gateway-service
      __path__: /data/logs/gateway-service/*/*info.log 
  pipeline_stages:
    - match:
        selector: '{job="admin-service"}' #  job为admin-service可以匹配到
        stages:
        - multiline:
            firstline: '^LOG'  # LOG开头进行多行合并
        - regex:
            expression: '.*(?P<level>INFO|WARN|ERROR).*' # 正则匹配解析 level 
        - timestamp:
            format: RFC3339Nano
            source: timestamp
        - labels:
            timestamp:
            level:  # 将level 作为以一个标签 ,label loki会建立索引，加快查询
    - match:
        selector: '{job="gateway-service"}'
        stages:
        - multiline:
            firstline: '^LOG'  
        - regex:
            expression: '.*(?P<level>INFO|WARN|ERROR).*'
        - timestamp:
            format: RFC3339Nano
            source: timestamp
        - labels:
            timestamp:
            level: 
```

个人使用中觉得 match 下面的自定义 label ，在实际使用中很有用，可以非常方便的进行自定义查询，速度很快。

#### 3.3 Grafana配置

Grafana 无需修改配置文件，而是直接在页面上配置。Grafana 默认端口为 **3000**

http://10.0.0.32:3000/\
10.0.0.32 为你安装Grafana 机器地址&#x20;

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

默认账号和密码 均为 admin。

**1.登录后添加数据源。**

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

选择loki&#x20;

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

**2.配置loki地址**

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

点击 Save & test 完成loki配置&#x20;

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

**3.开始日志查询**

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

**4.常见查询场景**

**1.根据label 查询**

​ 可以查到的label 都在promtail 配置中labels中配置。&#x20;

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

&#x20;​ 这个就表示查询 job 为 kakaclo-gateway-service 的日志。&#x20;

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

&#x20;这个表示 查询 level为 INFO 的日志。&#x20;

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

&#x20;也可以组合起来查询。&#x20;

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

**2.根据内容查询**

一个很常见的场景就是想更具日志中某个内容进行查询，如根据 trace\_id或某个特定的日志内容 进行查询。&#x20;

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

日志查询可以支持很多条件， 具体可以参考https://grafana.com/docs/loki/latest/logql/

### 4.资源消耗测试

测试环境 16G 8核机器，日均日志量300M。&#x20;

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

运行两天，cpu 1.7% ，内存 消耗 16\*0.8% = 0.128G = 131M 。

日志原始文件 420M ,loki 压缩后消耗 26M。

这么看资源消耗还是相当少的，日志压缩率 达到 6.2%。

### 5.Grafana Dashboards

生产环境中不是所有人都拥有 admin权限，但是又想查看对应的日志。这个时间就可以用到 Dashboard，生成Dashboard可以方便只读权限人员查看日志。下面推荐个loki很实用的Dashboard https://grafana.com/grafana/dashboards/13639-logs-app/&#x20;

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

导入后就可以loki数据源就可以用了&#x20;

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

### 5.生产实践的一些建议

#### 1. 日志最好有统一规范

日志统一后方便提取共同的标签 如

```
ACTLOG [INFO][2023-02-13 17:16:02 +0800] [63e9ffd2d5de0bbaf7e4d890][NettyServer-10.0.0.121:8002-3-thread-19] com.happotech.actmgr.motan.service.impl.ActMgrServiceImpl.getAccountInfoThird(ActMg
```

这个可以方便定位日志属于那个系统 ，日志等级，日志时间，日志内容，链路id。如果日志格式不统一，那定位不同系统的问题起来就会很蛋疼。

#### 2. 最好拥有全路径 trace\_id

有了全路径id后查找问题那就是顺藤摸瓜的事，效率相当高

这里具体可以参考：

https://blog.csdn.net/AndCo/article/details/126542050?spm=1001.2014.3001.5502

#### 3. 日志可以输出到统一的目录中

输出到统一的目录中后，日志收集和管理会简单很多。

例如不同的机器可以挂载一个统一的nas盘，把日志都输出到nas盘中，读取日志就变得很简单。 更多文章可以关注 **海鸥技术部落公众号**
