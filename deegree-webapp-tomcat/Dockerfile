## tfr42/deegree:3.4-jdk11
#
# This file is available under the following license:
# under LGPL 2.1 (LICENSE.TXT) Copyright 2020 Torsten Friebe <tfr@users.sourceforge.net>
FROM maven:3.6.3-jdk-11 as builder

RUN apt-get update && apt-get -yq install git

ARG REPO_URL=https://github.com/deegree/deegree3.git
ARG BRANCH=master
ARG TAG=3.4.14
ARG PROFILES=integration-tests
ARG MVN_OPTS=-Djava.awt.headless=true
WORKDIR /build_deegree/deegree3/
RUN mkdir -p /build_deegree && \
    cd /build_deegree && \
    git clone ${REPO_URL} && \
    cd deegree3 && \
    git checkout ${BRANCH} && \
    mvn ${MVN_OPTS} -P${PROFILES} install

FROM tomcat:9.0-jdk11 as runner

LABEL maintainer="Torsten Friebe <tfr@users.sourceforge.net>"

ARG DEEGREE_VERSION=3.4.14-SNAPSHOT-jdk11
ENV DEEGREE_WORKSPACE_ROOT /root/.deegree
ENV CATALINA_OPTS="-Djavax.xml.transform.TransformerFactory=com.sun.org.apache.xalan.internal.xsltc.trax.TransformerFactoryImpl"

WORKDIR /usr/local/tomcat/webapps/
# copy deegree war file from builder
COPY --from=builder /build_deegree/deegree3/deegree-services/deegree-webservices/target/deegree-webservices-${DEEGREE_VERSION}.war /usr/local/tomcat/webapps/deegree-webservices.war

# run tomcat
CMD ["catalina.sh", "run"]