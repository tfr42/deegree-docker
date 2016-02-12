deegree on Tomcat docker container
==================================

Latest deegree webservice on docker using Apache Tomcat 8 on Java SE 7 with deegree WAR from the deegree.org website.

Usage
-----

    % docker run -p 8080:8080 -d deegree/deegree-tomcat:latest

Build
-----
download the dockerfile into a directory an run:

    % docker build -t deegree/deegree-tomcat .

Access
------
open http://localhost:8080/deegree-webservices
when running docker on OS X or Windows with docker-machine then check the IP with

    % docker-machine ip <DOCKER_VM_NAME>

and run:

    % open http://$IP:8080/deegree-webservices