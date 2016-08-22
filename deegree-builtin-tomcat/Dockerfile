FROM java:7

MAINTAINER deegree TMC <tmc@deegree.org>

EXPOSE 8080

ENV DEEGREE_VERSION 3.3.18

# download deegree
RUN wget http://repo.deegree.org/content/repositories/public/org/deegree/deegree-webservices/${DEEGREE_VERSION}/deegree-webservices-${DEEGREE_VERSION}.zip -O /tmp/deegree.zip

# unpack 
RUN unzip /tmp/deegree.zip -d /opt/ && \
    ln -s /opt/deegree-webservices-${DEEGREE_VERSION}/ /opt/deegree && \
    rm /tmp/deegree.zip

# run tomcat
CMD /opt/deegree/bin/catalina.sh run
