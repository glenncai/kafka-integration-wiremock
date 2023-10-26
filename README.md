# Spring Boot Kafka Integration - Standalone WireMock

The associated repository for the Dispatch Service can be found here:  [Dispatch Service Repository](https://github.com/glenncai/spring-boot-kafka-integration)

This project contains a standalone WireMock implementation that represents a third-party Stock Service which is called by the Dispatch Service and used to trigger retry scenarios.

<br />

## Stock Service API

The API call is in the following format:

```
GET /api/stock?item=myItem
```

The wireMock is primed to return the following responses:

- `400` - if the item ends with the string `_400` e.g. `GET /api/stock?item=myItem_400`
- `500` - if the item ends with the string `_500`
- `502` - if the item ends with the string `_502` fail the first call then succeed. This allows for retry testing.
- `200` - for all other items

<br />

## Run the WireMock

First download the WireMock standalone jar file using the instructions found here:
https://wiremock.org/docs/download-and-installation/

Copy the jar to this project directory.

Run the WireMock by using the following command (replacing wiremock-standalone-3.2.0.jar with the name of the downloaded jar file): 
```
java -jar wiremock-standalone-3.2.0.jar --port 9001
```

The service will start on port `9001`, which is where the Dispatch Service will attempt to call it.