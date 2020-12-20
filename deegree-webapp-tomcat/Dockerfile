FROM tomcat:8.5-jdk8

LABEL maintainer="Torsten Friebe <tfr@users.sourceforge.net>"

# set deegree version
ENV DEEGREE_VERSION 3.4.14
ENV CATALINA_OPTS="-Djavax.xml.transform.TransformerFactory=com.sun.org.apache.xalan.internal.xsltc.trax.TransformerFactoryImpl"

EXPOSE 8080

# download deegree war file
RUN wget http://repo.deegree.org/content/repositories/public/org/deegree/deegree-webservices/${DEEGREE_VERSION}/deegree-webservices-${DEEGREE_VERSION}.war -O /usr/local/tomcat/webapps/deegree-webservices.war

# run tomcat
CMD ["catalina.sh", "run"]