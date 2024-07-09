---
description: 进峰
---

# 🕋 Go操作MySQL和Redis

内部分享视频，没有剪辑。\


{% embed url="https://www.bilibili.com/video/BV1N7421o7hn/" %}

## Go操作MySQL

### Mysql使用

新建test数据库，person、place 表

```
CREATE TABLE `person` (
    `user_id` int(11) NOT NULL AUTO_INCREMENT,
    `username` varchar(260) DEFAULT NULL,
    `sex` varchar(260) DEFAULT NULL,
    `email` varchar(260) DEFAULT NULL,
    PRIMARY KEY (`user_id`)
  ) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8;
​
CREATE TABLE place (
    country varchar(200),
    city varchar(200),
    telcode int
)ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8;
```

使用第三方开源的mysql库: github.com/go-sql-driver/mysql （mysql驱动） github.com/jmoiron/sqlx （基于mysql驱动的封装）

命令行输入 ：

```
    go get github.com/go-sql-driver/mysql 
    go get github.com/jmoiron/sqlx
```

链接mysql

```
    database, err := sqlx.Open("mysql", "root:XXXX@tcp(127.0.0.1:3306)/gotest")
    //database, err := sqlx.Open("数据库类型", "用户名:密码@tcp(地址:端口)/数据库名")
```

#### 1. Insert操作

```
package main
​
import (
    "fmt"
    _ "github.com/go-sql-driver/mysql"
    "github.com/jmoiron/sqlx"
)
​
type Person struct {
    UserId   int    `db:"user_id"`
    Username string `db:"username"`
    Sex      string `db:"sex"`
    Email    string `db:"email"`
}
​
type Place struct {
    Country string `db:"country"`
    City    string `db:"city"`
    TelCode int    `db:"telcode"`
}
​
var Db *sqlx.DB
​
func init() {
    database, err := sqlx.Open("mysql", "root:root@tcp(127.0.0.1:3306)/gotest")
    if err != nil {
        fmt.Println("open mysql failed,", err)
        return
    }
    Db = database
}
​
func main() {
    r, err := Db.Exec("insert into person(username, sex, email)values(?, ?, ?)", "stu001", "man", "stu01@qq.com")
    if err != nil {
        fmt.Println("exec failed, ", err)
        return
    }
    id, err := r.LastInsertId()
    if err != nil {
        fmt.Println("exec failed, ", err)
        return
    }
​
    fmt.Println("insert succ:", id)
}
```

#### 2. Select操作

```
package main
​
import (
    "fmt"
​
    _ "github.com/go-sql-driver/mysql"
    "github.com/jmoiron/sqlx"
)
​
type Person struct {
    UserId   int    `db:"user_id"`
    Username string `db:"username"`
    Sex      string `db:"sex"`
    Email    string `db:"email"`
}
​
type Place struct {
    Country string `db:"country"`
    City    string `db:"city"`
    TelCode int    `db:"telcode"`
}
​
var Db *sqlx.DB
​
func init() {
​
    database, err := sqlx.Open("mysql", "root:root@tcp(127.0.0.1:3306)/gotest")
    if err != nil {
        fmt.Println("open mysql failed,", err)
        return
    }
​
    Db = database
}
​
func main() {
​
    var person []Person
    err := Db.Select(&person, "select user_id, username, sex, email from person where user_id=?", 1)
    if err != nil {
        fmt.Println("exec failed, ", err)
        return
    }
​
    fmt.Println("select succ:", person)
}
```

输出结果：

```
    select succ: [{1 stu001 man stu01@qq.com}]
```

#### 3. Update操作

```
package main
​
import (
    "fmt"
​
    _ "github.com/go-sql-driver/mysql"
    "github.com/jmoiron/sqlx"
)
​
type Person struct {
    UserId   int    `db:"user_id"`
    Username string `db:"username"`
    Sex      string `db:"sex"`
    Email    string `db:"email"`
}
​
type Place struct {
    Country string `db:"country"`
    City    string `db:"city"`
    TelCode int    `db:"telcode"`
}
​
var Db *sqlx.DB
​
func init() {
​
    database, err := sqlx.Open("mysql", "root:root@tcp(127.0.0.1:3306)/gotest")
    if err != nil {
        fmt.Println("open mysql failed,", err)
        return
    }
​
    Db = database
}
​
func main() {
​
    res, err := Db.Exec("update person set username=? where user_id=?", "stu0003", 1)
    if err != nil {
        fmt.Println("exec failed, ", err)
        return
    }
    row, err := res.RowsAffected()
    if err != nil {
        fmt.Println("rows failed, ",err)
    }
    fmt.Println("update succ:",row)
​
}
```

