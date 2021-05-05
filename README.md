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


## USAGE
### alp
nginxの再起動(設定変更はツール導入時に終わっている)
```
isucon@ubuntu-bionic:~$ sudo systemctl reload nginx
```

同じハンドラでまとめて集計
```
sudo alp --sum -r -f /var/log/nginx/access.log --aggregates='/api/estate/[0-9]+','/api/estate/req_doc/[0-9]+','/api/chair/[0-9]+','/api/chair/buy/*','/api/recommended_estate/[0-9]+'
```

### pt-query-digest
mysqlの再起動(設定変更はツール導入時に終わっている)
```
isucon@ubuntu-bionic:~$ sudo service mysql reload
 * Reloading MySQL database server mysqld                                                                 [ OK ]
isucon@ubuntu-bionic:~$ sudo systemctl reload mysqld
Failed to reload mysqld.service: Unit mysqld.service not found.
isucon@ubuntu-bionic:~$
isucon@ubuntu-bionic:~$
isucon@ubuntu-bionic:~$
isucon@ubuntu-bionic:~$ sudo service mysql status
● mysql.service - MySQL Community Server
   Loaded: loaded (/lib/systemd/system/mysql.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2021-05-05 06:25:15 UTC; 2h 24min ago
 Main PID: 1183 (mysqld)
    Tasks: 37 (limit: 2361)
   CGroup: /system.slice/mysql.service
           └─1183 /usr/sbin/mysqld --daemonize --pid-file=/run/mysqld/mysqld.pid

May 05 06:25:12 ubuntu-bionic systemd[1]: Starting MySQL Community Server...
May 05 06:25:15 ubuntu-bionic systemd[1]: Started MySQL Community Server.
```
