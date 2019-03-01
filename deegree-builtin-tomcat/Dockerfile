FROM java:7

MAINTAINER Torsten Friebe <tfr@sourceforge.net>

# set deegree version
ENV DEEGREE_VERSION 3.3.21

EXPOSE 8080

# download deegree tomcat bundle
RUN wget http://repo.deegree.org/content/repositories/public/org/deegree/deegree-webservices/${DEEGREE_VERSION}/deegree-webservices-${DEEGREE_VERSION}.zip -O /tmp/deegree.zip

# unpack 
RUN unzip /tmp/deegree.zip -d /opt/ && \
    ln -s /opt/deegree-webservices-${DEEGREE_VERSION}/ /opt/deegree && \
    rm /tmp/deegree.zip

# run tomcat
CMD ["/opt/deegree/bin/catalina.sh", "run"]