运行结果：

第一次运行：

```
    update succ: 1
    #受影响的行数 1
```

第二次运行

```
    update succ: 0
    #受影响的行数 0
```

#### 4. Delete操作

```
package main

import (
    "fmt"

    _ "github.com/go-sql-driver/mysql"
    "github.com/jmoiron/sqlx"
)

type Person struct {
    UserId   int    `db:"user_id"`
    Username string `db:"username"`
    Sex      string `db:"sex"`
    Email    string `db:"email"`
}

type Place struct {
    Country string `db:"country"`
    City    string `db:"city"`
    TelCode int    `db:"telcode"`
}

var Db *sqlx.DB

func init() {

    database, err := sqlx.Open("mysql", "root:root@tcp(127.0.0.1:3306)/gotest")
    if err != nil {
        fmt.Println("open mysql failed,", err)
        return
    }

    Db = database
}

func main() {

    /*
    _, err := Db.Exec("delete from person where user_id=?", 1)
    if err != nil {
        fmt.Println("exec failed, ", err)
        return
    }
    */

    res, err := Db.Exec("delete from person where user_id=?", 1)
    if err != nil {
        fmt.Println("exec failed, ", err)
        return
    }

    row,err := res.RowsAffected()
    if err != nil {
        fmt.Println("rows failed, ",err)
    }

    fmt.Println("delete succ: ",row)
}
```

运行结果：

第一次运行：

```
    delete succ: 1
    #受影响的行数 1
```

第二次运行：

```
    delete succ: 0
    #受影响的行数 0
```

#### 5. MySQL事务

mysql事务特性：

```
    1) 原子性
    2) 一致性
    3) 隔离性
    4) 持久性
```

golang MySQL事务应用：

```
1） import (“github.com/jmoiron/sqlx")
2)  Db.Begin()        开始事务
3)  Db.Commit()        提交事务
4)  Db.Rollback()     回滚事务
```

```
package main

    import (
        "fmt"

        _ "github.com/go-sql-driver/mysql"
        "github.com/jmoiron/sqlx"
    )

    type Person struct {
        UserId   int    `db:"user_id"`
        Username string `db:"username"`
        Sex      string `db:"sex"`
        Email    string `db:"email"`
    }

    type Place struct {
        Country string `db:"country"`
        City    string `db:"city"`
        TelCode int    `db:"telcode"`
    }

    var Db *sqlx.DB

    func init() {
        database, err := sqlx.Open("mysql", "root:root@tcp(127.0.0.1:3306)/gotest")
        if err != nil {
            fmt.Println("open mysql failed,", err)
            return
        }
        Db = database
    }

    func main() {
        conn, err := Db.Begin()
        if err != nil {
            fmt.Println("begin failed :", err)
            return
        }

        r, err := conn.Exec("insert into person(username, sex, email)values(?, ?, ?)", "stu001", "man", "stu01@qq.com")
        if err != nil {
            fmt.Println("exec failed, ", err)
            conn.Rollback()
            return
        }
        id, err := r.LastInsertId()
        if err != nil {
            fmt.Println("exec failed, ", err)
            conn.Rollback()
            return
        }
        fmt.Println("insert succ:", id)

        r, err = conn.Exec("insert into person(username, sex, email)values(?, ?, ?)", "stu001", "man", "stu01@qq.com")
        if err != nil {
            fmt.Println("exec failed, ", err)
            conn.Rollback()
            return
        }
        id, err = r.LastInsertId()
        if err != nil {
            fmt.Println("exec failed, ", err)
            conn.Rollback()
            return
        }
        fmt.Println("insert succ:", id)

        conn.Commit()
    }
```

输出结果：

```
    insert succ: 2
    insert succ: 3
```

查看MySQL：

```
```

## Go操作Redis

命令行输入 ：

```
 go get github.com/garyburd/redigo/redis
```

### 1. 链接Redis

```
package main

import (
    "fmt"
    "github.com/garyburd/redigo/redis"
)

func main() {
    c, err := redis.Dial("tcp", "localhost:6379")
    if err != nil {
        fmt.Println("conn redis failed,", err)
        return
    } 

    fmt.Println("redis conn success")

    defer c.Close()
}
```

