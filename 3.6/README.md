deegree webservice 3.6 from the deegree.org website using Apache Tomcat 10.1 with OpenJDK 17.

## Build
    docker build --rm --load -t tfr42/deegree:3.6 .

## Run
    docker run -d --name deegree36 -p 8081:8080 tfr42/deegree:3.6