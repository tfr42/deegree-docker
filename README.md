deegree docker containers
=========================

This projects contains different docker containers for deegree webservices.


Run deegree with PostgreSQL 9.x/PostGIS 2.1
--------------------------------------------

Get docker image for PostgreSQL DB and start the container:

```
docker pull mdillon/postgis

docker run -p 5432:5432 --name db -d mdillon/postgis
```

see https://hub.docker.com/r/mdillon/postgis/ for more information.


Then start the container with deegree:

```
docker run --name deegree --link db:db -p 8080:8080 -d deegree/deegree
```

Run deegree with Oracle DB and Oracle WebLogic Server
-----------------------------------------------------

To run Oracle DB on Docker follow:
https://github.com/wnameless/docker-oracle-xe-11g

To run Oracle WLS on Docker follow:
https://github.com/oracle/docker/tree/master/OracleWebLogic