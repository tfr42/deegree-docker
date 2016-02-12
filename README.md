deegree docker containers
=========================

This projects contains different Docker containers for deegree webservices. Please consult the [deegree documentation](http://www.deegree.org/Documentation)
for further information how to configure and use deegree web services. The [Docker web site](https://www.docker.com/)
provides all information about Docker!


Run deegree with PostgreSQL 9.4/PostGIS 2.1
--------------------------------------------

Get docker image for PostgreSQL DB and start the container:

    % docker pull mdillon/postgis
    % docker run -p 5432:5432 --name postgis -d mdillon/postgis

see https://hub.docker.com/r/mdillon/postgis/ for more information.


Then start the container with deegree. Either use the [bundled Tomcat container](./deegree-builtin-tomcat) with:

    % docker run --name deegree --link db:db -p 8080:8080 -d deegree/deegree

Or use the [deegree WAR on Tomcat 8](./deegree-webapp-tomcat) with:

    % docker run --name deegree --link postgis:db -p 8080:8080 -d deegree/deegree-tomcat
    
To configure a JDBC connection connect to the [deegree console](http://localhost:8080/deegree-webservices) and enter the JDBC URL:

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

To run Oracle DB 11g on Docker follow:
https://github.com/wnameless/docker-oracle-xe-11g
    
    % docker pull wnameless/oracle-xe-11g
    % docker run -p 49160:22 -p 49161:1521 --name oracle11g -d wnameless/oracle-xe-11g

To run Oracle DB 12c on Docker follow:
https://github.com/wscherphof/oracle-12c

    % docker run --privileged --name oracle12g -d wscherphof/oracle-12c

To run Oracle WLS 12c (12.1 or 12.2) on Docker follow:
https://github.com/oracle/docker/tree/master/OracleWebLogic

    % docker run -p 7001:7001 --name wlsadmin -d 1221-domain
    
To configure a JDBC connection connect to the [deegree console](http://localhost:7001/deegree-webservices) and enter the JDBC URL: 

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

First download the Oracle JDBC driver from [Oracle Tech Net](http://www.oracle.com/technetwork/database/features/jdbc/index-091264.html)
Then copy the JAR file into the $CATALINA_HOME/lib directory inside the docker container:

    % docker cp PATH_TO/ojdbc7.jar deegree:/usr/local/tomcat/lib

Before configuring a JDBC connection to the Oracle DB you need to restart the docker container:

    % docker restart deegree
    
How to pass CATALINA_OPTS to Apache Tomcat
------------------------------------------
Here an example how to fix issue with Oracle JDBC when running in 'ORA-01882: timezone region not found':
 
    % docker run --env CATALINA_OPTS="-Doracle.jdbc.timezoneAsRegion=false -Duser.timezone=CET" -d deegree/deegree-tomcat
    
    
deegree on Oracle Weblogic HOWTOs
=================================
TBD