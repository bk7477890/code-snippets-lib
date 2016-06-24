# SQL

## DDL

### alter

alter table  `AlgoDcTaskConf` modify column `comment` varchar(128);

### add

ALTER TABLE `AlgoDc`.`AlgoDcFieldInfo` CHANGE COLUMN `relateTaskId` `relateTaskId` varchar(128) NOT NULL COMMENT '字段相关的任务id', ADD COLUMN `fieldType` int(4) NOT NULL DEFAULT 0 COMMENT '字段数据类型,0:int,1:String' AFTER `relateTaskId`, ADD COLUMN `fieldDefaultValue` varchar(32) NOT NULL DEFAULT 0 COMMENT '字段默认值' AFTER `fieldType`;

## Mysql


cd /usr/bin/mysql/bin/ && ./mysql -h10.11.4.171 -P3306 -usearch -p13734f13b4429a477428c828e489607a

./usr/bin/mysql -h10.11.4.171 -P3306 -Dmogujiesearch -usearch -p13734f13b4429a477428c828e489607a
