## tfr42/deegree:3.6-jdk17
#
# This file is available under the following license:
# under LGPL 2.1 (LICENSE.TXT) Copyright 2020 Torsten Friebe <tfr@users.sourceforge.net>
FROM tomcat:10.1-jdk17-temurin

RUN apt-get update && apt-get -yq install zip

LABEL maintainer="Torsten Friebe <tfr@users.sourceforge.net>"

# set deegree version
ARG DEEGREE_VERSION=3.6.2

# API key to use; if empty API key will not change
ENV DEEGREE_API_KEY=
# console password to use; if empty not effective
ENV DEEGREE_CONSOLE_PW=
ENV DEEGREE_WORKSPACE_ROOT=/root/.deegree
ENV CATALINA_OPTS="-Djavax.xml.transform.TransformerFactory=net.sf.saxon.TransformerFactoryImpl -Dlog.dir=$CATALINA_HOME/logs"
ENV JAVA_OPTS="--add-opens java.base/java.lang=ALL-UNNAMED --add-opens java.desktop/com.sun.imageio.spi=ALL-UNNAMED --add-opens java.desktop/javax.imageio.spi=ALL-UNNAMED --add-exports java.desktop/sun.awt=ALL-UNNAMED --add-exports java.desktop/com.sun.imageio.spi=ALL-UNNAMED --add-exports java.desktop/sun.swing=ALL-UNNAMED --add-opens java.desktop/javax.imageio.spi=ALL-UNNAMED"
ENV LANG=en_US.UTF-8

WORKDIR /usr/local/tomcat/webapps/
# download deegree war file
RUN curl https://repo.deegree.org/content/repositories/public/org/deegree/deegree-webservices/${DEEGREE_VERSION}/deegree-webservices-${DEEGREE_VERSION}.war -o /usr/local/tomcat/webapps/deegree-webservices.war
RUN curl https://repo.deegree.org/content/repositories/public/org/deegree/deegree-documentation/${DEEGREE_VERSION}/deegree-documentation-${DEEGREE_VERSION}-html.zip -o /tmp/handbook.zip
ENV dest=/usr/local/tomcat/webapps/ROOT/
RUN unzip -d "$dest" /tmp/handbook.zip
RUN mv "$dest"/*/* "$dest"
RUN rm /tmp/handbook.zip

VOLUME $DEEGREE_WORKSPACE_ROOT
WORKDIR $DEEGREE_WORKSPACE_ROOT
# apply API key and console password
EXPOSE 8080
# apply apikey, password and run tomcat
CMD ([ -z "$DEEGREE_API_KEY" ] || (echo $DEEGREE_API_KEY > $DEEGREE_WORKSPACE_ROOT/config.apikey)) \
 && ([ -z "$DEEGREE_CONSOLE_PW" ] || (openssl passwd -5 $DEEGREE_CONSOLE_PW > $DEEGREE_WORKSPACE_ROOT/console.pw)) \
 && /usr/local/tomcat/bin/catalina.sh run