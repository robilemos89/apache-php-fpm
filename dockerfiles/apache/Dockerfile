FROM centos:latest
RUN yum update && yum install -y httpd
RUN echo "LoadModule mpm_event_module modules/mod_mpm_event.so" > /etc/httpd/conf.modules.d/00-mpm.conf
RUN rm /etc/httpd/conf.d/welcome.conf
RUN echo "ProxyPassMatch ^/(.*\.php(/.*)?)$ fcgi://php:9000/var/www/html/$1" > /etc/httpd/conf.modules.d/02-php.conf
RUN echo "DirectoryIndex index.htm /index.htm /index.html index.html /index.php index.php" >> /etc/httpd/conf.modules.d/02-php.conf
COPY httpd.conf /etc/httpd/conf/httpd.conf
COPY apache2-foreground /usr/local/bin/

EXPOSE 80
CMD ["apache2-foreground"]
