deegree/Tomcat bundle docker container
======================================

Latest deegree webservice on docker using the pre-built deegree/Tomcat bundle from the deegree.org website.

Usage
-----

```
docker run -p 8080:8080 -d deegree/deegree:latest
```

Build
-----
download the dockerfile into a directory an run:

```
docker build -t deegree/deegree .
```

Access
------
open http://localhost:8080
when running docker on OS X or Windows with docker-machine then check the IP with
```
docker-machine ip <DOCKER_VM_NAME>
```
and run
open http://$IP:8080/

Security Advise
---------------
This Dockerfile uses the bundled Apache Tomcat with deegree webservices. This Apache Tomcat may be outdated! 
For deegree 3.3 this bundle is based on Apache Tomcat/6.0.29. 

