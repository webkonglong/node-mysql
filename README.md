# node链接本地mysql实现增删改查


##### 前期准备
* `mysql -uroot -p` 登陆mysql
* `show databases;` 查看现有数据库
* `create database test;` 创建名为test的数据库
* `use test;` 使用(进入)test数据库
* `create table userinfo(userid int, balance int, type varchar(20));` 创建userinfo表,包含字段userid(整数型),balance(整数型),type(字符串,最大20位)


#### node链接mysql数据库
``` javascript
  ver mysql = require('mysql')
  var connection = mysql.createConnection({
    host: 'localhost'， //因为是本地地址所以用localhost
    user: 'root', // 默认是root用户
    password: ******, // 用户密码
    database: 'test', // 数据库名
    port: 3306 // mysql默认端口是3306
  })
```

##### 插入数据

``` javascript
  var addSql = 'INSERT INTO test(userid, balance, type) VALUES(?,?,?)' // test为表名
  var addSqlParams = [1, 8888, '成功'] // 和上面test后面的key一一对应
  connection.query(addSql, addSqlParams, (err, result) => {
    if (err) {
      console.log(`插入失败::${err.message}`)
      return
    }
    console.log(`插入成功::${result}`)
  })
  
```

##### 修改数据

``` javascript
  var modSql = 'UPDATE test SET balance = ? WHERE userid = ?' // 根据test表的userid值去更新对应的userid值
  var modSqlParams = [0, 1] // 索引0是表示吧balance修改为0,索引1 是代表修改userid为1的balance值
  connection.query(modSql, modSqlParams, (err, result) => {
    if (err) {
      console.log(`修改失败::${err.message}`)
      return
    }
    console.log(`修改成功::${result}`)
  })
  
```


##### 获取数据

``` javascript
  var sql = 'SELECT * FROM test' // 获取test表数据
  connection.query(sql, (err, result) => {
    if (err) {
      console.log(`获取失败::${err.message}`)
    } else {
      console.log(`获取成功::${result}`)
    }
  })
```


#### 删除数据

``` javascript
  var delSql = 'DELETE FROM test where userid=1' // 删除test表userid为1的数据
  connection.query(delSql, (err, result) => {
    if (err) {
      console.log(`删除失败::${err.message}`)
    } else {
      console.log(`删除成功::${result}`)
    }
  })
```



