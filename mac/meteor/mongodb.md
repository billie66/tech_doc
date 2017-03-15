### mongo shell

* start mongo shell, type `meteor mongo` in your iterm

* then in the mongo shell type `help` to show help manual

* get all database methods, type `db.help()`

* get all collection methods, see `posts` collection, type `db.posts.help()`

* get all the records of the collection users, type `db.users.find()`


### check all the records of comments collection of meteor database

Note: meteor app should run

```
meteor mongo
use meteor
show collections
db.comments.find()
db.comments.find({postId: 1}).count()
```

### delete all of the records of comments collection

```
db.comments.remove({})
```

You can only remove one record at a time on browser console

```
Comments.remove('_id')
Comments.remove({postId: 1})
```

show all the records of comments collection

```
Comments.find().fetch()
```

the number of comments

```
Comments.find().count()
```

### update

```
db.users.update({username: 'aa'},{$set: {team: 4}})
```

### import data to mongodb

向 mongodb 导入数据需要用到 mongoimport 工具，meteor 自带的 mongodb 不提供这个工具，所以要在系统中重新安装 mongodb

```
brew update && brew install mongodb
```

mongodb 安装完成之后，新打开一个终端标签，输入 mongo，自动补全命令，可以看到所有与 mongodb 相关的命令。

在项目根目录下使用 mongoimport 命令，如下例所示，命令参数查看文档 [mongoimport](https://docs.mongodb.org/manual/reference/program/mongoimport/)

### 在本地开发环境导入数据

```
mongoimport -h 127.0.0.1:3001 --db meteor --collection users --file users.json
```

### 在服务器上导入数据

```
mongoimport --db qd --collection users --file users.json
```

若数据库中存在数据，想把备份的数据全部导入数据库，这是不能成功的，会报告如下错误：

```
☁  luck [master] mongoimport -h 127.0.0.1:3001 --db meteor --collection users --file ../users.json
2016-03-09T22:20:20.066+0800  connected to: 127.0.0.1:3001
2016-03-09T22:20:20.071+0800  error inserting documents: insertDocument :: caused by :: 11000 E11000 duplicate key error index: meteor.users.$_id_  dup key: { : "bJBG7uoNTmMcimLKq" }
2016-03-09T22:20:20.072+0800  imported 0 documents
```

经过测试后发现，执行 mongoimport 命令的时候，它不会覆盖数据库中的原有数据，而是把要导入的数据看做新数据插入到数据库中，这样必然导致上面的错误。

所以，要想如此暴力的导入数据，只能先清空数据库，然后再导入数据。感觉应该有比较温柔的方式吧，找找资料！！

### 在服务器上导出数据

```
mongoexport --db qd --collection users --out users.json
```

* 直接访问本地 mongodb 数据库中的 meteor collection, 也得保证 meteor 项目是运行着的

```
$ mongo 127.0.0.1:3001/meteor
```

* 如何在服务器端访问 mongodb 数据库的 meteor collection

```
server@aliyun:~$ mongo 127.0.0.1:27017/meteor
```

### 建议使用 mongodump 备份（导出）数据

```
mongodump -h 127.0.0.1 --port 27017 -d chat -c users
```

会在当前目录下生成一个 `dump/chat` 目录，存放从 `chat` 数据库 `users` 集合中导出的数据。

### 建议使用 mongorestore 导入数据

```
mongorestore --drop -h 127.0.0.1 --port 3001 -d meteor -c users ./meteor/users.bson
```

`-h` 默认值为 `localhost:27017`，`--port` 默认值为 27017

在服务器产品环境下，端口号为 `27017`，数据库名为 `chat`:

```
mongorestore --drop -h 127.0.0.1 --port 27017 -d chat -c users ./meteor/users.bson
```

[mongorestore](https://docs.mongodb.com/manual/reference/program/mongorestore/)

### 创建数据库

在 MongoDB 的 shell 命令行中操作：

```
use database_name
```

### 添加记录

```
db.users.insert({name: 'billie'})
```

### 删除数据库

比如说，一个名为 `bird` 的数据库，首先打开 MongoDB 的 shell 命令行，

```
mongo
```

然后 MongoDB 的 shell 命令行中操作：

```
show dbs
use bird
db.dropDatabase()
```

### 用 javascript 语言编写 mongo shell 脚本

<https://docs.mongodb.com/manual/tutorial/write-scripts-for-the-mongo-shell/>


### mongo shell quick reference

<http://docs.mongodb.org/manual/reference/program/mongo/>

<http://docs.mongodb.org/manual/reference/mongo-shell/>
