# spring-app-config

Shared `application.yaml` used by Spring Cloud microservices to register with a Eureka service discovery server. Point multiple services at this config to keep their Eureka wiring consistent.

## What's in here

`application.yaml` with Eureka client defaults:

```yaml
eureka:
  instance:
    prefer-ip-address: true
  client:
    fetch-registry: true
    register-with-eureka: true
    service-url:
      defaultZone: ${EUREKA_SERVER_ADDRESS:http://localhost:8761/eureka}
```

## Usage

Point a Spring Boot service at this config in one of these ways:

**1. As an external config location**

```bash
java -jar myservice.jar --spring.config.location=classpath:/,file:./spring-app-config/application.yaml
```

**2. As part of a Spring Cloud Config Server**

Host this file in a Git repo and configure Spring Cloud Config to serve it:

```yaml
# config-server application.yaml
spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/svrohith9/spring-app-config
```

## Override the Eureka URL

Set the `EUREKA_SERVER_ADDRESS` environment variable to point at a non-localhost Eureka registry:

```bash
export EUREKA_SERVER_ADDRESS=http://eureka.prod.example.com:8761/eureka
```

## License

MIT
