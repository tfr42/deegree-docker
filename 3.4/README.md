docker build --rm --load -t tfr42/deegree:3.4 .
docker run -d --name deegree34 -p 8081:8080 tfr42/deegree:3.4