# Social Rating Docker Compose

## To Run Locally

Make sure that [Data Collector](https://github.com/yaskovdev/data-collector) and [Social Rating Calculator](https://github.com/yaskovdev/social-rating-calculator) are cloned into the same directory as this repository.

Build Data Collector and Social Rating Calculator:

```
mvn -f ../data-collector clean package -D maven.test.skip
mvn -f ../social-rating-calculator clean package -D maven.test.skip
```

Build the services:

```
docker-compose build
```

Run the services:
```
docker-compose up
```

Send the test request:
```
curl -v -H "Content-Type: application/json" http://localhost:8080/persons --data '{"first_name": "Koshchey", "last_name": "Immortal", "age": 20000}'
```

See the logs of Social Rating Calculator, the social rating for the user from the cURL request should be logged there.

You can also connect to Redis using Redis CLI (`src/redis-cli` from Redis directory) and make sure the social rating is stored there.
