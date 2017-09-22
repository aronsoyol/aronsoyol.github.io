---
title: postgresql1
layout: post
date: 2017-09-11
---

## 9系をインストール

yum で8系が入ってる。そこで[https://yum.postgresql.org/repopackages.php](https://yum.postgresql.org/repopackages.php)からバージョン9のリポーをインストール


```
yum install https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-6-x86_64/pgdg-centos96-9.6-3.noarch.rpm

yum list | grep pgdg
yum install postgresql96
yum install postgresql96-devel
```


## サーバー起動、停止

```
#postgresユーザーでログイン、rootか他のユーザでは駄目らしい
$ su - postgres　

-bash-4.1$ /usr/pgsql-9.6/bin/pg_ctl -D /var/lib/pgsql/9.6/data -l logfile start
server starting
```

ちなみに`su  postgres`ハイフン抜けたらスタートできない、原因不明

```
[root@localhost dev]# su postgres
bash-4.1$ /usr/pgsql-9.6/bin/pg_ctl -D /var/lib/pgsql/9.6/data -l logfile start
could not change directory to "/home/dev": 許可がありません
server starting
bash-4.1$ /bin/sh: logfile: 許可がありません
```

停止もできない

```
bash-4.1$ /usr/pgsql-9.6/bin/pg_ctl stop
could not change directory to "/home/dev": 許可がありません
pg_ctl: no database directory specified and environment variable PGDATA unset
Try "pg_ctl --help" for more information.
```

## 外部アクセス可にする

[https://www.projectgroup.info/documents/PostgreSQL/POS_000007.html](https://www.projectgroup.info/documents/PostgreSQL/POS_000007.html)

`/var/lib/pgsql/9.6/data/pg_hba.conf`

```
host    all             all             0.0.0.0/0            password
```

`/var/lib/pgsql/9.6/data/postgresql.conf`

## 設定

- 設定ファイル
`sudo vi /var/lib/pgsql/data/postgresql.conf`

```
listen_addresses = "*"
port = 5432 
```
- create table
- \dt
- \d
- alter table
- drop table
- \i 外部SQLファイル

## python module 

`pip install psycopg2`

## insert 

❌`INSERT INTO url (url) VALUES ("http://mongolian.news.cn");`   
⭕`INSERT INTO url (url) VALUES ('http://mongolian.news.cn');` 

[http://mmiyauchi.com/?p=1223](http://mmiyauchi.com/?p=1223)

ダブル

