deegree docker container
========================

latest deegree webservice with docker using tomcat+deegree bundle from the deegree.org website

Usage
-----

```
docker run -p 8080:8080 -d martinvi/deegree:latest
```

Build
-----
download the dockerfile into a directory an run:

```
docker build -t martinvi/deegree .
```
