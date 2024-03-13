# deegree v3.5 on Tomcat 9 with JDK 11

Latest deegree webservice from the deegree.org website using Apache Tomcat 9 with OpenJDK 11.

## Build

To build a docker image run:

    % docker build --rm --load -t tfr42/deegree:3.5 .

## Usage

To run a container use:

    % docker run -d --name deegree35 -p 8082:8080 tfr42/deegree:3.5

## Access

Enter the address into a browser: http://localhost:8082/deegree-webservices or run:

    % open http://$IP:8082/deegree-webservices

where $IP is the IP address of host.

## Documentation

The documentation is accessible at http://localhost:8082/deegree-webservices-handbook-3.5.6/index.html