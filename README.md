deegree webservices on Docker
=============================

This projects contains sample ```Dockerfile```s for building Docker images containing ready to use deegree webservices.
This includes quick start ```Dockerfile```s and samples to facilitate installation, configuration, and environment setup 
of deegree webservices running on different Java EE application servers and using different database systems for data storage.
 
Please consult the [deegree documentation](http://www.deegree.org/Documentation) for further information how to 
configure and use deegree webservices. The [Docker web site](https://www.docker.com/) provides all information 
about Docker!


Run deegree with PostgreSQL 9.4/PostGIS 2.1
--------------------------------------------

Get the Docker image for PostgreSQL 9.4 with PostGIS 2.1 extension installed and start the container with:

    % docker pull mdillon/postgis
    % docker run --name postgis -p 5432:5432 -d mdillon/postgis

see https://hub.docker.com/r/mdillon/postgis/ for more information.


Then start the container with deegree. Either use the ```Dockerfile``` for the [bundled Tomcat container](./deegree-builtin-tomcat) to build the Docker image and then run:

    % docker run --name deegree -p 8080:8080 --link postgis:db -d deegree/deegree

Or use the ```Dockerfile``` for the [deegree WAR on Tomcat 8](./deegree-webapp-tomcat) to build the Docker image and start the container with:

    % docker run --name deegree -p 8080:8080 --link postgis:db -d deegree/deegree-tomcat
    
To configure a JDBC connection for deegree use the [deegree console](http://localhost:8080/deegree-webservices) and create a JDBC connection for PostgreSQL:

```
<?xml version='1.0' encoding='UTF-8'?>
<JDBCConnection configVersion='3.0.0'  xmlns='http://www.deegree.org/jdbc' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xsi:schemaLocation='http://www.deegree.org/jdbc http://schemas.deegree.org/jdbc/3.0.0/jdbc.xsd'>
  <Url>jdbc:postgresql://localhost:5432/postgres</Url>
  <User>postgres</User>
  <Password>postgres</Password>
  <ReadOnly>false</ReadOnly>
</JDBCConnection>
```


Run deegree with Oracle DB 11g/12c and Oracle WebLogic Server 12c
-----------------------------------------------------------------

To run Oracle DB 11g inside a Docker container follow:
https://github.com/wnameless/docker-oracle-xe-11g
    
    % docker pull wnameless/oracle-xe-11g
    % docker run --name oracle11g -p 49160:22 -p 49161:1521 -d wnameless/oracle-xe-11g

To run Oracle DB 12c inside a Docker container follow:
https://github.com/wscherphof/oracle-12c

    % docker run --privileged --name oracle12g -d wscherphof/oracle-12c

To run Oracle WLS 12c (12.1 or 12.2) inside a Docker container follow:
https://github.com/oracle/docker/tree/master/OracleWebLogic

    % docker run --name wlsadmin -p 7001:7001 -d 1221-domain
    
To configure a JDBC connection for deegree use the [deegree console](http://localhost:7001/deegree-webservices) and create a JDBC connection for Oracle: 

```
<JDBCConnection xmlns="http://www.deegree.org/jdbc" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" configVersion="3.0.0" xsi:schemaLocation="http://www.deegree.org/jdbc http://schemas.deegree.org/jdbc/3.0.0/jdbc.xsd">
  <Url>jdbc:oracle:thin:@localhost:49161:xe</Url>
  <User>system</User>
  <Password>oracle</Password>
  <ReadOnly>false</ReadOnly>
</JDBCConnection>
```

deegree on Tomcat HOWTOs
========================

How to add Oracle JDBC driver to Apache Tomcat
----------------------------------------------

First download the Oracle JDBC driver from [Oracle Tech Net](http://www.oracle.com/technetwork/database/features/jdbc/index-091264.html).
Then copy the Oracle JDBC driver JAR file into the $CATALINA_HOME/lib directory inside the Docker container:

    % docker cp PATH_TO/ojdbc7.jar deegree-tomcat:/usr/local/tomcat/lib

Before configuring a JDBC connection for Oracle you need to restart the Docker container with:

    % docker restart deegree-tomcat
    
How to pass CATALINA_OPTS to Apache Tomcat
------------------------------------------

This is an example how to fix the issue with Oracle JDBC when running into the error *ORA-01882: timezone region not found*:
 
    % docker run --env CATALINA_OPTS="-Doracle.jdbc.timezoneAsRegion=false -Duser.timezone=CET" -d deegree/deegree-tomcat
    
    
deegree on Oracle Weblogic HOWTOs
=================================
TBD

Use Docker Compose to run the Docker application
================================================

Use the sample Docker Compose file ```docker-compose.yml``` to run the multi-container Docker application:

    % docker-compose up -d web 

Starts the container ```deegree-webapp-tomcat``` with ```postgis```.