### Install MariaDB on Centos 7 for Zabbix
#### https://www.zabbix.com/documentation/2.4/manual/appendix/install/db_scripts


yum install mariadb-server
systemctl start mariadb
chkconfig mariadb on

ip=xxx
shell>
```
mysql -uroot -p
```
mariadb>
```
create database zabbix character set utf8 collate utf8_bin;
GRANT ALL ON zabbix.* TO 'zabbix'@'$ip' IDENTIFIED BY 'zabbix';
quit
```

# Create zabbix database
shell>
```
cd /usr/share/zabbix-mysql/
```
mariadb>
```
mysql -uroot zabbix < schema.sql
# stop here if you are creating database for Zabbix proxy
mysql -uroot zabbix < images.sql
mysql -uroot zabbix < data.sql