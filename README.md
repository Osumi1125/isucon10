# isucon10

インストールもと  
`git clone https://github.com/matsuu/vagrant-isucon`

ファイルの設定変更(クローンもとをiwashiさんのリポジトリに変える)  
`-    git clone https://github.com/isucon/isucon10-qualify.git ${GITDIR}`  
`+    git clone https://github.com/iwashi/isucon10-qualify.git ${GITDIR}`

Vargantファイルのあるディレクトリで  
`vagrant up`

ベンチマークの実行
`sudo -i -u isucon
cd isuumo/bench
./bench -target-url http://127.0.0.1`
