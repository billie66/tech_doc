### mongo shell

* start mongo shell, type `meteor mongo` in your iterm

* then in the mongo shell type `help` to show help manual

* get all database methods, type `db.help()`

* get all collection methods, see `posts` collection, type `db.posts.help()`

* get all the records of the collection users, type `db.users.find()`

### import data to mongodb

向 mongodb 导入数据需要用到 mongoimport 工具，meteor 自带的 mongodb 不提供这个工具，所以要在系统中重新安装 mongodb

```
brew update && brew install mongodb
```

mongodb 安装完成之后，新打开一个终端标签，输入 mongo，自动补全命令，可以看到所有与 mongodb 相关的命令。

在项目根目录下使用 mongoimport 命令，如下例所示，命令参数查看文档 [mongoimport](https://docs.mongodb.org/manual/reference/program/mongoimport/)

```
mongoimport -h 127.0.0.1:3001 --db users --collection contacts --file contacts.json
```

### mongo shell quick reference

<http://docs.mongodb.org/manual/reference/program/mongo/>

<http://docs.mongodb.org/manual/reference/mongo-shell/>
