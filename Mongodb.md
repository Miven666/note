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
- 查看集合 `db.collection_name.find()`
- 创建集合 `db.createCollection(name, options)`
- 插入集合 `db.collection_name.insert(document)`
- 删除集合 `db.collection_name.remove(<query>,options)`
- 查看指定列 
  + 查看 id 和 title 列 `db.collection_name.find({}, {id:1,title:1})`
  + 查看所有列除了 `content` `db.collection.find({}, {content:0})`

### 导出数据

```shell
#!/bin/bash

if [ ! $1 ]; then
        echo " Example of use: $0 database_name [dir_to_store]"
        exit 1
fi
db=$1
out_dir=$2
if [ ! $out_dir ]; then
        out_dir="./"
else
        mkdir -p $out_dir
fi

tmp_file="fadlfhsdofheinwvw.js"
echo "print('_ ' + db.getCollectionNames())" > $tmp_file
cols=`/usr/local/mongodb/bin/mongo $db $tmp_file | grep '_' | awk '{print $2}' | tr ',' ' '`
for c in $cols
do
    /usr/local/mongodb/bin/mongoexport -d $db -c $c -o "$out_dir/exp_${db}_${c}.json"
done
tar -czvf ${db}.tar.gz exp_* && rm -rf exp_*
rm $tmp_file
```



- 用上述脚本导出指定库
- 上传至 ftp `put feeder.tar.gz`