deegree/Tomcat bundle docker container
======================================

Latest deegree webservice on docker using deegree/Tomcat bundle from the deegree.org website.

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
when running docker on OS X or Windows with boot2docker then check the IP with
```
boot2docker ip
```
and run
open http://$IP:8080/