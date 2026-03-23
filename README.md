# deegree docker containers

This projects contains different [container images for deegree webservices](https://hub.docker.com/r/tfr42/deegree), starting from version 3.3 to the current version 3.6. It's main purpose is to test und compare the behaviour of the different versions. To use deegree webservices for production environments use the official container images [here](https://github.com/deegree/deegree3-docker). Please consult the [deegree documentation](https://www.deegree.org/documentation)
for further information how to configure and use deegree webservices. The [Docker website](https://www.docker.com/)
provides all information about Docker!

## Official deegree container images

The OSGeo project deegree publishes it's container images here: https://hub.docker.com/r/deegree/deegree3-docker/

## Run deegree with PostgreSQL 15/PostGIS 3.5

Get docker image for PostgreSQL DB and start the container:

    % docker pull postgis/postgis:15-3.5
    % docker run -p 5432:5432 --name db -e POSTGRES_PASSWORD=secretpassword -d postgis/postgis:15-3.5

see https://hub.docker.com/r/postgis/postgis/ for more information.

Then start the container with deegree webservices:

    % docker run --name deegree --link db:db -p 8080:8080 -d tfr42/deegree:latest

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
 
    % docker run --env CATALINA_OPTS="-Doracle.jdbc.timezoneAsRegion=false -Duser.timezone=CET" -d tfr42/deegree:latest