### 2. String类型Set、Get操作

```
package main

import (
    "fmt"
    "github.com/garyburd/redigo/redis"
)

func main() {
    c, err := redis.Dial("tcp", "localhost:6379")
    if err != nil {
        fmt.Println("conn redis failed,", err)
        return
    }

    defer c.Close()
    _, err = c.Do("Set", "abc", 100)
    if err != nil {
        fmt.Println(err)
        return
    }

    r, err := redis.Int(c.Do("Get", "abc"))
    if err != nil {
        fmt.Println("get abc failed,", err)
        return
    }

    fmt.Println(r)
}
```

### 3. String批量操作

```
package main

import (
    "fmt"
    "github.com/garyburd/redigo/redis"
)

func main() {
    c, err := redis.Dial("tcp", "localhost:6379")
    if err != nil {
        fmt.Println("conn redis failed,", err)
        return
    }

    defer c.Close()
    _, err = c.Do("MSet", "abc", 100, "efg", 300)
    if err != nil {
        fmt.Println(err)
        return
    }

    r, err := redis.Ints(c.Do("MGet", "abc", "efg"))
    if err != nil {
        fmt.Println("get abc failed,", err)
        return
    }

    for _, v := range r {
        fmt.Println(v)
    }
}
```

运行结果：

```
    100
    300
```

### 4.设置过期时间

```
package main

import (
    "fmt"
    "github.com/garyburd/redigo/redis"
)

func main() {
    c, err := redis.Dial("tcp", "localhost:6379")
    if err != nil {
        fmt.Println("conn redis failed,", err)
        return
    }

    defer c.Close()
    _, err = c.Do("expire", "abc", 10)
    if err != nil {
        fmt.Println(err)
        return
    }
}
```

命令行运行：

```
    go run main.go
```

### 5.List队列操作

```
package main

import (
    "fmt"
    "github.com/garyburd/redigo/redis"
)

func main() {
    c, err := redis.Dial("tcp", "localhost:6379")
    if err != nil {
        fmt.Println("conn redis failed,", err)
        return
    }

    defer c.Close()
    _, err = c.Do("lpush", "book_list", "abc", "ceg", 300)
    if err != nil {
        fmt.Println(err)
        return
    }

    r, err := redis.String(c.Do("lpop", "book_list"))
    if err != nil {
        fmt.Println("get abc failed,", err)
        return
    }

    fmt.Println(r)
}
```

### 6.Hash表

```
package main

import (
    "fmt"
    "github.com/garyburd/redigo/redis"
)

func main() {
    c, err := redis.Dial("tcp", "localhost:6379")
    if err != nil {
        fmt.Println("conn redis failed,", err)
        return
    }

    defer c.Close()
    _, err = c.Do("HSet", "books", "abc", 100)
    if err != nil {
        fmt.Println(err)
        return
    }

    r, err := redis.Int(c.Do("HGet", "books", "abc"))
    if err != nil {
        fmt.Println("get abc failed,", err)
        return
    }

    fmt.Println(r)
}
```

### 7. Redis连接池

```
package main
​
import (
    "fmt"
    "strconv"
    "time"
    "github.com/gomodule/redigo/redis"
)
​
func getConnFromPool(pool *redis.Pool, i int) {
    conn := pool.Get()
    defer conn.Close()
    reply, err := conn.Do("SET", "conn"+strconv.Itoa(i), i)
    if err != nil {
        fmt.Println("Error setting value " + strconv.Itoa(i) + ":", err)
        return
    }
    s, err := redis.String(reply, err)
    if err != nil {
        fmt.Println("Error converting reply to string:", err)
        return
    }
    fmt.Println(s)
}
​
func main() {
    pool := &redis.Pool{
        MaxIdle:     10, //最大限制连接数
        MaxActive:   5, //最大活动连接数 ， 0 = 无限
        IdleTimeout: 100 * time.Second, //闲置链接超时的最大时间
        Dial: func() (redis.Conn, error) { //定义拨号获得连接的函数
            c, err := redis.Dial("tcp", "127.0.0.1:6379")
            return c, err
        },
    }
    //延时关闭连接池
    defer pool.Close()
​
    for i := 0; i < 10; i++ {
        //开辟并发协程执行
        go getConnFromPool(pool,i)
    }
    time.Sleep(3 * time.Second)
}
​
```
