## wordpressにnginxを使う場合に必要なものおよび導入手順

### 必要パッケージ
1. php(5.6)
2. php-fpm
3. mysql(5.6)

### 1. php
```
yum install http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
yum install php --enablerepo=remi-php56
```

### 2. php-fpm
```
yum install php-fpm --enablerepo=remi-php56
```

#### /etc/php-fpm.d/\www.confの設定
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

#### php-fpmの起動および自動起動設定
```
$ service php-fpm start
$ chkconfig php-fpm on
```

### 3. mysql
```
$ yum install http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
$ sed -i "s/enabled=1/enabled=0/g" /etc/yum.repos.d/mysql-community.repo
$ yum -y install mysql-community-server --enablerepo=mysql56-community
```

#### mysqlの起動および自動起動設定
```
$ service mysqld start
$ chkconfig mysqld on
```

#### mysqlの初期設定
```
$ mysql_secure_installation
Enter current password for root (enter for none): 【ENTERキーを入力】

Set root password? [Y/n] Y
New password:【mysqlのrootユーザのパスワード】
Re-enter new password:【mysqlのrootユーザのパスワード】

Remove anonymous users? [Y/n] Y

Disallow root login remotely? [Y/n] Y　

Remove test database and access to it? [Y/n] Y

Reload privilege tables now? [Y/n] Y
```

### おまけ(wordpress)
wgetするだけ。
urlをいちいち調べるのがだるいのでメモ
```
wget https://ja.wordpress.org/wordpress-4.3.1-ja.tar.gz
```
