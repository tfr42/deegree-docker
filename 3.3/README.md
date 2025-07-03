deegree webservice 3.3 from the deegree.org website using Apache Tomcat 8.5 with OpenJDK 1.8.

## Build
    docker build --rm --load -t tfr42/deegree:3.3 .

## Run
    docker run -d --name deegree33 -p 8080:8080 tfr42/deegree:3.3