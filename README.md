# City Population
Playground for Kafka and Akka-Streams

The goal is to grow a city based on life-events read from a Kafka queue. The life-events come in random order, but need to be processed in a specific order. The proper order is explained below. If an event comes in the incorrect order, it should be requeued, and a log line should be printed. If the event doesn't need to be handled, it should be ignored and logged on debug level.

## Live-Events
### Valid Events: 
`Birth`, `Adulthood`, `Partner`, `Children`, `Education`, `Death`

### Ignored Events: 
`Travels`, `Accidents`

### Restrictions: 
Children can only happen after Adulthood and Partner
Nothing can happen until Birth
Nothing can happen after Death
Death can happen at any moment
Partner can only happen after Adulthood 

### Sample Life-Events Queue: 
```
Birth-1
Birth-2
Travel-1
Birth-3
Adulthood-1
Birth-4
Adulthood-5
Education-1
Birth-5
Adulthood-3
Death-2
Partner-1-2
Partner-1-3
Children-1-3
```


### API

The state of the city needs to be maintained and be able to be queried via an API. 

GET /inhabitant/:id   => Returns Events for a specific inhabitant
GET /city             => Returns total population
GET /city/adults      => Returns number of Adults
GET /city/partners    => Returns number of Partner


### Tech Stack
The application should be written with: 
- Akka Streams for processing the events
- Kafka for emitting the events
- Finch for the api
- Free to use any kind of storage that suits your needs (e.g. in memory, neo4j, akka)

The final api is described in OpenAPI specifications (a.k.a. Swagger file). 
