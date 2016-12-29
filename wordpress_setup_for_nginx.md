## wordpressにnginxを使う場合に必要なものおよび導入手順

### 必要パッケージ
- php(5.6)
- php-fpm
- mysql(5.6)

### php
```
yum install http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
yum install php --enablerepo=remi-php56
```

### php-fpm
```
yum install php-fpm --enablerepo=remi-php56
```

### mysql
```
$ yum install http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
$ sed -i "s/enabled=1/enabled=0/g" /etc/yum.repos.d/mysql-community.repo
$ yum -y install mysql-community-server --enablerepo=mysql56-community
```

### おまけ(wordpress)
wgetするだけ。
urlをいちいち調べるのがだるいのでメモ
```
wget https://ja.wordpress.org/wordpress-4.3.1-ja.tar.gz
```
