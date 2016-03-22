FROM centos:6

# Update
RUN yum -y update
RUN yum install -y epel-release

# Apache Install
RUN yum -y install httpd tinyproxy dnsmasq supervisor \
  && rm /etc/httpd/conf.d/welcome.conf \
  && sed -i 's,ErrorLog logs/error_log,ErrorLog /dev/stderr,' /etc/httpd/conf/httpd.conf \
  && sed -i 's,CustomLog logs/access_log combined,CustomLog /dev/stdout combined,' /etc/httpd/conf/httpd.conf \
  && sed -i 's,DirectoryIndex index.html index.html.var,DirectoryIndex index.php index.hh index.html index.html.var,' /etc/httpd/conf/httpd.conf \
  && rpm --import http://dag.wieers.com/rpm/packages/RPM-GPG-KEY.dag.txt && rpm -Uvh http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm \
  && yum -y install mod_fastcgi \
  && sed -i 's/^FastCgiWrapper On/FastCgiWrapper Off/' /etc/httpd/conf.d/fastcgi.conf \
  && mkdir /usr/lib/cgi-bin \
  && yum -y clean all

ADD vhosts.conf /etc/httpd/conf.d/zzz_custom.conf
ADD dnsmasq.conf /etc/dnsmasq.conf
ADD resolv.dnsmasq.conf /etc/resolv.dnsmasq.conf
ADD tinyproxy.conf /etc/tinyproxy/tinyproxy.conf
ADD supervisord.conf /etc/supervisord.conf
ADD fix_resolv.sh /fix_resolv.sh

VOLUME /var/www/html
EXPOSE 80
EXPOSE 8888

#ENTRYPOINT ["httpd","-DFOREGROUND" ]
#ENTRYPOINT ["supervisord"]
