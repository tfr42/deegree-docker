docker build --rm --load -t tfr42/deegree:3.3.21 -t tfr42/deegree:3.3 .
docker run -d --name deegree33 -p 8080:8080 tfr42/deegree:3.3