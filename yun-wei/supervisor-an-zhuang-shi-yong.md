# 🚑 supervisor安装使用

### 安装

```bash
yum -y install epel-release supervisor
```

### 设置开机自启动

```bash
systemctl enable supervisord
```

### 重启

```shell
systemctl restart supervisord
```

### 配置

在 /etc/supervisord.d 目录下 创建一个 xx.ini

```ini
[program:spug-api]
command = bash /data/spug/spug_api/tools/start-api.sh
autostart = true
stdout_logfile = /data/spug/spug_api/logs/api.log
redirect_stderr = true
```

### 查看状态

```bash
supervisorctl
```

### 常见问题

#### command 不能设置 2>&1 & ，不然会出现 下面的报错

```
Exited too quickly (process log may have details)
```

#### 如果是后台启动的线程可以增加一个守护线程脚本

```bash
#!/bin/bash

# 定义进程名称
PROCESS_NAME="job"

# 无限循环
while true; do
    # 使用pgrep检查名为job的进程是否存在
    if ! pgrep -x "$PROCESS_NAME" > /dev/null; then
        # 如果进程不存在，则执行run.sh脚本
        echo "进程 $PROCESS_NAME 不存在，正在执行 run.sh..."
        ./run.sh
    else
        echo "进程 $PROCESS_NAME 存在，等待5秒后再次检查..."
    fi

    # 休眠5秒
    sleep 5
done
```

### 示例

运行 es

```ini
[program:es]
command = sh /opt/soft/elasticsearch-7.13.3/bin/start.sh
directory = /opt/soft/elasticsearch-7.13.3/bin
user = es
autostart = true
stdout_logfile = /opt/logs/supervisor/es.log
redirect_stderr = true
```

start.sh

```bash
export ES_JAVA_HOME=/opt/jdk-11
export JAVA_HOME=/opt/jdk-11
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
./elasticsearch >>/dev/null
```
