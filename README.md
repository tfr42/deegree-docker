# deegree docker containers

This projects contains different Docker containers for deegree webservices. Please consult the [deegree documentation](http://www.deegree.org/Documentation)
for further information how to configure and use deegree web services. The [Docker web site](https://www.docker.com/)
provides all information about Docker!

## Run deegree with PostgreSQL 14/PostGIS 3.3

Get docker image for PostgreSQL DB and start the container:

    % docker pull postgis/postgis:14-3.3
    % docker run -p 5432:5432 --name db -d postgis/postgis:14-3.3

see https://hub.docker.com/r/postgis/postgis/ for more information.

Then start the container with deegree webservices:

    % docker run --name deegree --link postgis:db -p 8080:8080 -d tfr42/deegree:latest

## Configure a database connection

### For PostgreSQL DB

To configure a JDBC connection connect to the [deegree console](http://localhost:8080/deegree-webservices) and enter the JDBC URL:

```
<?xml version='1.0' encoding='UTF-8'?>
<JDBCConnection xmlns='http://www.deegree.org/jdbc' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xsi:schemaLocation='http://www.deegree.org/jdbc https://schemas.deegree.org/core/3.5/jdbc/jdbc.xsd'>
  <Url>jdbc:postgresql://db:5432/postgres</Url>
  <User>postgres</User>
  <Password>postgres</Password>
  <ReadOnly>false</ReadOnly>
</JDBCConnection>
```

### For Oracle DB

To configure a JDBC connection connect to a Oracle Database use: 

```
<?xml version='1.0' encoding='UTF-8'?>
<JDBCConnection xmlns="http://www.deegree.org/jdbc" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.deegree.org/jdbc https://schemas.deegree.org/core/3.5/jdbc/jdbc.xsd">
  <Url>jdbc:oracle:thin:@db:49161:xe</Url>
  <User>system</User>
  <Password>oracle</Password>
  <ReadOnly>false</ReadOnly>
</JDBCConnection>
```

## deegree on Tomcat HOWTOs

### How to add Oracle JDBC driver to Apache Tomcat

First download the Oracle JDBC driver from [Oracle Tech Net](http://www.oracle.com/technetwork/database/features/jdbc/index-091264.html)
Then copy the JAR file into the $CATALINA_HOME/lib directory inside the docker container:

    % docker cp PATH_TO/ojdbc8.jar deegree:/usr/local/tomcat/lib

Before configuring a JDBC connection to the Oracle DB you need to restart the docker container:

    % docker restart deegree
    
### How to pass CATALINA_OPTS to Apache Tomcat

Here an example how to fix issue with Oracle JDBC when running in 'ORA-01882: timezone region not found':
 
    % docker run --env CATALINA_OPTS="-Doracle.jdbc.timezoneAsRegion=false -Duser.timezone=CET" -d deegree/deegree-tomcat
