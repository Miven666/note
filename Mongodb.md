# Mongodb
## MongoDB后台管理 Shell
> 如果你需要进入MongoDB后台管理，你需要先打开mongodb装目录的下的bin目录，然后执行mongo命令文件。
MongoDB Shell是MongoDB自带的交互式Javascript shell,用来对MongoDB进行操作和管理的交互式环境。
当你进入mongoDB后台后，它默认会链接到 test 文档（数据库）：
```shell script
cd /usr/local/mongodb/bin
./mongo
```
- 看已有数据库 `show dbs`
- 切换数据库 `use test`
- 查看已有集合 `show collections` 或 `show tables`
- 创建集合 `db.createCollection(name, options)`
- 插入集合 `db.collection_name.insert(document)`
- 删除集合 `db.collection_name.remove(<query>,options)`