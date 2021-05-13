# Docker Compose Example

This example illustrates how to use [Docker Compose](https://docs.docker.com/compose/) to run two simple [Spring Boot](https://spring.io/projects/spring-boot) microservices ([Data Collector](https://github.com/yaskovdev/data-collector) and [Social Rating Calculator](https://github.com/yaskovdev/social-rating-calculator)) that communicate with each other via [Kafka](https://kafka.apache.org/) and store data in [Redis](https://redis.io/).

## To Run Locally

Make sure that [Data Collector](https://github.com/yaskovdev/data-collector) and [Social Rating Calculator](https://github.com/yaskovdev/social-rating-calculator) are cloned into the same directory as this repository.

Create a working directory and clone Docker Compose Example:
```
mkdir sandbox
cd sandbox
git clone https://github.com/yaskovdev/docker-compose-example.git
```

Clone and build Data Collector and Social Rating Calculator:
```
git clone https://github.com/yaskovdev/data-collector.git
mvn -f data-collector clean package -D maven.test.skip

git clone https://github.com/yaskovdev/social-rating-calculator.git
mvn -f social-rating-calculator clean package -D maven.test.skip
```

Build and pull all the required images and start the containers:
```
cd docker-compose-example
docker-compose up
```

Send the test request:
```
curl -v -H "Content-Type: application/json" http://localhost:8080/persons \
    --data '{"first_name": "Koshchey", "last_name": "Immortal", "age": 20000}'
```

See the logs of Social Rating Calculator, the social rating for the user from the cURL request should be logged there.

You can also connect to Redis using Redis CLI (`src/redis-cli` from Redis directory) and make sure the social rating is stored there.
