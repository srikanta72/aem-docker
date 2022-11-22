FROM centos:7

# Install Apache
RUN yum install -y --enablerepo=centosplus \
      tar \
      wget \
      libselinux-devel \
      httpd-2.4.6 \
    && yum clean all

# Download the dispatcher
RUN wget https://www.adobeaemcloud.com/content/companies/public/adobe/dispatcher/dispatcher/_jcr_content/top/download_9/file.res/dispatcher-apache2.4-linux-x86-64-ssl-4.2.3.tar.gz
RUN mkdir -p dispatcher
RUN tar -C dispatcher -zxvf dispatcher-apache2.*.tar.gz

# Copy the dispatcher
RUN cp ./dispatcher/dispatcher-apache2.*.so /etc/httpd/modules/
RUN ln -s /etc/httpd/modules/dispatcher-apache2.*.so /etc/httpd/modules/mod_dispatcher.so

# RUN cp ./dispatcher/conf/httpd.conf.disp2 /etc/httpd/conf/httpd.conf
# RUN cp ./dispatcher/conf/dispatcher.any /etc/httpd/conf/dispatcher.any
# RUN cp ./dispatcher/conf/author_dispatcher.any /etc/httpd/conf/author_dispatcher.any

# Add config files
#ADD ./httpd/conf /etc/httpd/conf
#ADD ./httpd/conf.d /etc/httpd/conf.d
#ADD ./httpd/conf.dispatcher.d /etc/httpd/conf.dispatcher.d
#ADD ./httpd/conf.modules.d /etc/httpd/conf.modules.d

ADD ./httpd.conf /etc/httpd/conf/httpd.conf
ADD ./dispatcher.any /etc/httpd/conf/dispatcher.any
ADD ./aem-disp2.conf /etc/httpd/conf.d/aem-disp2.conf
ADD ./proxy.conf /etc/httpd/conf.d/proxy.conf
# Set permissions
RUN chown -R daemon:daemon /var/www/html

EXPOSE 80 443
CMD /usr/sbin/httpd -D FOREGROUND