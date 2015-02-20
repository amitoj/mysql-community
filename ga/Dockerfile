FROM centos:7
# basic repo stuff: EPEL and Oracle MySQL GA
RUN yum -y install http://mirrors.mit.edu/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
RUN yum -y install --nogpgcheck http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm

# Update
RUN yum -y distro-sync
RUN yum -y install --nogpgcheck  yum-utils \
	supervisor \
	hostname \
	perl-Data-Dumper \
	sysvinit-tools

# Common for Enterprise and Community
RUN yum -y install --nogpgcheck mysql-utilities

# Community
RUN yum -y install --nogpgcheck mysql-community-* 

RUN rm /var/lib/mysql/* -fr

VOLUME /var/lib/mysql
VOLUME /backup

RUN useradd backup -d /backup -g mysql
RUN chown -R mysql:mysql /var/lib/mysql
RUN chown -R backup:mysql /backup

ADD ./docker-entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ADD ./Dockerfile /Dockerfile

ENTRYPOINT /entrypoint.sh
