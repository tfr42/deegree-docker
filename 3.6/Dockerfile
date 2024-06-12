## tfr42/deegree:3.6-jdk17
#
# This file is available under the following license:
# under LGPL 2.1 (LICENSE.TXT) Copyright 2020 Torsten Friebe <tfr@users.sourceforge.net>
FROM tomcat:10.1-jdk17-temurin

RUN apt-get update && apt-get -yq install zip

LABEL maintainer="Torsten Friebe <tfr@users.sourceforge.net>"

# set deegree version
ARG DEEGREE_VERSION=3.6.0-pre2

# API key to use; if empty API key will not change
ENV DEEGREE_API_KEY=
# console password to use; if empty not effective
ENV DEEGREE_CONSOLE_PW=
ENV DEEGREE_WORKSPACE_ROOT=/root/.deegree
ENV CATALINA_OPTS="-Djavax.xml.transform.TransformerFactory=net.sf.saxon.TransformerFactoryImpl -Dlog.dir=$CATALINA_HOME/logs"

WORKDIR /usr/local/tomcat/webapps/
# download deegree war file
RUN curl https://repo.deegree.org/content/repositories/public/org/deegree/deegree-webservices/${DEEGREE_VERSION}/deegree-webservices-${DEEGREE_VERSION}.war -o /usr/local/tomcat/webapps/deegree-webservices.war
RUN curl https://repo.deegree.org/content/repositories/public/org/deegree/deegree-webservices-handbook/${DEEGREE_VERSION}/deegree-webservices-handbook-${DEEGREE_VERSION}-html.zip -o /tmp/handbook.zip
RUN unzip /tmp/handbook.zip -d /usr/local/tomcat/webapps/ROOT/

VOLUME $DEEGREE_WORKSPACE_ROOT
WORKDIR $DEEGREE_WORKSPACE_ROOT
# apply API key and console password
RUN ([ -z "$DEEGREE_API_KEY" ] || (echo $DEEGREE_API_KEY > $DEEGREE_WORKSPACE_ROOT/config.apikey))
RUN ([ -z "$DEEGREE_CONSOLE_PW" ] || (openssl passwd -5 $DEEGREE_CONSOLE_PW > $DEEGREE_WORKSPACE_ROOT/console.pw))

EXPOSE 8080
# run tomcat
CMD ["catalina.sh", "run"]