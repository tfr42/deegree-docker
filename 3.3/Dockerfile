## tfr42/deegree:3.3
#
# This file is available under the following license:
# under LGPL 2.1 (LICENSE.TXT) Copyright 2020 Torsten Friebe <tfr@users.sourceforge.net>
FROM tomcat:8.5-jdk8

MAINTAINER Torsten Friebe <tfr@sourceforge.net>

# set deegree version
ENV DEEGREE_VERSION=3.3.21

EXPOSE 8080

# download deegree war file
RUN wget http://repo.deegree.org/content/repositories/public/org/deegree/deegree-webservices/${DEEGREE_VERSION}/deegree-webservices-${DEEGREE_VERSION}.war -O /usr/local/tomcat/webapps/deegree-webservices.war

# run tomcat
CMD ["catalina.sh", "run"]