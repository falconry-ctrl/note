# centos 安装 mysql

### 1、下载 mysql

    https://downloads.mysql.com/archives/community/

### 2、解压到 /usr/local 目录下

    tar -zxvf mysql-5.7.37-linux-glibc2.12-x86_64.tar.gz
    mv mysql-5.7.37-linux-glibc2.12-x86_64 mysql
    mv mysql /user/local/

### 3、配置环境变量

    vim /etc/profile
    增加 export PATH=$PATH:/usr/local/mysql/bin
    source /etc/profile

### 4、修改配置文件

    vim /etc/my.cnf

    [mysql]
    default-character-set=utf8
    [mysqld]
    port = 3306
    basedir=/usr/local/mysql
    datadir=/usr/local/mysql/data
    character-set-server=utf8
    default-storage-engine=INNODB

### 5、创建 mysql 用户

    useradd -r -s /sbin/nologin mysql

### 6、给 mysql 用户授权

    chown -R mysql:mysql /usr/local/mysql/

### 7、将 mysql 添加到系统服务

    cp /usr/local/mysql/support-files/mysql.server /etc/init.d/
    chmod +x /etc/init.d/mysql.server
    chkconfig --add mysql.server

### 8、初始化

    cd /usr/local/mysql
    mysqld --initialize --user=mysql

### 9、启动mysql

    service mysql.server start

### 10、修改root密码

    mysql -u root -p
    ALTER USER 'root'@'localhost' IDENTIFIED BY '重置的密码';
    update user set host = '%' where user = 'root';
    FLUSH PRIVILEGES;
