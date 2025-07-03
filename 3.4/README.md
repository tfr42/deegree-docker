deegree webservice 3.4 from the deegree.org website using Apache Tomcat 8.5 with OpenJDK 1.8.

## Build
    docker build --rm --load -t tfr42/deegree:3.4 .

## Run
    docker run -d --name deegree34 -p 8081:8080 tfr42/deegree:3.4