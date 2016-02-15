deegree on Tomcat docker container
==================================

Latest deegree webservices on docker using Apache Tomcat 8 on Java SE 7 with deegree WAR from the deegree.org website.

Usage
-----

    % docker run -p 8080:8080 -d deegree/deegree-tomcat:latest

Build
-----

Download the Dockerfile into a directory an run:

    % docker build -t deegree/deegree-tomcat .

Access
------

Open http://localhost:8080/deegree-webservices
when running Docker on OS X or Windows with ```docker-machine``` then check the IP with:

    % docker-machine ip <DOCKER_VM_NAME>

and run:

    % open http://$IP:8080/deegree-webservices