# isucon10

## 導入  
### 元ファイルをクローン  
`git clone https://github.com/matsuu/vagrant-isucon`

### Vargantfileの内容変更(クローンもとをiwashiさんのリポジトリに変える)  
```
-    git clone https://github.com/isucon/isucon10-qualify.git ${GITDIR}  
+    git clone https://github.com/iwashi/isucon10-qualify.git ${GITDIR}
```

### Vargantfileのあるディレクトリで  
`vagrant up`

### ベンチマークの実行  
```sudo -i -u isucon  
cd isuumo/bench  
./bench -target-url http://127.0.0.1
```

### 計測ツールの導入
```
cd 	isucon_secret_source
chmod -R +x  ./isucon_secret_sauce/
cd isucon_secret_sauce

./setup.sh
```


## 計測ツールUSAGE
### alp
アクセスログの解析  
nginxの再起動(設定変更はツール導入時に終わっている)
```
isucon@ubuntu-bionic:~$ sudo systemctl reload nginx
```

同じハンドラでまとめて集計
```
sudo alp --sum -r -f /var/log/nginx/access.log --aggregates='/api/estate/[0-9]+','/api/estate/req_doc/[0-9]+','/api/chair/[0-9]+','/api/chair/buy/*','/api/recommended_estate/[0-9]+'
```

### pt-query-digest
mysql設定変更
```
isucon@ubuntu-bionic:~/isuumo/bench$ sudo vi  /etc/mysql/mysql.conf.d/mysqld.cnf
```
以下のチェックを外してスローログ取得を有効化する
```
# Here you can see queries with especially long duration
slow_query_log         = 1
slow_query_log_file    = /var/log/mysql/mysql-slow.log
long_query_time = 0
```

mysqlの再起動
```
isucon@ubuntu-bionic:~/isuumo/bench$ sudo service mysql restart
```


mysqlログイン&スローログ設定確認
```
isucon@ubuntu-bionic:~/isuumo/bench$ sudo mysql -u isucon -p
Enter password:isucon
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2416
Server version: 5.7.33-0ubuntu0.18.04.1 (Ubuntu)

Copyright (c) 2000, 2021, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show variables like 'slow%';
+---------------------+-------------------------------+
| Variable_name       | Value                         |
+---------------------+-------------------------------+
| slow_launch_time    | 2                             |
| slow_query_log      | ON                            |
| slow_query_log_file | /var/log/mysql/mysql-slow.log |
+---------------------+-------------------------------+
3 rows in set (0.00 sec)
```


## netdata
ブラウザでサーバリソース使用量のリアルタイム表示
```
http://172.28.128.3:19999/
```
スクリーンショット 2021-05-05 19.19.21![image](https://user-images.githubusercontent.com/82875507/117127374-f7630380-add6-11eb-9bf4-f8c8a2a61698.png)



