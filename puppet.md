# Scratchpad 4 Puppet
puppet master --verbose --no-daemonize

##	puppet.conf:
```
dns_alt_names = puppet,puppet.example.com,puppetmaster01,puppetmaster01.example.com
```

##	Setup Web server - Passenger with Apache
```
yum install -y httpd httpd-devel mod_ssl ruby-devel rubygems gcc
gem install -y rack passenger
yum install -y gcc-c++ libcurl-devel openssl-devel zlib-devel
passenger-install-apache2-module
```

##	add /etc/puppet/puppet.conf
```
echo '[master]
always_cache_feature=true' >> /tmp/l1
```

##	Install the Puppet Master Rack App
```
mkdir -p /usr/share/puppet/rack/puppetmasterd
mkdir /usr/share/puppet/rack/puppetmasterd/public /usr/share/puppet/rack/puppetmasterd/tmp
cp /usr/share/puppet/ext/rack/config.ru /usr/share/puppet/rack/puppetmasterd/
chown puppet:puppet /usr/share/puppet/rack/puppetmasterd/config.ru
```
##	Create and Enable the Puppet Master Vhost
```
touch /etc/httpd/conf.d/puppetmaster.conf
```
## RHEL/CentOS:
```
#LoadModule passenger_module /usr/lib/ruby/gems/1.8/gems/passenger-4.0.x/ext/apache2/mod_passenger.so
#PassengerRoot /usr/lib/ruby/gems/1.8/gems/passenger-4.0.x
#PassengerRuby /usr/bin/ruby

   LoadModule passenger_module /usr/lib/ruby/gems/1.8/gems/passenger-5.0.11/buildout/apache2/mod_passenger.so
   <IfModule mod_passenger.c>
     PassengerRoot /usr/lib/ruby/gems/1.8/gems/passenger-5.0.11
     PassengerDefaultRuby /usr/bin/ruby
   </IfModule>

chkconfig puppetmaster off
chkconfig httpd on
```
##	Foreman
```
yum -y install http://yum.theforeman.org/releases/1.8/el6/x86_64/foreman-release.rpm
yum -y install foreman-installer
foreman-installer
```