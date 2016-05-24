# HBASE

## Shell

```bash
$ ./bin/hbase shell

# List Information About your Table
hbase(main):002:0> list

# Scan the table for all data at once
hbase(main):006:0> scan 'test'

hbase(main):008:0> disable 'test'


hbase(main):007:0> get 'test', 'row1'
```

scan 'xsearch_solr',{LIMIT=>1}

## RESTFUL

### Starting and Stopping the REST Server

```bash
# Foreground
$ bin/hbase rest start -p <port>

# Background, logging to a file in $HBASE_LOGS_DIR
$ bin/hbase-daemon.sh start rest -p <port>

# To stop the REST server, use Ctrl-C if you were running it in the foreground, or the following command if you were running it in the background.

$ bin/hbase-daemon.sh stop rest
```
### RESTFUL API GET

```xml
http://example.com:8000/

http://example.com:8000/<table>/schema

http://example.com:8000/<table>/regions

http://example.com:8000/<table>/<row>/<column>:<qualifier>/<timestamp>/content:raw


http://example.com:8000/<table>/scanner/<scanner-id>


http://10.11.3.179:8088/

http://10.11.3.179:8088/xsearch_solr/regions

http://10.11.3.179:8088/xsearch_solr/000000460000000000241832402/cf:cate_prop_ids
```

## Reference

1. [HBase官方文档](https://hbase.apache.org/book.html#_rest)
