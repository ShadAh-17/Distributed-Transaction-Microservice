# Distributed transactions in microservices

In this project I'm demonstrating a simple architecture of microservices that perform distributed transactions. The example application applications are simple Spring Boot app that expose some HTTP endpoints for CRUD operations and connects to Postgres using Spring Data JPA.

## Getting Started 

## Usage
1. Start discovery-server. It is available on port 8761.
2. Start RabbitMQ on Docker with command `docker run -d --name rabbit -h rabbit -p 5672:5672 -p 15672:15672 rabbitmq:3-management`
3. Start transaction-server
4. Start Postgres on Docker with command `docker run -d --name postgres -p 5432:5432 -e POSTGRES_USER=trx -e POSTGRES_PASSWORD=trx123 -e POSTGRES_DB=trx postgres`
4. Start microservices: account-service, product-service and order-service. The app order-service is listening on port 8080.
5. Add some test data to product-service and account-service
5. Send some tests requests. For example: `$ curl http://localhost:8080/orders -H "Content-Type: application/json" -d "{\"productId\":1, \"count\":10, \"customerId\":1}"`

## Docker
You can test all the apps on Docker. To do that first build the whole project using the following command:
```shell
$ mvn clean package -DskipTests -Pbuild-image
```

Then you can just run all the apps including RabbitMQ and Postgres with `docker-compose`:
```shell
$ docker compose up
```