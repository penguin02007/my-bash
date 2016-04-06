### Install Zabbix 2.2 and MariaDB on Centos 7
#### DB Script taken from https://www.zabbix.com/documentation/2.4/manual/appendix/install/db_scripts

#### Install repository
```
cd /tmp
wget http://repo.zabbix.com/zabbix/2.2/rhel/7/x86_64/zabbix-release-2.2-1.el7.noarch.rpm
wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
yum localinstall *release.epm
```

#### Install PHP dependency
```
yum install php-bcmath php-bcstring
```
#### Install zabbix server for MySQL
```
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
ip=localhost	# Replace if database is installed seperatly
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
cd /usr/share/doc/zabbix-server-mysql-1.2.11/create
cd /usr/share/zabbix-mysql/	# if you install from epel
```
mariadb>
```
mysql -uroot zabbix < schema.sql
# stop here if you are creating database for Zabbix proxy
mysql -uroot zabbix < images.sql
mysql -uroot zabbix < data.sql
