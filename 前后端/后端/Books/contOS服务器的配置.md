# contSO的配置
## 1.先把阿里云服务器的系统切换为ContOS 
## 2.使用Xshell对服务器进行连接 
- 存在的问题:之前是用ssh对Ubuntu进行连接的,但是现在再用ssh进行连接就会出现这样的情况: 
![](https://github.com/fighting1023/Books/blob/master/notebook/img/2020-07-10%2018-27-28%20%E7%9A%84%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE.png)
- 解决办法:进入".ssh"隐藏文件夹,删除"known-hosts"文件,返回目录就能行了
- cd 命令可直接返回上一级目录
```angularjs
ubuntu@ubuntu:~$ cd .ssh/
ubuntu@ubuntu:~/.ssh$ ls
known_hosts
ubuntu@ubuntu:~/.ssh$ rm -rf known_hosts 
ubuntu@ubuntu:~/.ssh$ cd
ubuntu@ubuntu:~$ ssh root@47.105.91.77
The authenticity of host '47.105.91.77 (47.105.91.77)' can't be established.
ECDSA key fingerprint is SHA256:zzLf+CTDpRTe0ugjrrwDMPeGg8aMYBi/WWZSLyMvDnw.
Are you sure you want to continue connecting (yes/no)? y
Please type 'yes' or 'no': yes
Warning: Permanently added '47.105.91.77' (ECDSA) to the list of known hosts.
root@47.105.91.77's password: 

Welcome to Alibaba Cloud Elastic Compute Service !

Activate the web console with: systemctl enable --now cockpit.socket

Last login: Fri Jul 10 17:04:28 2020 from 159.226.194.170
[root@AliYun ~]# 
```
## 3.配置Mysql
- 下载安装包命令: wget http://...
- 确认安装包已下载
- 安装mysql命令: rpm -ivh mysql57-community-release-el7-9.noarch.rpm
- 进入/ect/yum.repos.d/,查看是否有两个repo文件
- 在当前文件夹下,安装mysql yum install mysql-server
```angularjs
[root@AliYun setup]# wget https://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm
--2020-07-10 17:15:01--  https://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm
Resolving dev.mysql.com (dev.mysql.com)... 137.254.60.11
Connecting to dev.mysql.com (dev.mysql.com)|137.254.60.11|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://repo.mysql.com//mysql57-community-release-el7-9.noarch.rpm [following]
--2020-07-10 17:15:02--  https://repo.mysql.com//mysql57-community-release-el7-9.noarch.rpm
Resolving repo.mysql.com (repo.mysql.com)... 23.211.97.88
Connecting to repo.mysql.com (repo.mysql.com)|23.211.97.88|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 9224 (9.0K) [application/x-redhat-package-manager]
Saving to: ‘mysql57-community-release-el7-9.noarch.rpm’

mysql57-community-release-e 100%[=========================================>]   9.01K  --.-KB/s    in 0s      

2020-07-10 17:15:02 (182 MB/s) - ‘mysql57-community-release-el7-9.noarch.rpm’ saved [9224/9224]

[root@AliYun setup]# ls
mysql57-community-release-el7-9.noarch.rpm
[root@AliYun setup]# rpm -ivh mysql57-community-release-el7-9.noarch.rpm 
warning: mysql57-community-release-el7-9.noarch.rpm: Header V3 DSA/SHA1 Signature, key ID 5072e1f5: NOKEY
Verifying...                          ################################# [100%]
Preparing...                          ################################# [100%]
Updating / installing...
   1:mysql57-community-release-el7-9  ################################# [100%]
[root@AliYun setup]# cd /etc/yum.repos.d/
[root@AliYun yum.repos.d]# ls
CentOS-AppStream.repo   CentOS-Debuginfo.repo  CentOS-Media.repo       mysql-community.repo
CentOS-Base.repo        CentOS-epel.repo       CentOS-PowerTools.repo  mysql-community-source.repo
CentOS-centosplus.repo  CentOS-Extras.repo     CentOS-Sources.repo
CentOS-CR.repo          CentOS-fasttrack.repo  CentOS-Vault.repo
[root@AliYun yum.repos.d]# yum install mysql-server
MySQL Connectors Community                                                    114 kB/s |  72 kB     00:00    
MySQL Tools Community                                                         531 kB/s | 440 kB     00:00    
MySQL 5.7 Community Server                                                    1.3 MB/s | 1.8 MB     00:01    
Dependencies resolved.
==============================================================================================================
 Package                         Arch        Version                                     Repository      Size
==============================================================================================================
Installing:
 mysql-server                    x86_64      8.0.17-3.module_el8.0.0+181+899d6349        AppStream       22 M
Installing dependencies:
 mariadb-connector-c-config      noarch      3.0.7-1.el8                                 AppStream       13 k
 mecab                           x86_64      0.996-1.module_el8.0.0+41+ca30bab6.9        AppStream      397 k
 mysql                           x86_64      8.0.17-3.module_el8.0.0+181+899d6349        AppStream       11 M
 mysql-common                    x86_64      8.0.17-3.module_el8.0.0+181+899d6349        AppStream      143 k
 mysql-errmsg                    x86_64      8.0.17-3.module_el8.0.0+181+899d6349        AppStream      557 k
 protobuf-lite                   x86_64      3.5.0-7.el8                                 AppStream      150 k
Enabling module streams:
 mysql                                       8.0                                                             

Transaction Summary
==============================================================================================================
Install  7 Packages

Total download size: 33 M
Installed size: 216 M
Is this ok [y/N]: y
Downloading Packages:
(1/7): mariadb-connector-c-config-3.0.7-1.el8.noarch.rpm                      180 kB/s |  13 kB     00:00    
(2/7): mysql-common-8.0.17-3.module_el8.0.0+181+899d6349.x86_64.rpm           1.9 MB/s | 143 kB     00:00    
(3/7): mecab-0.996-1.module_el8.0.0+41+ca30bab6.9.x86_64.rpm                  2.0 MB/s | 397 kB     00:00    
(4/7): mysql-errmsg-8.0.17-3.module_el8.0.0+181+899d6349.x86_64.rpm           7.2 MB/s | 557 kB     00:00    
(5/7): protobuf-lite-3.5.0-7.el8.x86_64.rpm                                   2.4 MB/s | 150 kB     00:00    
(6/7): mysql-8.0.17-3.module_el8.0.0+181+899d6349.x86_64.rpm                   20 MB/s |  11 MB     00:00    
(7/7): mysql-server-8.0.17-3.module_el8.0.0+181+899d6349.x86_64.rpm            39 MB/s |  22 MB     00:00    
--------------------------------------------------------------------------------------------------------------
Total                                                                          44 MB/s |  33 MB     00:00     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                      1/1 
  Installing       : mariadb-connector-c-config-3.0.7-1.el8.noarch                                        1/7 
  Installing       : mysql-common-8.0.17-3.module_el8.0.0+181+899d6349.x86_64                             2/7 
  Installing       : mysql-8.0.17-3.module_el8.0.0+181+899d6349.x86_64                                    3/7 
  Installing       : mysql-errmsg-8.0.17-3.module_el8.0.0+181+899d6349.x86_64                             4/7 
  Installing       : protobuf-lite-3.5.0-7.el8.x86_64                                                     5/7 
  Installing       : mecab-0.996-1.module_el8.0.0+41+ca30bab6.9.x86_64                                    6/7 
  Running scriptlet: mecab-0.996-1.module_el8.0.0+41+ca30bab6.9.x86_64                                    6/7 
  Running scriptlet: mysql-server-8.0.17-3.module_el8.0.0+181+899d6349.x86_64                             7/7 
  Installing       : mysql-server-8.0.17-3.module_el8.0.0+181+899d6349.x86_64                             7/7 
  Running scriptlet: mysql-server-8.0.17-3.module_el8.0.0+181+899d6349.x86_64                             7/7 
ValueError: File context for /var/log/mysql(/.*)? already defined

  Verifying        : mariadb-connector-c-config-3.0.7-1.el8.noarch                                        1/7 
  Verifying        : mecab-0.996-1.module_el8.0.0+41+ca30bab6.9.x86_64                                    2/7 
  Verifying        : mysql-8.0.17-3.module_el8.0.0+181+899d6349.x86_64                                    3/7 
  Verifying        : mysql-common-8.0.17-3.module_el8.0.0+181+899d6349.x86_64                             4/7 
  Verifying        : mysql-errmsg-8.0.17-3.module_el8.0.0+181+899d6349.x86_64                             5/7 
  Verifying        : mysql-server-8.0.17-3.module_el8.0.0+181+899d6349.x86_64                             6/7 
  Verifying        : protobuf-lite-3.5.0-7.el8.x86_64                                                     7/7 

Installed:
  mariadb-connector-c-config-3.0.7-1.el8.noarch                                                               
  mecab-0.996-1.module_el8.0.0+41+ca30bab6.9.x86_64                                                           
  mysql-8.0.17-3.module_el8.0.0+181+899d6349.x86_64                                                           
  mysql-common-8.0.17-3.module_el8.0.0+181+899d6349.x86_64                                                    
  mysql-errmsg-8.0.17-3.module_el8.0.0+181+899d6349.x86_64                                                    
  mysql-server-8.0.17-3.module_el8.0.0+181+899d6349.x86_64                                                    
  protobuf-lite-3.5.0-7.el8.x86_64                                                                            

Complete!
[root@AliYun yum.repos.d]# 
```

## 4.设置Mysql的密码
- 奇怪的一点:安装完mysql之后,输入命令"mysql"就能进去了
- 查找临时密码的语句也是失效的
```angularjs
进入mysql之后
mysql> ALTER USER USER() IDENTIFIED BY 'naruto';
Query OK, 0 rows affected (0.01 sec)
```
这样就对root用户添加了新的密码.
```angularjs
ctrl + d
就能退出mysql
```
- 检查mysql文件的保存位置,以及当前保存位置的磁盘大小 \
![](https://github.com/fighting1023/Books/blob/master/notebook/img/2020-07-10%2019-45-09%20%E7%9A%84%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE.png)
- 重启服务器之后用命令"mysql -u root -p"是进不去mysql的,需要重新启动mysql的服务,命令是"systemctl start mysqld",这样就能进去了
