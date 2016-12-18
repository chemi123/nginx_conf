### 目的
yumでインストールする際の手順をnginxを例にメモ

### レポジトリ登録
/etc/yum.repos.d以下にnginx.repoを作成(~.repoでインストールするものを登録するイメージ)
```
$ sudo touch /etc/yum.repos.d/nginx.repo
```

nginx.repoは以下の内容
```
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=0
enabled=1
```

### インストール
```
sudo yum install nginx
```

以上！


### おまけ
nginxを起動する際にnginxユーザがないと怒られるので追加する必要あり
```
sudo useradd --shell /sbin/nologin nginx
```

### /etc/php-fpm/www.confの設定

ここですっごくつまづいた。。。

修正前
```
listen = 127.0.0.1:9000 

user = apache
group = apache
```

修正後
```
listen = 9000

user = nginx
group = nginx
```
