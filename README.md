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

### nginxユーザ
nginxを起動する際にnginxユーザがないと怒られるので追加する必要あり
```
sudo useradd --shell /sbin/nologin nginx
```
