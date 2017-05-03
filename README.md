# Dropwizard Heroku Event Microservice

[![Build Status](https://travis-ci.org/damorton/dropwizardheroku-event-service.svg?branch=master)](https://travis-ci.org/damorton/dropwizardheroku-event-service) [![Coverage Status](https://coveralls.io/repos/github/damorton/dropwizardheroku-event-service/badge.svg?branch=master)](https://coveralls.io/github/damorton/dropwizardheroku-event-service?branch=master)

##Browser client API 
https://dropwizardheroku-webgateway.herokuapp.com/

##Event Microservice
https://dropwizardheroku-event-service.herokuapp.com/

A Dropwizard Heroku Event Microservice deployed to Heroku with a hosted PostgreSQL database.

## Build

- Heroku config

```
heroku config:set WEB_OPTS='-Ddw.server.connector.port=$PORT'
```

- Clone repo
```
git clone https://github.com/damorton/dropwizardheroku-webgateway.git
```
- Build
```
cd dropwizardheroku-webgateway
./gradlew stage
```
- Run
```
heroku local
```


## API Endpoints for ExampleResource

```
curl https://dropwizardheroku-event-service.herokuapp.com/v1/api/example/query?message=hello
curl https://dropwizardheroku-event-service.herokuapp.com/v1/api/example/hello
curl -X POST -d 'message=hello' https://dropwizardheroku-event-service.herokuapp.com/v1/api/example/postparam
curl -X POST -d 'hello' https://dropwizardheroku-event-service.herokuapp.com/v1/api/example/postbody
```

## API Endpoints for EventResource

```
GET curl https://dropwizardheroku-event-service.herokuapp.com/v1/api/events
GET curl https://dropwizardheroku-event-service.herokuapp.com/v1/api/events/{name}
POST curl -H "Content-Type: application/json" -X POST -d '{"name":"Sesh","description":"Drinkys","location":"Toms","date":"2017-04-11"}' https://dropwizardheroku-event-service.herokuapp.com/v1/api/events
```

## Project Structure

### Example package names:

```
com.bitbosh.dropwizardheroku.api (Resources & Representations. Communicates will all parts of the Microservice and contains Domain objects)
com.bitbosh.dropwizardheroku.service (Coordination across multiple Domain modules, multiple business transactions)
com.bitbosh.dropwizardheroku.domain (Domain Modules/Classes, this Microservices business logic)
com.bitbosh.dropwizardheroku.repositories (Dao, handles multiple Domain entities and has access to persistent storage)
com.bitbosh.dropwizardheroku.gateways (Encapsulates message passing and error handling with other Microservices)
com.bitbosh.dropwizardheroku.client (HTTP Client to communicate with other Microservices)
...
```

### Structure

```
.
├── config.yml
├── pom.xml
├── README.md
└── src
    ├── main
    │   ├── java
    │   │   └── com
    │   │       └── dropwizardheroku
    │   │	       	└── event    
    │   │      			├── api
    │   │           		├── service
    │   │           		├── domain
    │   │           		├── repositories
    │   │           		├── gateways
    │   │           		├── client
    │   │           		├── Main.java
    │   │           		├── ApplicationConfiguration.java
    │   │           		├── ...
    │   └── resources
    │       ├── assets
    │       	├── component
    │       		└── Event.jsx
    └── test
        ├── java
        │   └── com
        │       └── dropwizardheroku
        │       	└── event
        │	           	├── api
        │   	       		├── service
        │       	   	├── domain
        │         		├── repositories
        │	           	├── gateways
        │   	        	├── client
        │       	    	├── MainUnitTest.java
        │           		├── ApplicationConfigurationUnitTest.java
        │           		├── ...
        └── resources
            └── fixtures
```

# Tutorial

http://www.bitbosh.com/2017/04/microservices-with-dropwizard-on-heroku.html
