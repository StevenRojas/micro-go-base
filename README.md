# micro-go-base
Boilerplate code for Go microservices

# Folder Structure
````text
.
├── adapter
│ ├── cache
│ │ ├── cache.go
│ │ └── cache_test.go
│ └── metrics
│     ├── datadog.go
│     ├── datadog_mock.go
│     └── datadog_test.go
├── api
│ ├── proto
│ │ └── user.proto
│ └── rest
│     ├── api.yaml
│     └── postman
│         └── collection.json
├── cmd
│ ├── command
│ │ ├── app.go
│ │ ├── app_test.go
│ │ └── doc.go
│ └── main.go
├── config
│ ├── config.go
│ ├── config.yaml
│ └── config_test.go
├── docker
│ ├── Dockerfile
│ ├── Dockerfile.test
│ └── environment.sh
├── docs
│ ├── api
│ └── cli
├── go.mod
├── pkg
│ ├── error
│ │ └── error.go
│ ├── grpc
│ │ ├── pb
│ │ │ └── user.pb.go
│ │ └── user.go
│ ├── logger
│ │ ├── logger.go
│ │ └── logger_test.go
│ ├── middleware
│ │ ├── circuit_breaker.go
│ │ ├── circuit_breaker_test.go
│ │ ├── rate_limiting.go
│ │ └── rate_limiting_test.go
│ ├── model
│ │ └── user.go
│ ├── repository
│ │ ├── mysql
│ │ └── user_repository.go
│ ├── rest
│ │ ├── gin
│ │ ├── health.go
│ │ ├── router.go
│ │ └── version.go
│ ├── server
│ │ ├── grpc.go
│ │ └── http.go
│ ├── service
│ │ └── user
│ │     └── service.go
│ └── util
│     ├── util.go
│     └── util_test.go
└── scripts
    ├── migrations
    │ └── db.sql
    └── pipeline
        └── Jenkinsfile
````

## adapter
The `adapter pattern` is implemented in this folder to have a light wrapper around other microservices or third-party APIs, so that the external dependency is reduced using interfaces.
Each dependency is implemented in a subfolder, and it has its tests and even mocks that will facilitate the integration tests.

## api
This folder contains the API definition, both for REST and Protocol Buffers, it can also have the Postman collections

## cmd
CLI implementation for the app, where all commands are implemented. 
The commands could be native Golang code using config files and environment variables, but it is possible to use the [Cobra library](https://github.com/spf13/cobra), for example, to have the richest command-line interface that supports flags and inline configuration updates (without restart the service)

`main.go` is the application bootstrap that will launch one or more commands that are set in the corresponding `cmd/command` folder.
Each `command` subfolder contains the command code at `app.go` file, its tests at `app_test.go` file and the docs at `doc.go` file

## config
Configuration files (json, yaml, toml, etc.) and, code to read and validate the files and environment variables into Go structs

## docker
Docker files and environment setup scripts to have environments up and running

## docs
Service API and CLI documentation

## scripts
This folder contains different kind of scripts, for example DB migrations or CI/CD automation pipeline

## pkg
Application related code

### error
Error handlers (consider using a company's error package instead)

### grpc
GRPC services are implemented in this folder using the generated PB files

### logger
Wrapper for logger libraries (consider using a company's logger package instead)

### middleware
Middlewares to handle the request live cycle are here. For example:
* Authentication
* Audit logs
* Rate Limiting
* Circuit Breaker
* Metrics

### model
Business model definitions

### repository
Here the `Repository` pattern is applied. It should be agnostic to use Gorm or other ORM

### rest
HTTP wrapper that isolates the application services from the REST API framework/toolkit that would be used (Gin, Gorilla, etc)

### server
HTTP and GRPC server initialization

### service
This folder contains all the services provided by the application, each service is defined in its own subfolder

### util
Util functions used by the application, could be a method to get an array intersection or JWT methods