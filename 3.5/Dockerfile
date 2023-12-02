## tfr42/deegree:3.5-jdk11
#
# This file is available under the following license:
# under LGPL 2.1 (LICENSE.TXT) Copyright 2020 Torsten Friebe <tfr@users.sourceforge.net>
FROM tomcat:9-jdk11

RUN apt-get update && apt-get -yq install zip

LABEL maintainer="Torsten Friebe <tfr@users.sourceforge.net>"

# set deegree version
ARG DEEGREE_VERSION=3.5.5
ENV DEEGREE_WORKSPACE_ROOT=/root/.deegree
ENV CATALINA_OPTS="-Djavax.xml.transform.TransformerFactory=net.sf.saxon.TransformerFactoryImpl -Dlog.dir=$CATALINA_HOME/logs"

WORKDIR /usr/local/tomcat/webapps/
# download deegree war file
RUN curl https://repo.deegree.org/content/repositories/public/org/deegree/deegree-webservices/${DEEGREE_VERSION}/deegree-webservices-${DEEGREE_VERSION}.war -o /usr/local/tomcat/webapps/deegree-webservices.war && \
    curl https://repo.deegree.org/content/repositories/public/org/deegree/deegree-webservices-handbook/${DEEGREE_VERSION}/deegree-webservices-handbook-${DEEGREE_VERSION}-html.zip -o /tmp/handbook.zip && \
    unzip /tmp/handbook.zip -d /usr/local/tomcat/webapps/ROOT/

EXPOSE 8080
# run tomcat
CMD ["catalina.sh", "run"]