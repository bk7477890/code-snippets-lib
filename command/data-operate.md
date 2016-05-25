# Data Operate

## SQL

mysql.server start

awk 生成sql

1.#!/bin/sh
2.awk '
3.{
4.  sql="t_reply_message_copy_del.sql";
5.  printf("%s","delete from bbs_msg_copy.t_reply_message_copy where Fgroup_id=" )>>sql;
6.  printf("%s", $1) >>sql;
7.  printf("%s", " and Freply_message_id=") >>sql ;
8.  printf("%s", $2) >>sql;
9.  printf("%s\n", ";") >>sql;
10.}
11.' t_reply_message_copy_del_tmp.txt
