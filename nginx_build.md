## nginxのビルド/インストール手順

### 前提
gcc, prceライブラリ, zlibライブラリ, openSSLがインストールされている必要がある。  
ない場合はyumかapt-getでインストール出来る。  

以下はyumの場合の例
```
$ yum install gcc 
$ yum install prce prce-devel
$ yum install zlib zlib-devel
$ yum install openssl openssl-devel
```

### ダウンロード
バージョンは[ここ](http://nginx.org/en/download.html)で確認
```
$ wget http://nginx.org/download/nginx-1.11.7.tar.gz
```

### コンフィグスクリプトの実行
解凍後、レポジトリを移動して以下スクリプトを実行。このスクリプトを実行することでobjsフォルダができる。  
このフォルダにビルドに必要な設定が記述されたMakefileが出来る。
```
$ ./configure
```

何もオプションをつけないとデフォルトの設定になる。  
例えばインスールディレクトリがデフォルトで`/usr/local/nginx`となるので変更したい場合は`--prefix=`をつけて指定すると良い。  
様々なモジュールをオプションとしてつけることができる。  
しかしながら動的にモジュールをつけることはできないので何かモジュールをつけたい時に再コンパイルが必要となる欠点がある。  

**補足: nginx-1.9系から設定ファイルを修正することで動的にモジュールを追加できるようになった。しかし全てのモジュールには対応してない**  

### ビルド/インストール
以下コマンドでビルド
```
$ make
```

そして以下コマンドでインストール
```
$ make install
```

### TIPS
デフォルトのインストールディレクトリだと`/usr/local/nginx`にインストールされてしまうためnginxのバージョンが上がった場合デフォルトのディレクトリにインストールすると上書きされてしまう。  
それを回避するためには`--prefix=/usr/local/nginx-1.x.x`と指定して作成した後にシンボリックリンクで`/usr/local/nginx`が`/usr/local/nginx/1.x.x`を指すようにすれば良い。  
そうすることでnginxのバージョンが上がって再ビルドした場合もシンボリックの切り替えで対応出来る。
