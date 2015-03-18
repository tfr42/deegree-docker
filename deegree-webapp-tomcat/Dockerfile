FROM dockerfile/java

MAINTAINER Sebastian Goerke <goerke@lat-lon.de>

EXPOSE 8080

ENV DEEGREE_VERSION 3.3.14

# add user
RUN sudo useradd -d /home/deegree -m deegree -p deegree
RUN sudo su deegree

# download tomcat
RUN wget http://mirror.netcologne.de/apache.org/tomcat/tomcat-8/v8.0.20/bin/apache-tomcat-8.0.20.zip -O /home/deegree/apache-tomcat-8.0.20.zip
RUN unzip /home/deegree/apache-tomcat-8.0.20.zip -d /home/deegree/
RUN sudo chmod 666 /home/deegree/apache-tomcat-8.0.20/bin/catalina.sh

# download deegree 
RUN wget http://repo.deegree.org/content/repositories/public/org/deegree/deegree-webservices/${DEEGREE_VERSION}/deegree-webservices-${DEEGREE_VERSION}.war -O /home/deegree/apache-tomcat-8.0.20/deegree-webservices.war


CMD /home/deegree/apache-tomcat-8.0.20/bin/catalina.sh start

