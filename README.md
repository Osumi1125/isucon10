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
同じハンドラでまとめて集計
```
sudo alp --sum -r -f /var/log/nginx/access.log --aggregates='/api/estate/[0-9]+','/api/estate/req_doc/[0-9]+','/api/chair/[0-9]+','/api/chair/buy/*','/api/recommended_estate/[0-9]+'
```
