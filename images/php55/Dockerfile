FROM centos:6

# Update
RUN yum -y update
RUN yum install -y epel-release


# PHP Install
RUN yum install -y curl git \
  && curl http://rpms.famillecollet.com/enterprise/remi-release-6.rpm -o /root/remi-release-6.rpm && rpm -Uvh /root/remi-release-6.rpm && rm /root/remi-release-6.rpm \
  && yum install -y --enablerepo=remi,remi-php55 php php-cli php-fpm php-common php-pear php-gd php-imap php-ldap php-mbstring php-mysql php-pdo php-mcrypt php-soap php-bcmath php-xml php-xmlrpc php-pecl-xdebug mysql \
  && curl http://www.phing.info/get/phing-latest.phar -o /usr/local/bin/phing && chmod a+x /usr/local/bin/phing \
  && curl https://phar.phpunit.de/phpunit.phar -o /usr/local/bin/phpunit && chmod a+x /usr/local/bin/phpunit \
  && curl curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin && mv /usr/local/bin/composer.phar /usr/local/bin/composer \
  && sed -e 's/127.0.0.1:9000/9000/' \
        -e '/allowed_clients/d' \
        -e '/catch_workers_output/s/^;//' \
        -e '/error_log/d' \
        -i /etc/php-fpm.d/www.conf \
  && yum -y clean all

ADD php.ini /etc/php.d/zzz_custom.ini

VOLUME /var/www/html
EXPOSE 9000

#ENTRYPOINT ["php-fpm","-F"]
