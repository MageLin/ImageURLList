# 1.安装MySql
进入官网[下载地址:https://dev.mysql.com/downloads/mysql/](https://dev.mysql.com/downloads/mysql/ "mysql下载地址")，对应自己的系统，下载最新的版本即可，电脑是64位的，请选择64-bit的那个。
![](https://github.com/MageLin/MyDiary/blob/master/install%20mysql%20for%20idea/mysql_download_page.png)
如何想下载以前的版本，可以点击右上角的`Looking for previous GA versions?`。

# 2.配置
因为下载免安装版的，所以需要进行配置。
解压到某个文件路径后，进入bin文件夹下，找到一个名为`my-default.ini`文件，如果没有就需要创建一个。使用记事本打开文件：
![](https://github.com/MageLin/MyDiary/blob/master/install%20mysql%20for%20idea/custom_ini.png)
找到`# basedir = ....``# datadir = ....`这两个，把后面的省略号改成自己的所在路径，比如改为
```
#basedir = D:\\Software\\mysql-5.6.46-winx64
#datadir = D:\\Software\\mysql-5.6.46-winx64\\sqldata
```
datadir是保存的数据库的路径，按习惯设在当前路线下就好。

___

如果没有默认的配置文件，可以使用这个模板，更改某些路径参数即可
```
[client]
# 设置mysql客户端默认字符集
default-character-set=utf8
 
[mysqld]
# 设置3306端口
port = 3306
# 设置mysql的安装目录
basedir=D:\\Software\\mysql-5.6.46-winx64
# 设置 mysql数据库的数据的存放目录，MySQL 8+ 不需要以下配置，系统自己生成即可，否则有可能报错
# datadir=D:\\Software\\mysql-5.6.46-winx64\\sqldata
# 允许最大连接数
max_connections=20
# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
```

# 3.使用CMD工具
右键点击桌面左下角的window图标，弹出系统菜单，找到`Windows Powershell管理员`单击它，打开命令窗口。接下来，进入mysql的bin目录，我的在D盘，所以可以先输入`D：`然后按回车键，接着把bin目录路径直接复制粘贴到命令窗口里，路径前面加上cd关键字，按下回车进入目录。
![](https://github.com/MageLin/MyDiary/blob/master/install%20mysql%20for%20idea/cmd_mysql_into_dir.png)

## 安装mysql
接下来,输入命令`.\mysqld -install`。

## 启动服务
输入命令`net start mysql`。

## 停止服务
输入命令`net stop mysql`。

## 登录ROOT账户
输入命令`.\mysql -u root -p`,成功后，会需要你输入密码，但是因为未设置过密码，所以可以直接按enter键跳过。到此，我们就进入了mysql的控制台了。

## 新建自己的用户账号
输入命令`insert into mysql.user(Host,User,Password) values("localhost","请输入你自己的账号名字",password("请输入你自己的账号密码"));`
回车后，再输入命令刷新系统`flush privileges;`，记得别忘记分号。

## 删除自己的用户账号
输入命令`delete from mysql.user where User="请输入你自己的账号名字" and Host="localhost";`,再输入命令刷新系统`flush privileges;`，记得别忘记分号。

## 为自己的用户授权数据库访问权限
先创建一个数据，输入命令`create database 请输入你自己的数据库名字;`,然后输入
命令`grant all privileges on 请输入你自己的数据库名字.* to 请输入你自己的账号名字@localhost identified by '请输入你自己的账号密码';`
，再输入命令刷新系统`flush privileges;`，记得别忘记分号。如果想要删除数据库，输入命令`drop database 请输入你自己的数据库名字;`即可。

## 登录自己的用户账号
先退出ROOT账户，输入命令`exit;`。退出成功后，输入命令`.\mysql -u 请输入你自己的账号名字 -p`

## 修改自己的用户账号密码
退出自己的用户账号，登录ROOT用户账号后，输入命令
```
update mysql.user set password=password('请输入你自己的账号新密码') where User="请输入你自己的账号名字" and Host="localhost";
```
，再输入命令刷新系统`flush privileges;`，记得别忘记分号。
