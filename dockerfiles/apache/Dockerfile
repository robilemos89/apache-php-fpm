FROM centos:latest
RUN yum update && yum install -y httpd mod_ssl
# SSL
RUN mkdir /etc/httpd/ssl
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/httpd/ssl/apache.key -out /etc/httpd/ssl/apache.crt -subj "/C=GB/ST=London/L=London/O=Global Security/OU=IT Department/CN=localhost"
COPY ssl.conf /etc/httpd/conf.d/ssl.conf
# Apache MPM Event
RUN echo "LoadModule mpm_event_module modules/mod_mpm_event.so" > /etc/httpd/conf.modules.d/00-mpm.conf
# Remove welcome from CentOS
RUN rm /etc/httpd/conf.d/welcome.conf
# PHP-FPM settings
RUN echo "ProxyPassMatch ^/(.*\.php(/.*)?)$ fcgi://php:9000/var/www/html/$1" > /etc/httpd/conf.modules.d/02-php.conf
# Directory indexes
RUN echo "DirectoryIndex index.htm /index.htm /index.html index.html /index.php index.php" >> /etc/httpd/conf.modules.d/02-php.conf
# Apache settings
COPY httpd.conf /etc/httpd/conf/httpd.conf
<<<<<<< HEAD
# Copy apache startup script to /usr/local/bin
COPY apache2-foreground /usr/local/bin/

# Expose the HTTP & HTTPS ports
EXPOSE 80 443

# Finally, run httpd entrypoint
=======
COPY apache2-foreground /usr/local/bin/

EXPOSE 80
>>>>>>> 723b1debf6085dfa4079a0b4320714fe016d6dcd
CMD ["apache2-foreground"]
