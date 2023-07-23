# deegree v3.5 on Tomcat 

Latest deegree webservice from the deegree.org website using Apache Tomcat 9 with OpenJDK 11.

## Build

To build a docker image run:

    % docker build --rm --load -t tfr42/deegree:3.5.0  -t tfr42/deegree:3.5 -t tfr42/deegree:latest .

## Usage

To run a container use:

    % docker run -p 8080:8080 -d deegree/deegree:3.5.0
    % docker run -d --name deegree35 -p 8082:8080 tfr42/deegree:3.5

## Access

Enter the address into a browser: http://localhost:8080/deegree-webservices or run:

    % open http://$IP:8080/deegree-webservices

where $IP is the IP address of host.