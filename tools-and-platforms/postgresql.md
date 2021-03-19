# PostgreSQL

## [Linux 安装](https://www.youtube.com/watch?v=lX9uMCSqqko)

### 安装PostgreSQL 

```text
sudo apt install postgresql
也可以同时安装一个包
sudo apt install postgresql postgresql-contrib
```

### 安装pgAdmin

```text
curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo apt-key add
sudo sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
sudo apt install pgadmin4
安装成功后在Ubuntu系统的app界面可以直接打开pgadmin的app
第一次打开需要设置密码：root123
```

初次设置pgAdmin就按照[视频](https://www.youtube.com/watch?v=lX9uMCSqqko)从14：20开始

## 登录

### 初次登录，用系统默认的账户

```text
sudo -u postgres psql
退出  \q
查询信息  \conninfo
返回数据库名称、用户名称和端口号：
You are connected to database "postgres" as user "postgres" via 
socket in "/var/run/postgresql" at port "5432".
修改密码
ALTER USER postgres PASSWORD 'root';
```

### 创建用户登录

```text
第一步：
sudo -u postgres createuser --interactive
Enter name of role to add: hdong
Shall the new role be a superuser? (y/n) 

第二步：
通过postgres账户进入系统修改hdong的密码为root
\q 退出当前数据库

第三步：
通过hdong登录
psql -U hdong -h localhost -d 数据库name
输入刚才修改的密码root
\conninfo
You are connected to database "demo1" as user "hdong" on host "localhost" (address "127.0.0.1") at port "5432".
SSL connection (protocol: TLSv1.3, cipher: TLS_AES_256_GCM_SHA384, bits: 256, compression: off)

或者在上述登录指令中不输入最后的-d，则进入根目录，
```

### 创建/删除数据库

```text
sudo -u postgres createdb demo1
或者在根目录下
CREATE DATABASE demo2;
DROP DATABASE demo2;
```

## 基础指令

```text
\l  list of database
\c name use this database
\du list of roles
\dt show table in database
```

