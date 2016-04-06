### Install Zabbix and MariaDB on Centos 7
#### https://www.zabbix.com/documentation/2.4/manual/appendix/install/db_scripts


#### Install PHP dependency
```
yum install php-bcmath php-bcstring
```
#### Install zabbix server for MySQL
```
wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
yum localinstall -y epel-release-7-5.noarch.rpm
yum install -y zabbix-server-mysql zabbix-web-mysql
```
#### Install agent to monitor itself and JMX
```
yum install -y zabbix-agent zabbix-java-gateway
```

#### Install MariaDB
```
yum install mariadb-server
systemctl start mariadb
systemctl enable mariadb
```
ip=xxx
shell>
```
mysql -uroot -p
```
mariadb>
```
create database zabbixdb character set utf8 collate utf8_bin;
GRANT ALL ON zabbixdb.* TO 'zabbix'@'$ip' IDENTIFIED BY 'zabbix';
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
